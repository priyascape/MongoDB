# Using MongoDB

//Create a database called 'my_first_db'.
use my_first_db
 
//Create students collection.
db.createCollection("students")

//Each document you insert into this collection should have the following format: ({name: STRING, home_state: STRING, lucky_number: NUMBER, birthday: {month: NUMBER, day: NUMBER, year: NUMBER}})
db.students.insert({name: "John Smith", home_state: "London", lucky_number: 7, birthday:{month:8, day:19, year:1970}})

//Create 5 students with the appropriate info.
db.students.insert({name: "John Smith", home_state: "London", lucky_number: 7, birthday:{month:8, day:19, year:1970}})
db.students.insert({name: "Richard Hartley", home_state: "Cambridge", lucky_number: 3, birthday:{month:1, day:21, year:1980}})
db.students.insert({name: "Eleanor Rigby", home_state: "Birmingham", lucky_number: 11, birthday:{month:2, day:14, year:1993}})
db.students.insert({name: "Trevor Bailey", home_state: "Solihull", lucky_number: 18, birthday:{month:9, day:19, year:1984}})
db.students.insert({name: "Chaka Khan", home_state: "Matunga", lucky_number: 1, birthday:{month:11, day:1, year:2001}})

//Get all students.
db.students.find({})
db.students.find({}).pretty()   

//Retrieve all students who are from California (San Jose Dojo) or Washington (Seattle Dojo).
db.students.find({home_state: "London"}) 

//Get all students whose lucky number is greater than 3
db.students.find({lucky_number: {$gt: 3}}).pretty() 

//Get all students whose lucky number is less than or equal to 10
db.students.find({lucky_number: {$lte: 10}}).pretty() 

//Get all students whose lucky number is between 1 and 9 (inclusive)
db.students.find({lucky_number: {$gte: 1, $lte: 9}}).pretty() 

//Add a field to each student collection called 'interests' that is an ARRAY. It should contain the following entries: 'coding', 'brunch', 'MongoDB'. Do this in ONE operation.
db.students.updateMany({}, {$set: {interests: ["coding", "brunch", "MongoDB"]}})

//Add some unique interests for each particular student into each of their interest arrays.
db.students.update({_id: ObjectId("60a42928e917fa91d631ce3e")}, {$push: {interests: "Flying"}})

//Add the interest 'taxes' into someone's interest array.
db.students.update({_id: ObjectId("60a42928e917fa91d631ce3e")}, {$push: {interests: "taxes"}})

//Remove the 'taxes' interest you just added.
db.students.update({_id: ObjectId("60a42928e917fa91d631ce3e")}, {$pop: {interests: 1}})

//Remove all students who are from California.
db.students.remove({home_state: "London"})

//Remove a student by name.
db.students.remove({name: "Richard Hartley"})

//Remove a student whose lucky number is greater than 5 (JUST ONE)
db.students.remove({lucky_number: {$gt: 5}})

//Add a field to each student collection called 'number_of_belts' and set it to 0.
db.students.updateMany({}, {$set: {number_of_belts: 0}})

//Increment this field by 1 for all students in Washington (Seattle Dojo).
db.students.updateMany({}, {$set: {number_of_belts: 1}})

//Rename the 'number_of_belts' field to 'belts_earned'
db.students.updateMany({}, {$rename: {'number_of_belts': 'belts_earned'}})

//Remove the 'lucky_number' field.
db.students.remove({lucky_number:1})

//Add a 'updated_on' field, and set the value as the current date.
