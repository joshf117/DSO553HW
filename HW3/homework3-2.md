```
# Question a
db.grades.distinct("class_id").length
# Using query above, we can know that there are 501 different classes.

# Question b
db.grades.distinct("student_id").length
# Using query above, we can know that there are 10000 students.

# Question c
db.grades.aggregate([
   {
      "$unwind":"$scores"
   },
   {
      "$match":{
         "class_id":212
      }
   },
   {
      "$group":{
         "_id":{
            "class_id":"$class_id",
            "name":"$scores.type"
         },
         "value":{
            "$avg":"$scores.score"
         }
      }
   }
])
# output
[
  {
    _id: { class_id: 212, name: 'homework' },
    value: 51.28406633092742
  },
  { _id: { class_id: 212, name: 'exam' }, value: 49.32031796981391 },
  { _id: { class_id: 212, name: 'quiz' }, value: 51.52482268546838 }
]
# Using query above, we can know that the average exam score for class 212 is 49.32.

# Question d
db.grades.aggregate([
   {
      "$unwind":"$scores"
   },
   {
      "$match":{
         "class_id":212
      }
   },
   {
      "$group":{
         "_id":{
            "class_id":"$class_id",
            "name":"$scores.type"
         },
         "value":{
            "$stdDevSamp":"$scores.score"
         }
      }
   }
])
# output
[
  { _id: { class_id: 212, name: 'exam' }, value: 29.34583940313283 },
  { _id: { class_id: 212, name: 'quiz' }, value: 29.803845325101385 },
  {
    _id: { class_id: 212, name: 'homework' },
    value: 29.791026803560154
  }
]
# Using query above, we can know that the standard deviation of the exam score is 29.35.
