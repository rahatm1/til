##TIL##
A random list of things that I learned during programming

###MongoDB

**To search in array of Objects/Documents using field/value inside the array:**

`db.tenders.find({partsList: {$elemMatch: {partNum:'45046-67245'}}})`

**To find documents with partial match:**

`db.tenders.find({tenderNum: {$regex : 'query'}})`
