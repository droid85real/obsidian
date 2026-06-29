MINIO playlist
https://www.youtube.com/playlist?list=PLFOIsHSSYIK37B3VtACkNksUw8_puUuAC
watch video: 1 to 6 , 8, 14, 15, 17


up and runnin minio using docker
https://youtu.be/zqjsw4O2-4U?list=PLFOIsHSSYIK37B3VtACkNksUw8_puUuAC


---
Docker for minio s3
```
docker run -d \
--name minio \
--restart no \
-p 9000:9000 \
-p 9001:9001 \
-e MINIO_ROOT_USER=admin \
-e MINIO_ROOT_PASSWORD=admin123 \
-v ~/minio-data:/data \
quay.io/minio/minio server /data --console-address ":9001"
```

http://localhost:9001 for web UI
port: 9000 for s3 endpoint

---
Don't use the root user for client access.
create dedicated user per application
user access should follow the principle of least privilege

###### Create user per application

**install CLI**
```
wget https://dl.min.io/client/mc/release/linux-amd64/mc
chmod +x mc
sudo mv mc /usr/local/bin/
```

**One time only :**
```
mc alias set local http://localhost:9000 admin admin123
```

**Create User :**
```
mc admin user add local user1 user1password
```

**To Check User :**
```
mc admin user list local
```
or
```
mc admin user info local user1
```

(skip) **Add permission : (not recommended as it give access to all bucket readwrite) **
```
mc admin policy attach local readwrite --user user1
```

(skip) **To detach readwrite:**
```
mc admin policy detach local readwrite --user user1
```

Then create a file
`nano vaultlearn-policy.json`

```json
{
 "Version":"2012-10-17",
 "Statement":[
   {
     "Effect":"Allow",
     "Action":[
       "s3:GetObject",
       "s3:PutObject",
       "s3:DeleteObject"
     ],
     "Resource":[
       "arn:aws:s3:::vaultlearn/*"
     ]
   },
   {
     "Effect":"Allow",
     "Action":[
       "s3:ListBucket"
     ],
     "Resource":[
       "arn:aws:s3:::vaultlearn"
     ]
   }
 ]
}
```
Two things are happening here:
• first rule → operate on objects inside the bucket  
• second rule → allow listing the bucket itself

**To upload policy to server :**
```
mc admin policy create local vaultlearn-policy vaultlearn-policy.json
```

**To list all policy :**
```
mc admin policy list local
```

**Add policy to created user :**
```
mc admin policy attach local vaultlearn-policy --user user1
```

**all the code for faster setup :**
```
mc admin user add local vaultlearn vaultlearnpass
mc admin policy create local vaultlearn-policy vaultlearn-policy.json
mc admin policy attach local vaultlearn-policy --user vaultlearn
```

---

###### **Permission mismatch between host and container**
if suddenly **user, bucket and policy disappear** as if they never existed in first place

Your directory is owned by:

root root

Containers often run MinIO as **UID 1000** internally.

If the process cannot safely write metadata files during IAM updates (user creation, policy attach), those writes may partially succeed. Later on restart, MinIO rebuilds metadata and the IAM entries vanish.

Fixing ownership eliminates that instability:

```
sudo chown -R 1000:1000 ~/minio-data
```


---
###### Testing using alias

The “temporary alias” is just a **testing lens**. Nothing mystical. It lets you interact with the same server using **different credentials** without constantly reconfiguring your main alias.

Right now your `mc` setup looks like this:

```id="5y7f35"
local → http://localhost:9000
AccessKey: admin
```

That means every command you run like:

```id="v2b2p4"
mc ls local
```

is executed with **root credentials** (`admin/admin123`). Root can see **everything**. So if you test permissions with that account, you learn nothing about whether your policy works.

The alias trick creates a second “identity” in the CLI.

```
mc alias set vaultlearn-user http://localhost:9000 user1 user1password
```

Now your CLI has two perspectives:

```
local            → root user
vaultlearn-user  → restricted user
```

So when you run:
```
mc ls vaultlearn-user
```

the request goes to MinIO as **user1**, not admin.

This reveals whether your policy is actually working.

