db.createCollection("Customer", {
   "validator": {
      $jsonSchema: {
         bsonType: "object",
         required: [ "customer_numb", "customer_first_name", "customer_last_name", "customer_street",
                    "customer_city", "customer_state", "customer_zip", "customer_phone", "order" ],
         properties: {
            customer_numb: {
               bsonType: "number",
               description: "must be a number and is required"
            },
            customer_first_name: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            customer_last_name: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            customer_street: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            customer_city: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            customer_state: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            customer_zip: {
               bsonType: "int",
               description: "must be an integer between [10000,99999] and is required"
            },
            customer_phone: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            order: {
               bsonType: "object",
               description: "orders information"
            }
         },
      }
   }
})

db.createCollection("Order", {
   "validator": {
      $jsonSchema: {
         bsonType: "object",
         required: [ "order_numb", "customer_numb", "order_date", "credit_card_numb",
                    "credit_card_exp_date", "order_complete", "pickup_or_ship" ],
         properties: {
            order_numb: {
               bsonType: "number",
               description: "must be a number and is required"
            },
            customer_numb: {
               bsonType: "number",
               description: "must be a number and is required"
            },
            order_date: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            credit_card_numb: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            credit_card_exp_date: {
               bsonType: "string",
               description: "must be a string and is required"
            },
            order_complete: {
               bsonType: "bool",
               description: "must be a boolean to indicate whether order is completed and is required"
            },
            pickup_or_ship: {
               bsonType: "string",
               description: "must be a string and is required"
            }
         },
      }
   }
})

db.Customer.insertMany([
    {
        "customer_numb": 0001,
        "customer_first_name": "Josh", 
        "customer_last_name": "Smith",
        "customer_street": "325 W Aams Blvd",
        "customer_city": "Los Angeles",
        "customer_state": "California",
        "customer_zip": 90008,
        "customer_phone": "213-001-0001",
        "order":{}
        
    },
    {
        "customer_numb": 0002,
        "customer_first_name": "Mary", 
        "customer_last_name": "Jones",
        "customer_street": "245 Ralph Ave",
        "customer_city": "New York",
        "customer_state": "New York",
        "customer_zip": 11233,
        "customer_phone": "213-002-0002",
        "order":{}
        
    }
])

db.Order.insertMany([
    {
        "order_numb": 1000001,
        "customer_numb": 0001, 
        "order_date": "2022-01-01", 
        "credit_card_numb": "0000-0000-0000-0001",
        "credit_card_exp_date": "2022-12-31",
        "order_complete": true,
        "pickup_or_ship": "pickup"
        
    },
    {
        "order_numb": 1000002,
        "customer_numb": 0001, 
        "order_date": "2022-01-02", 
        "credit_card_numb": "0000-0000-0000-0001",
        "credit_card_exp_date": "2022-12-31",
        "order_complete": false,
        "pickup_or_ship": "pickup"
        
    },
    {
        "order_numb": 1000003,
        "customer_numb": 0001, 
        "order_date": "2022-01-01", 
        "credit_card_numb": "0000-0000-0000-0001",
        "credit_card_exp_date": "2022-12-31",
        "order_complete": true,
        "pickup_or_ship": "ship"
        
    },
    {
        "order_numb": 1000004,
        "customer_numb": 0002, 
        "order_date": "2022-01-01", 
        "credit_card_numb": "0000-0000-0000-0002",
        "credit_card_exp_date": "2022-12-31",
        "order_complete": false,
        "pickup_or_ship": "pickup"
        
    },
    {
        "order_numb": 1000005,
        "customer_numb": 0002, 
        "order_date": "2022-01-01", 
        "credit_card_numb": "0000-0000-0000-0002",
        "credit_card_exp_date": "2022-12-31",
        "order_complete": true,
        "pickup_or_ship": "ship"
        
    },
    {
        "order_numb": 1000006,
        "customer_numb": 0002, 
        "order_date": "2022-01-01", 
        "credit_card_numb": "0000-0000-0000-0002",
        "credit_card_exp_date": "2022-12-31",
        "order_complete": true,
        "pickup_or_ship": "pickup"  
    }
])

db.Customer.aggregate( [
   {
     $lookup:
       {
         from: "Order",
         localField: "customer_numb",
         foreignField: "customer_numb",
         as: "order"
       }
  }
] )
