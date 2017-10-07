# Virtual Stacks & Promises
Untangling async code

Consider Express middleware. Express allows you to specify a chain of middleware - a number of functions that are called, in order before the final request handler is called. Any middleware might decide that an error occurred, at which point it calls `next()` with an error, skips all the other middleware, and jumps to the nearest error-handling middleware.  To be able to call functions in the order in which they are added, Express needs functionality similar to the JS stack (when a function is called, an item is added on top of the stack; and when a value is returned, an item is popped off the top of the stack), but because Express was designed to allow middlewares to handle async operations, we are not able to use the JS stack directly.

To solve this issue Express implements a 'virtual stack' that works like the JS stack, but it doesn't directly use the JS stack.  

The virtual stack provides the same mechanics as the JS stack:
- Nesting of operations: middleware like routers in Express, nested function calls in the JS stack
- Sequential operation: consecutive middlewares for Express, consecutive lines of code in the JS stack
- Interruption of the normal execution path, followed by 'stack unwinding' and searching for the nearest error handler: error-handling middleware (handles the error) and next(err) (which interrupts the normal execution path) in Express, a catch block (specifically the part that handles the error) and the throw (which is what interrupts the normal excecution path) in the JS stack.

## Promises and how they relate to the stack:
The fact that we cannot return any values from an async operation is impractical. It means that we can't do stuff like `asyncThing(otherAsyncThing(), anotherAsyncThing())`. It essentially breaks down most of the features in the language because we will never have access to the results at the time we need them, whenever an async anything is involved. Promises exist as a solution to this problem.

A Promise is synchronously created, before the async operation even starts. In most scenarios, in order to produce a useful Promise, the async operation is passed a callback that is specifically designed to tie into the Promise - that callback, upon completion, calls a resolve/reject function, which itself sets values and then calls some hooks on the Promise object; like the registered .then handlers - and finally, from the function that both created the Promise and initiated the async operation with that special callback, the Promise is immediately, synchronously returned, in the same tick.

The return value doesn't exists in the same stack but it provides a placeholder object that later on can be exchanged for the value (through the `.then` handlers - this handlers also get the async result passed into it).

**So whenever you return anything with Promises, we are always returning other Promises.**

Promises build a 'virtual stack' and async callbacks are used to wire up all the behaviour. We are able to get the Promise synchronously but the result that that Promise represents was obtained asynchronously.

This the main reason that promises exist. It's a way to 'regain' language constructs that would work with sync code but in a way that you can also use them with async code. Essentially a way to untangle async code.