Example outcome:
```id="y1nqwr"
mc ls local
```

might show
```id="b3n2qp"
vaultlearn
logs
backup
private
```

But:
```id="u5v7r1"
mc ls vaultlearn-user
```

should show only
```id="x4c8mf"
vaultlearn
```

If the policy is correct, the user literally **cannot even see other buckets**.

That’s the purpose of the alias.

Think of it like wearing different security badges in a building:

```id="v6h4z8"
admin badge   → opens every door
user badge    → opens only one room
```

You test the badge by walking around the building.

The CLI alias is just the **badge swap**.

One more practical engineering note: this alias is only for **debugging**. In your VaultLearn backend you will never use `mc`. Your Node server will instead use the S3 SDK with:

```id="g7c4p9"
accessKeyId: user1
secretAccessKey: user1password
```

to generate **pre-signed URLs**. The alias simply lets you simulate what that restricted user can or cannot do before you wire it into your code.





---

**To create bucket :**
```
mc mb local/vaultlearn
```

**List buckets :**
```
mc ls local
```

**List objects in your bucket :**
```
mc ls local/vaultlearn
```

---

`ls -la ~/minio-data/.minio.sys`

```
MinIO metadata tree
└── .minio.sys
    ├── buckets      → bucket definitions
    ├── config       → users, policies, settings
    ├── multipart    → unfinished uploads
```


---
###### prefix and objects
+ think prefix as a directory or file path
+ A prefix becomes part of the path to access Object
+ and objects are immutable
+ and think of buckets as drives and Object as files
+ A prefix only exists in MINIO if there are objects with the prefix
+ An object only exists in one prefix (You cannot have the same object simultaneously appear in multiple prefixes like a filesystem shortcut.)


In **MinIO** (and any system compatible with **Amazon S3**) the hierarchy works like this:
```
bucket → object key → object data + metadata
```

Example bucket:
```
vaultlearn
```

Inside that bucket you might upload something that _looks_ like a folder structure:
```
vaultlearn/
   courses/
      math101/
         lecture1.mp4
```

But internally there is **no folder**. The actual object key stored in the system is simply:
```
courses/math101/lecture1.mp4
```

That entire string is the **object key**.

Now the term **prefix** just means “the beginning part of the object key”.
Example:
```
courses/math101/lecture1.mp4
```

Possible prefixes:
```
courses/
courses/math101/
courses/math101/lecture1
```

The storage system uses prefixes to filter objects.

For example, this command:
```bash
mc ls local/vaultlearn/courses
```

is basically asking the server:
```
list objects whose key starts with "courses/"
```

That’s all a prefix really is.
The mental model becomes:
```
Bucket
 ├── courses/math101/lecture1.mp4
 ├── courses/math101/lecture2.mp4
 └── courses/physics201/lecture1.mp4
```

There are no real directories—only **keys that share prefixes**.

This design is the reason object storage scales absurdly well. Traditional filesystems need complex directory trees and locking. Object storage just stores billions of keys in distributed indexes.

One subtle property of object storage worth remembering: objects are immutable. You don’t edit a file in place. If something changes, the system writes a new object with the same key. That behavior influences how systems like backup engines, data lakes, and media platforms are designed.


---

AWS S3 overview: https://youtu.be/d8A8JmAImc4

AWS S3 in nodejs by piyush: https://youtu.be/DOUxRYi2Fwg
s3 client and presigned url in vid at 18:00 

IAM and policy: https://youtu.be/MDM8AraFgUE


----
#### MinIO Webhook Event Configuration
You must configure a bucket notification.

`hostname -I` to get ip address

```
mc admin config set local notify_webhook:primary \
endpoint="http://192.168.1.8:3000/api/webhooks/upload-completed" \
enable="on"
```

To restart
```
mc admin service restart local
```

To verify
```
mc admin config get local notify_webhook
```

attach the bucket event:
```
mc event add local/vaultlearn \
arn:minio:sqs::primary:webhook \
--event put
```

verify
```
mc event list local/vaultlearn
```


Can MinIO's network reach your backend?
```
docker run --rm alpine/curl \
curl http://192.168.1.8:3000/api/webhooks/upload-completed
```

