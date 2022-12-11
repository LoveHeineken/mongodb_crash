# How To Set Up Mongo
> https://www.mongodb.com/docs/manual/administration/install-community/
> click Install on macOS
> xcode-select --install
> click Install brew using the official Homebrew installation instructions.
> brew tap mongodb/brew
> brew update
> brew install mongodb-community@6.0
> https://www.mongodb.com/docs/mongodb-shell/install/#std-label-mdb-shell-install
> brew install mongosh
> mongosh

# Command Samples
> show dbs
> use appdb
> show collections
> db.dropDatabase()
> exit

# Get
> db.users.find()

# Create
> db.users.insertOne({name: "Hoge"})
> db.users.insertMany([{name: "Foo"}, {name: "Bar"}])
> db.users.find().limit(1)
> db.users.find().sort({name: 1}).limit(10)
> db.users.find().sort({name: -1}).limit(10)
> db.users.find().skip(1).limit(1)
> db.users.find({name: "Foo"}, {name: 1, age: 1})
> db.users.find({name: "Foo"}, {name: 1, age: 0})
> db.users.find({name: { $eq: "Foo"}}) # equal to
> db.users.find({name: { $ne: "Foo"}}) # not equal to
> db.users.find({age: { $gt: 13 }}) # greater than 
> db.users.find({age: { $gte: 13 }}) # greater than equal to
> db.users.find({age: { $lt: 13 }}) # less than
> db.users.find({age: { $lte: 13 }}) # less than
> db.users.find({name: { $in: ["FooBar", "Foo"] }}) # within
> db.users.find({name: { $nin: ["FooBar", "Foo"] }}) # except
> db.users.find({age: { $exists: true }})
> db.users.find({age: { $gte: 20, $lte: 40 }, name: "Foo"})
> db.users.find({ $and: [{ age: 26}, { name: "Foo" }] })
> db.users.find({ $or: [{ age: {$lte: 26}}, { name: "Foo" }] })	
> db.users.find({ age: { $not: {$lte: 20 } } })
> db.users.insertMany([{name: "One", balance: 100, debt: 100},{name: "Two", balance: 200, debt: 200},{name: "Three", balance: 300, debt: 300}])
> db.users.find($expr: { $gt: ["$debt", "$balance"]}}) # expression. debt is greater than balance
> db.users.find({"address.street": "123 Main St"}) # find 「address.street: '123 Main st'」
> db.users.countDocuments({ age: { $lte: 40}})

# Update
> db.users.updateOne({age:26},{ $set: {age:27}})
> db.users.updateOne({_id:ObjectId("000")},{ $inc: {age:3}})
> db.users.updateOne({_id:ObjectId("000")},{ $rename: {name:"firstName"}})
> db.users.updateOne({_id:ObjectId("000")},{ $unset: {age:""}})
> db.users.updateOne({_id:ObjectId("000")},{ $push: {hobbies:"Swimming"}}) # add new key
> db.users.updateOne({_id:ObjectId("000")},{ $pull: {hobbies:"Swimming"}}) # remove key
> db.users.updateMany({ address:{ $exists: true } }, { $unset: {address: ""}}) # remove address key value from all
> db.users.replaceOne({ age: 30}, {name: "Hoge"}) # rename whose age is 30

# Delete
> db.users.deleteOne({name: "Hoge"})
> db.users.deleteMany({age: {$exists: false}}) # delete all who does not have age key
