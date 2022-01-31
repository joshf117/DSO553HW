```
# Question a  - 1 stage in the pipeline
db.orders.aggregate({$group:{_id:"$productName",sumQuantity:{$sum:"$quantity"}}})
 # output
 [{ _id: 'Iron rod', sumQuantity: 75 },
  { _id: 'Steel beam', sumQuantity: 60 }]

# Question b - 2 stages in the pipeline
db.orders.aggregate([{$match:{status:"urgent"}},{$group:{_id:"$productName",sumQuantity:{$sum:"$quantity"}}}])
 # output
 [{ _id: 'Iron rod', sumQuantity: 60 },
  { _id: 'Steel beam', sumQuantity: 50 }]

# Question c - 1 stage in the pipeline
db.orders.aggregate({$group:{_id:["$productName","$status"],sumQuantity:{$sum:"$quantity"}}})
 # output
 [{ _id: [ 'Iron rod', 'new' ], sumQuantity: 15 },
  { _id: [ 'Iron rod', 'urgent' ], sumQuantity: 60 },
  { _id: [ 'Steel beam', 'new' ], sumQuantity: 10 },
  { _id: [ 'Steel beam', 'urgent' ], sumQuantity: 50 }]

# Question d - 2 stages in the pipeline
db.orders.aggregate([{$group:{_id:["$productName","$status"],sumQuantity:{$sum:"$quantity"}}},{$match:{sumQuantity:{$gte:15}}}])
 # output
 [{ _id: [ 'Iron rod', 'urgent' ], sumQuantity: 60 },
{ _id: [ 'Iron rod', 'new' ], sumQuantity: 15 },
{ _id: [ 'Steel beam', 'urgent' ], sumQuantity: 50 }]
```
