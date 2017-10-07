# The Stack
Why code executes synchronously

A stack is an ordered colletion of items.
In programing, the stack is used to track the execution of an application. When a function is called, an item is added on top of the stack; and when a value is returned, an item is popped off the top of the stack.

![](http://i.imgur.com/0yoklCem.png)

A stack frame is the collection of all data on the stack associated with one function. After an item is popped off the top of the stack, execution of the application is returned to the previous stack frame (the one below it) with access to the return value. For example:

```javascript
function a() {
  console.log("foo");
};

function b() {
console.log("here is bar!")
};

function c() {
  console.log("baz");
};

a();
b();
c();

// > foo
// > here is bar!
// > baz

 ```

And this is the behaviour if we were to schedule an async callback in one of those sync functions. Note how the callback is scheduled but not excecuted immediately:

 ```javascript
 function a() {
  console.log("foo");
};

function b(cb){
  setTimeout(cb, 1)
};

function c() {
  console.log("baz");
};

a();
b(()=>console.log("skip"));
c();

// > foo
// > Code in b gets executed - not the async callback that b scheduled (console.log("skip")),
//   only the code that b itself contains (ie. synchronous code).
// > baz
// > skip

 ```

The execution order:
```
--- tick 0 ---
1) function a
2) console.log in function a
3) function b
4) setTimeout in function b
5) function c
6) console.log in function c

--- tick 1 ---
7) cb that was setTimeout'd in function b
8) console.log in that cb
```
(it might also be tick 45213 instead of tick 1, depending on how many ticks occur before the 1ms is over, but the important part is that it's not tick 0). This is why **code executes synchronously when you call a function even if it doesn't contain a return statement**.

#### How does the timeout work? and where in the stack is the callback?  
Because the callback in b is executed in another stack, there's nothing to return the value to right away. The callback is executed 'detached' from the stack in which it was defined. Its important to remember that **any value returned from an async callback (that was invoked directly from the event loop) is lost irrevocably**.

### Rules of The Stack
- A 'return' means you pop an item off the top of the stack (and pass the return value to the previous item on the stack, returning execution control to it)
- An async callback, executed from the event queue, gets executed with an empty stack to start with
- A callback must unwind the entire stack before the next callback in the queue is executed
