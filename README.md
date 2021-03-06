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

### Access Android app data without root
http://blog.shvetsov.com/2013/02/access-android-app-data-without-root.html

###Javascript

**Closures**

```javascript
(function(){
   //do something...
})();
```

* Use this for immediately-invoked function expression (IIFE)
* Do __NOT__ use them with anonymous functions because stack traces have a hard time finding the function name. e.g.

```javascript
//bad
var foo = (function(){
  //do something...
})();
```

**Function Declarations vs. Function Expressions Notes**

* Prefer Named Function Expression
```javascript
var foo = function foo() {
	//do stuff
}
```
* Otherwise, use anonymous functions
```javascript
var foo = function() {
	//do stuff
}
```
Caveat: Hard to debug because stack traces can't always print the function name.

* Avoid function declarations because of hoisting e.g.
```javascript
function foo() {
	//do stuff
}
```

This is bad because the following returns 8 instead of 3.

```javascript
//bad
function foo(){
    function bar() {
        return 3;
    }
    return bar();
    function bar() {
        return 8;
    }
}
alert(foo());
```

Above code actually runs as:

```javascript
function foo(){
    //define bar once
    function bar() {
        return 3;
    }
    //redefine it
    function bar() {
        return 8;
    }
    //return its invocation
    return bar(); //8
}
alert(foo());
```

###Array Initization###

**Java**

```Java
int[] arr = new int[10]; //defaults to 0

int[] arr = {1, 2, 3};
```

**Python**

List(like Array, can contain mixed data types)

```Python
list = ["Sarah",29,30000.00]
```

Tuple(Data is immutable)

```Python
days = ("Sunday", "Monday", "Tuesday")
```

Set(Like Mathematical sets, cannot contain duplicates)

```Python
set = { 2, 3, 5}
```


**C**

```C
   int arr[10]= {0}; //Initializes to 0
   int arr[] = {1, 2, 3};
```

**JavaScript**

```JavaScript
var cars = ["Saab", "Volvo", "BMW"]; 
```

###Swapping variables without using a temp###

```C
  int a = 3, b = 5;
 
 //Swap V1
  a = a + b;  // a now becomes 8
  b = a - b;  // b becomes 3
  a = a - b;  // a becomes 5
  
  //Swap V2
  a = a ^ b;
  b = a ^ b;
  a = a ^ b;
  ```
