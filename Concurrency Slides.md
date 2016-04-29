
Using Asynchronous Methods in .NET
==================================

### Benefits of Asynchronous Programming
 
1. UI Responsiveness
2. Scalability (server-side)

### Styles of Asyncrony

* Manually create `Thread()`s, manually syncronize them.
* .NET 2.0 Threadpool: `ThreadPool.QueueUserWorkItem(...)`.
* `BackgroundWorker`
* .NET 4.0 Threadpool: `Task.Factory.StartNew(...)`.
* .NET 4.5 Task Parallel Library (TPL):  `async`, `await`, `Task.Run(...)`, and much more.


---
### Futures
A future (or _promise_) is a type that represents some operation that will complete in the future.  In modern .NET, these types are `Task` and `Task(Of TResult)`



---

As soon as you type `new Thread()`, it's over; your project already has legacy code.

---
## Task.Run Etiquette
0. `Foobar()` vs. `FoobarAsync()`
    * If `Foobar()` is CPU-bound then `await Task.Run(() => Foobar())`
    * If `Foobar()` is blocking I/O, then `FoobarAsync()` should   
1. Don't use `Task.Run()` for async i/o.  [Use it for CPU-bound tasks.](http://blog.stephencleary.com/2013/11/taskrun-etiquette-examples-using.html) 
2. Don't use `Task.Run()` in the implementation of a method to "make it" Async.  Use it to call a method that is "naturally" synchronous.  (see: http://blog.stephencleary.com/2013/11/taskrun-etiquette-examples-dont-use.html)
3. The complex case (doing both cpu-bound and i/o intense), make an Async Method, do the CPU bound stuff syncronously within it and the I/O stuff async within it: http://blog.stephencleary.com/2013/11/taskrun-etiquette-examples-even-in.html




