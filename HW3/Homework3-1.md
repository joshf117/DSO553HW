```
# Question a (1 stage in the pipeline)
db.orders.aggregate({$group:{_id:"$productName",sumQuantity:{$sum:"$quantity"}}})

# Question b (2 stages in the pipeline)
db.orders.aggregate([{$match:{status:"urgent"}},{$group:{_id:"$productName",sumQuantity:{$sum:"$quantity"}}}])

# Question c (1 stage in the pipeline)
db.orders.aggregate({$group:{_id:["$productName","$status"],sumQuantity:{$sum:"$quantity"}}})

# Question d (2 stages in the pipeline)
db.orders.aggregate([{$group:{_id:["$productName","$status"],sumQuantity:{$sum:"$quantity"}}},{$match:{sumQuantity:{$gte:15}}}])
```
