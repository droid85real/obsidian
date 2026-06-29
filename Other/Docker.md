
container = process
volume = disk
image = blueprint


`docker container ls`
`docker container a`

`docker start <container_name>`
`docker stop <container_name>`


`docker exec -it <container_name> bash`

`docker run -it <image_name>`

`docker exec <container_name> <command>`

`docker images ls`
`docker container ls`

###### PORT mapping
`docker run -it -p <your_device_port>:<container_port> -p <your_device_port>:<container_port> <image>`

###### environment variable
`docker run -it -p <your_device_port>:<container_port> -e key=value -e key=value <image>`


###### Application dockerization
https://youtu.be/31k6AtW-b3Y?t=2561

create file with name `DockerFile`


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

with webhook
```
docker run -d \
  --name minio \
  --restart no \
  -p 9000:9000 \
  -p 9001:9001 \
  -e MINIO_ROOT_USER=admin \
  -e MINIO_ROOT_PASSWORD=admin123 \
  -e MINIO_NOTIFY_WEBHOOK_ENABLE_PRIMARY=on \
  -e MINIO_NOTIFY_WEBHOOK_ENDPOINT_PRIMARY=http://192.168.1.6:3000/api/webhooks/upload-completed \
  -v ~/minio-data:/data \
  quay.io/minio/minio server /data --console-address ":9001"
```

---

Docker for mongodb

```
docker run -d \
  --name mongodb \
  -p 27017:27017 \
  -v mongodb_data:/data/db \
  mongo:8
```