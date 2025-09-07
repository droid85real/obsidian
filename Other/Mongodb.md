https://www.mongodb.com/docs/manual/crud/

+ download mongodb , mongodb shell (for CLI) and mogodb compass (for GUI)
+ `mongod --version` To check mongodb version
+ `mongosh --version` To check shell version

**Table** in relational DB is called **Collection** in mongodb
**Row** in relational DB is called **Document** in mongodb
**Column** in relational DB is called **Attribute** in mongodb


# CLI (mongosh)
+ `C:\Program Files\MongoDB\Server\7.0\bin>mongosh` To start mongosh shell
+ `show dbs` To list all db
+ `use dbname` To switch or to create db , If it doesn’t exist yet, it’s created when you store data.
+ `show collections` To see all collections in the current db

To insert data
```json
db.users.insertOne({ name: "Alice", age: 25 })

db.users.insertMany([
  { name: "Bob", age: 30 },
  { name: "Charlie", age: 28 }
])
```

To Find / Read data
```json
db.users.find(); //show all documents
db.users.find().pretty() //pretty print
db.users.find({name:"Alice"}) // Filter
db.users.find({age: {$gt:25} }) // age > 25
```

To update data
```json
db.users.updateOne(
	{ name: "Alice" }, // Filter
	{ $set: { age: 26} } // Update
)

db.users.updateMany(
	{ age: $lt: 30 }, // Filter
	{ $inc: {age: 1} } // Increase age by 1
)
```

To delete data
```json
db.users.deleteOne( {name: "Alice"} ) // Delete one

db.users.deleteMany(
	{ age: { $gte: 30 } } // Delete all greater than equal to 30
)

db.users.deleteOne({_id: ObjectId("64d4f2a2a3b4c5d6e7f8g9h0") }) // Delete using object Id
```


Count documents
```json
db.users.countDocuments() 

db.users.countDocuments({ age: 26 })

db.users.countDocuments({ years: {$exists: true} }) // return count of all documents having year irrespective of their value
```

Drop (delete) collection or database
```json
db.users.drop() // Delete collection

db.dropDatabase() // Delete current DB
```

Indexes (for performance)
```json
db.users.createIndex({ name: 1 }) // Ascending

db.users.getIndexes()
```

Helpful commands
```json
cls // clear screen
help // see shell commands
db.help() // DB-specific help
```

MongoDB shell is JavaScript-based — you can run JS commands:
```js
for(let i=1; i<=5, i++){
	db.numbers.insertOne({ num: i })
}
```


No build in undo for delete
```json
db.collectionName.updateOne(
	{ _id: ObjectId("...") }, // Filtering
	{ $set: { deleted: true } } 
);
```
Instead of deleting, mark documents as deleted.
Then exclude documents where deleted: true in your queries.
This lets you “undo” by clearing the flag.






TODO: MongoDB operators






---

## Mongodb in nodejs

#### Native Mongodb driver
https://www.npmjs.com/package/mongodb
https://www.mongodb.com/blog/post/quick-start-nodejs-mongodb-how-to-get-connected-to-your-database
+ `npm i mongodb` To install mongodb package
+ config in mongodb.js

```js
// mongodb.js
import dotenv from "dotenv";

//config
dotenv.config();
 
import { MongoClient } from "mongodb";
console.log("MONGO_URI:", process.env.MONGO_URI);

const client =new MongoClient(process.env.MONGO_URI);

const connectToMongoDB = async() => {
    try {
        await client.connect(); //returns promise
        console.log("MongoDB is connected");
        return client.db(process.env.DB_NAME); //return DB instance for later use
    } catch (error) {
        console.error("MongoDB connection failed",error);
        process.exit(1);
    }
};

export default connectToMongoDB;
```
+ can also be done with then and catch


calling `connectToMongoDB()` in index.js
```js
// index.js

// Start server only after DB connection
const startServer=async()=>{
    try {
    const db=await connectToMongoDB(); // connect to mongodb
    server.locals.db=db; // store in app locals
    
    server.listen(PORT,()=>{ //listening on port , dtart after connecting to db
        console.log(`server is listening on ${PORT}`);
    });
    } catch (error) {
        console.error("Failed to start server",error);
        process.exit(1);
    }
};

startServer(); // call function
```


#### **Sign Up** (ecommerce project)

user.controller.js
```js
export default class UserController{
    
    async postSignUp(req,res){ //postSignUp middleware
        try {
            const db=req.app.locals.db; // inject db
            const userRepo=new UserRepository(db);

            //before creating, creating check if user already exists
            const existingUser=await userRepo.findByEmail(req.body.email);

            if(existingUser){
                return res.status(400).json({ message: "Email already registered"});
            }

            const newUser=await userRepo.signUp(req.body);

            return res.status(201).json(newUser);
        } catch (error) {
            console.error(error);
            return res.status(500).json({ message: "Internal Server Error" });
        }
    }
}
```

user.repository.js
```js
import UserModel from "./user.model.js";

export default class UserRepository {
  constructor(db) {
    this.collection = db.collection("users");
  }

  async signUp({name,email,password,type}) {
    try {
      // create document
      const newUser = new UserModel(name,email,password,type);

      // insert document
      await this.collection.insertOne(newUser);

      return newUser;
    } catch (error) {
      throw new Error("Error inserting user: " + error.message);
    }
  }

  async findByEmail(email) {
    return await this.collection.findOne({ email });
  }
}
```

user.model.js
```js
export default class UserModel {
  constructor(name, email, password, type) {
    this.name = name;
    this.email = email;
    this.password = password;
    this.type = type;
  }
}
```

















week8|topic2|lec1
