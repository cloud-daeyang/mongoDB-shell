# Installing MongoDB Shell for Amazon Linux 2023
---
## Install the required prerequisite
```
cat <<EOF >> /etc/yum.repos.d/mongodb-org-7.0.repo
[mongodb-org-7.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2023/mongodb-org/7.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://pgp.mongodb.com/server-7.0.asc
EOF
sudo yum install -y mongodb-org
sudo systemctl enable --now mongod
```

## MongoDB Shell command
```
mongosh
```

## Connection 확인
```
mongo --ssl --host <documentDB URI> --ssl --username <documentDB username> --password <documentDB password>
```

## MongoDB Practice
```
// Create a “Hello World” Database and Document
use helloWordDB
db.greeting.insert({message: "Hello, World!"})

// Retrieve the Document
db.greeting.find()
{message: "Hello, World!"}
```

## Advance Practice
```
// Create an index on an array field
db.col1.save({'colors': ['red','blue']})
db.col1.ensureIndex({'colors': 1})
// Finding
db.col1.find({'colors': 'red'})
> { "_id" : ObjectId("4ccc78f97cf9bdc2a2e54ee9"), "colors" : [ "red", "blue" ]}
db.col1.find({'colors': 'blue'})
> { "_id" : ObjectId("4ccc78f97cf9bdc2a2e54ee9"), "colors" : [ "red", "blue" ]}

// How to query MongoDB with %like%?
// Problem:
select *
from users
where name like '%m%'
// Answer
db.users.find({name: /a/}) // like %a%
db.users.find({name: /^pa/}) // like pa%
db.users.find({name: /ro$/}) // like %ro
// or using Mongoose:
db.users.find({ 'name': {'$regex': 'sometext'}})
```
