# MongoDB Notes

MongoDB Compass: https://www.mongodb.com/products/tools/compass

MongoSSH: https://www.mongodb.com/try/download/shell

You can use GUI or CLI version like MongoSSH / or in VS code (Require to install MongoDB extension first)

## Commands:

### << Database Basics >>

cls - clear screen

exit - exit MongoDB terminal

show dbs - show databases in MongoDB

use [databaseName] - use database (ex: use admin) [visible in the database’s list]

db.createCollection(”[collectionName]”) - create a database collection (ex: db.createCollection(”school”)

db.dropDatabase() - drop the database 

### << Insertion >>

db.[databaseName].insertOne({}) - insert one document/details inside the database (ex: db.students.insertOne({name: “Daniel”, age: “XX”, GPA: “4.0”}) )

db.[databaseName].find() - find the database details that are inserted.

db.[databaseName].insertMany([{}]) - insert multiple documents/details (ex: db.students.insertMany([{name: “Daniel”, age: “XX”, GPA: “4.0”}, {name: “Jack” , age: “XX”, GPA: “3.7”}, {name: “Petro”, age: “20”, GPA: “3.5”}])

### << Datatypes>>

Strings - “ “ (double quote) (ex: name)

Integers - No need to quote just insert number. (ex: 1234)

Doubles - ex: 1.23

Booleans - True or false (ex: isMale: True)

Date - Show Date (ex: new Date(), graduationDate: null (null means no value))

Array - [] (ex: [”RMCT”, “DSTR”, “FWDD”]

Nested Documents (use curvy brackets)- {} (ex: {street: “123 ABC”, city: “ABC”, zip: “12345”})

### << Sorting & Limiting >>

db.[databaseName].find().sort({}) - by which field which should be sorted? 

Ascending Order

(ex: db.[databaseName].find().sort({name: 1})

Descending Order

(ex: db.[databaseName].find().sort({name: -1})

db.[databaseName].find().limit() - by which field should be limited?

(ex: db.[databaseName].find().limit(3)) - it will limit 3 documents as shown in the output for example.

Combining sort and limit methods

(ex: db.students.find().sort({gpa: -1}).limit(1) )

(ex: db.students.find().sort({gpa: 1}).limit(1) )

### << Find >>

db.[databaseName].find() - find documents and check documents.

formula:

db.[databaseName].find({query}, {projection})

(ex: db.students.find({fullTIme:false}) )

Projection Parameter Usage Examples:

(ex: db.students.find({}, {name:true}) )

(ex: db.students.find({}, {_id: false, name:true}))

### << Update >>

formula:

db.[databaseName].updateOne(filter, update) - update only one document.

set -

(ex: db.students.updateOne({name: “Spongebob”}, {$set: {fullTime: true}}) )

unset - 

(ex: db.students.updateOne({name: “Spongebob”}, {$unset: {fullTime: “”}}) )

formula:

db.[databaseName].updateMany({filter, update}, {filter, update})

(ex: db.students.updateMany({},, {$set:{fullTImel:false}}} ) 

exists - 

db.[databaseName].updateMany({filter, update}..}

(ex: db.students.updateMany{(fullTime: {$exists: false}}, {$set: {fullTime: true}}} ) 

### << Delete >>

formula:

db.[databaseName].deleteOne({filter, delete}) - delete one document

(ex: db.students.deleteOne({name: “Garry”}} )

formula:

db.[databaseName].deleteMany({filter, delete}, {filter, delete}})

(ex: db.students.deleteMany({registerDate: {$exists: false}}) ) 

### << Comparison Operators >>

- Return Data based on comparison.

formula:

$ne = not equal

db.[databaseName].find({example: {$ne: “example”}})

$lt = less than

$lte = less than equal

db.[databaseName].find({example: {$lte: 23}})

$gt = greater than

$gte = greater than equal

db.[databaseName].find({example: {$gte: 23}})

$in = in operator

db.[databaseName].find({name:{$in:[”Example”, “Test1”, “Test2”]}})

$nin = not in operator

db.[databaseName].find({name:{$nin:[”Example”, “Test1”, “Test2”]}})

### << Logical Operators >>

formula:

$and = and operator

db.[databaseName].find({$and: [{isFullTime: true}], {age:{$lte:22}]})

$or = or operator

db.[databaseName].find({$or: [{isFullTime: true}], {age:{$lte:22}]})

$nor = neither or operator

db.[databaseName].find({$nor: [{isFullTime: true}], {age:{$lte:22}]})

$not = not operator

db.[databaseName].find({age:{$Not:{$gte:30}}})

$and = joins query clauses and return all documents that match both condition of both clauses.

$not = inverts the effect of query expression and returns documents that do not match the query expression.

$nor = joins query clauses and return all documents that fail to match both clauses.

$or = join query clauses and return all documents that match the conditions of either clauses.

### << Indexes >>

db.[databaseName[.find({example: “Daniel”}).explain(”executionStats”) - this command use to explain the stats.

formula:

db.[databaseName].createIndex({test: 1}) for example

db.[databaseName].getIndexes()

db.[databaseName].dropIndex(”example_1”)

### << Collections>>

A collection is a group of documents

A database is a gruop of collections

commands:

show collections

create a collection (capped here is to set a maximum size) - db.createCollection(”example”, {capped:true, size:10000000, max:100}, {autoIndexId: true/false)

There are some pros and cons for indexing but should be fine either way.