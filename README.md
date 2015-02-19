##TIL##
A random list of things that I learned during programming

###MongoDB

**To search in array of Objects/Documents using field/value inside the array:**

`db.tenders.find({partsList: {$elemMatch: {partNum:'45046-67245'}}})`

**To find documents with partial match:**

`db.tenders.find({tenderNum: {$regex : 'query'}})`

###Web

**live update an HTML form using javascript**
```javascript
document.getElementById("field1").onkeyup = function() {
    document.getElementById("field2").value = this.value;   
}
```

###Multithreaded vs Asynchronous Notes

**Multithreaded**

* Benefits on CPU-bound operations
* Recent Mac's have a hard limit of 2000 spawnable threads.
* With 4 cores, only 4 threads can be executing instructions at any given time.
* It takes time to create new threads and it takes resources during context switching/thread memory overhead.
* Ideal number of threads can only be found by testing.
* Apache is multithreaded and it creates new threads per request until it a the defined limit. It is said to be bad because it consumes resources even when the threads are idle and waiting  for I/O operations.
* Common Issues include: Starvation, deadlock, etc. (Basically screwing up with shared resources)

**Asynchronous**

* Benefits on I/O-bound operations
* In Node.js, there's a single thread but it is event-based. All I/O is evented and asynchronous.
* At an I/O call, the event loop saves the callback function in a callback queue and the main thread continues other operations in the system. When the I/O operation is complete, the I/O operation can fire a interrupt like hardware interrupts to signal that. Then, the event loop puts that function back on the call stack so that that main thread can run the rest of the function with the received data.
* Easy to learn, hard to screw up.
