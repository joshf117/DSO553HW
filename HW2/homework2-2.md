```
db.student.drop()

db.createCollection("student", {  
  "validator": {  
      $jsonSchema: {  
         bsonType: "object",  
         required: [ "name", "phone", "address"],  
         properties: {  
            name: {  
               bsonType: "string",  
               description: "must be a string and is required"  
            },  
            phone: {  
               bsonType: "string",  
               description: "must be a string and is required"  
            },  
            address: {
               bsonType: "object",
               required: [ "city", "state", "zip_code" ],
               properties: {
                  city: {
                     bsonType: "string",
                     description: "must be a string and is required"
                  },
                  state: {
                     bsonType: "string",
                     description: "must be a string and is required"
                  },
                  zip_code: {
                     bsonType: "number",
                     description: "must be a number between [10000,99999] and is required"
                  },
                  street_name_number: {
                     bsonType: "string",
                     description: "must be a string if the field exists"
                  }
               }
            }
         }
      },
   }
})

db.student.insertMany([
    {
        "name": "Josh Smith",
        "phone": "213-001-0001", 
        "address": {
            "city": "Los Angeles",
            "state": "California",
            "zip_code": 90007,
            "street_name_number": "325 W Adams Blvd"
            }
        
    },
    {
        "name": "David Jones",
        "phone": "213-245-6789", 
        "address": {
            "city": "Los Angeles",
            "state": "California",
            "zip_code": 90007,
            "street_name_number": "325 W Adams Blvd"
            }
        
    },{
        "name": "Peter Wang",
        "phone": "213-056-8127", 
        "address": {
            "city": "Los Angeles",
            "state": "California",
            "zip_code": 90014,
            "street_name_number": "802 Broadway S"
            }
        
    },{
        "name": "Nick Roger",
        "phone": "213-785-4513", 
        "address": {
            "city": "Los Angeles",
            "state": "California",
            "zip_code": 90014,
            "street_name_number": "802 Broadway S"
            }
        
    },{
        "name": "Faye May",
        "phone": "213-560-9716", 
        "address": {
            "city": "Los Angeles",
            "state": "California",
            "zip_code": 90021,
            "street_name_number": "2276 E 16th Street"
            }
        
    },{
        "name": "James Cotten",
        "phone": "213-435-0817", 
        "address": {
            "city": "Los Angeles",
            "state": "California",
            "zip_code": 90021
            }
        
    },{
        "name": "Qiwen Yang",
        "phone": "213-098-5615", 
        "address": {
            "city": "Los Angeles",
            "state": "California",
            "zip_code": 90017
            }
        
    },{
        "name": "Chandler Robin",
        "phone": "213-032-9011", 
        "address": {
            "city": "Los Angeles",
            "state": "California",
            "zip_code": 90013,
            "street_name_number": "361 S Spring St"
            }
        
    },{
        "name": "David Ben",
        "phone": "213-032-9011", 
        "address": {
            "city": "Los Angeles",
            "state": "California",
            "zip_code": 90013,
            "street_name_number": "361 S Spring St"
            }
        
    },{
        "name": "Stephan Brown",
        "phone": "213-191-2379", 
        "address": {
            "city": "Los Angeles",
            "state": "California",
            "zip_code": 90007
            }
        
    }
])

db.student.createIndex( { "phone": 1, "address.zip_code": 1 } )

db.student.find({"phone": "213-245-6789"},{"name": 1})

db.student.find({"phone": "213-245-6789"}).explain("executionStats")
db.student.find({"phone": "213-245-6789"},{"name": 1}).explain("executionStats")
```

