**Hello Developers!**
Library Management System is a simple project which I built to improve my understanding about MongoDB and backend connections along with the use of password authentication to enhance security using bcrypt library. After entering the password, this project allows the librarian to add, edit and delete the details of various books (CRUD operations) in the library's database. Here are some tips to setup this project in your systems.

# Setup instructions

# 2 tables are required
The connections to these tables are stored in a **.env** file. 
Create a '.env' file and add your MongoDB URIs to connect to MongoDB.

# .env file
MONGO_URI_LOGINS=your_mongodb_connection_string_here
MONGO_URI_BOOKS=your_mongodb_connection_string_here

**NOTE : If you want passwords other than the ones which I have defined, you can directly make changes in the 'base.js' in your system.**

# 1.) For storing the hashed passwords [loginDB.js]
**Design your MongoDB table 'Logins' according to the schema given here and also make a 'loginDB.js' according to the code given below.**
require("dotenv").config();
const mongoose = require("mongoose")
const { Schema } = mongoose;
const conn1 = mongoose.createConnection(process.env.MONGO_URI_LOGINS,{
    useNewUrlParser: true,
    useUnifiedTopology: true
})
const loginDetails = new Schema({
    Password: { type: String, required: true }
}, { versionKey: false });
const Logins = conn1.model("Login", loginDetails)
module.exports = { conn1, Logins }

# 2.) For maintaining the details of the books [booksDB.js]
**Design your MongoDB table 'Books' according to the schema given here and also make a 'booksDB.js' according to the code given below.**
require("dotenv").config();
const mongoose = require("mongoose")
const { Schema } = mongoose;
const conn2 = mongoose.createConnection(process.env.MONGO_URI_BOOKS, {
    useNewUrlParser: true,
    useUnifiedTopology: true
})
const blogSchema = new Schema({
    bid: { type: String, required: true, unique: true },
    name: String,
    author: String,
    publisher: String,
    genre: String,
    availability: String,
    total_copies: String
});
const Books = conn2.model("books", blogSchema)
module.exports = { conn2, Books }

**Once all these files are setup, Library Management System should run smoothly in your systems. Let me know if there is any issue.**
