# Promises
What are promises

A promise is an object that represents an async operation (process) that's still in progress.  The purpose of Promises is to make it easier to write sequential code.
```javascript
Promise.try(() => {
  return taskOne();
}).then((result) => {
  return taskTwo();
}).then((result) => {
  return taskThree();
});
```
In the above snippet, even though there are technically 6 promises involved, only three implement real functionality:
* Promise.try(...)  -> Tracks the result of taskOne below
* taskOne           -> **Implements real functionality**
* .then(...)        -> Propagate the `result`
* taskTwo           -> **Implements real functionality**
* .then(...)        -> Propagate the `result`
* taskThree         -> **Implements real functionality**

The order of execution:
```
--- tick 0 ---
 Promise.try called
 taskOne called
 a Promise is returned from taskOne
 return that Promise from the Promise.try callback, Promise.try will now track it
 first .then called (note, .then itself, *not* the callback) with a callback as argument
 second .then called, with a callback as argument
 --- tick 10 ---
 taskOne Promise resolves
 Promise.try Promise resolves
 first .then callback called
 taskTwo called
 a Promise is returned from taskTwo
 return that Promise from the first .then callback, the first .then will now track it
 --- tick 20 ---
 taskTwo Promise resolves
 first .then Promise resolves
 second .then callback called
 taskThree called
 a Promise is returned from taskThree
 return that Promise from the second .then callback, the second .then will now track it
 --- tick 30 ---
 taskThree Promise resolves
 second .then Promise resolves
 --- the end ---
```

### What's the difference with callbacks?
The main difference between Promises and callbacks is that a Promise is a placeholder object you get access to immediately that represents the in-progress operation; in a callback you have to immediately specify the next behaviour.

Nested callbacks also allow for writing sequential async code, but are more difficult to use right.
Similar functionality of the above snippet as a series of nested callbacks:
```javascript
taskOne((err, result) => {
  taskTwo((err, result) => {
    taskThree((err, result) => {
      // ...
    });
  });
});
```
With error-first callbacks you have to **immediately** specify the next code to run when a task completes. This is not true for Promises. With Promises you are able to attach behaviour at any time including after the Promise has already resolved. This allows for a lot of improvements:

- Compose things easier - `Promise.all([promise1, promise2])` will produce a combined Promise that resolves when `promise1` and `promise2` both resolve. `Promise.all` wires up things internally, which it can do because it can specify behaviour at any time on `promise1` and `promise2`, including its own behaviour.
- Propagate errors automatically - Because behaviour can be attached at any time, you can return a Promise from another Promise's `.then` callback, and then that other Promise can wire up error propagation automatically.
- The returned value isn't the actual result, but it can be returned and passed around just as easily.
