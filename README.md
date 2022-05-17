# Interview-Questions

## What is EventLoop? Explain in brief?
We know javascript is a synchronous and single-threaded language which means javascript executes one statement at a time and sequentially. But in the current scenario, we want more dynamic content on our website this content to fetch from a server so this process takes time to do that so these functions need to be asynchronous, otherwise, the entire browser would remain frozen during the waiting, which would result in a poor user experience. That is why javascript provides an asynchronous Enviroment in these environments both synchronous and asynchronous code run parallel This happens because the JavaScript host environment, in this case, the browser, uses a concept called the event loop to handle concurrency or parallel events. Since JavaScript can only execute one statement at a time, it needs the event loop to be informed of when to execute which specific statement. The event loop handles this with the concepts of a stack and a queue.
Let's understand the flow of execution. first all code comes in stack and execution in a LIFO manner and any asynchronous code show so this code pass on to the web API and executed outside of the call stack and this code is ready to execute so the web API passes these code in the queue.and In the call stack all synchronous code are executed after event loop continus check any code is available in queue so this code enter in call stack and finish the execution.  
 
## Flexbox vs Grid system
### Grid
CSS Grid Layout, is a two-dimensional grid-based layout system with rows and columns, making it easier to design web pages without having to use floats and positioning. Like tables, grid layout allow us to align elements into columns and rows.

### Flexbox
The CSS Flexbox offers a one-dimensional layout. It is helpful in allocating and aligning the space among items in a container (made of grids). It works with all kinds of display devices and screen sizes.

Grid is made for two-dimensional layout while Flexbox is for one. This means Flexbox can work on either row or columns at a time, but Grids can work on both.
Flexbox, gives you more flexibility while working on either element (row or column). HTML markup and CSS will be easy to manage in this type of scenario.
GRID gives you more flexibility to move around the blocks irrespective of your HTML markup.

## Event Loop and Async javascript
### Event loop
An event loop is something that pulls stuff out of the queue and places it onto the function execution stack whenever the function stack becomes empty.
### Async Javascript
In the early days of the internet, websites often consisted of static data in an HTML page. But now that web applications have become more interactive and dynamic, it has become increasingly necessary to do intensive operations like make external network requests to retrieve API data. To handle these operations in JavaScript, a developer must use asynchronous programming techniques.

Since JavaScript is a single-threaded programming language with a synchronous execution model that proccesses one operation after another, it can only process one statement at a time. However, an action like requesting data from an API can take an indeterminate amount of time, depending on the size of data being requested, the speed of the network connection, and other factors. If API calls were performed in a synchronous manner, the browser would not be able to handle any user input, like scrolling or clicking a button, until that operation completes. This is known as blocking.

In order to prevent blocking behavior, the browser environment has many Web APIs that JavaScript can access that are asynchronous, meaning they can run in parallel with other operations instead of sequentially. This is useful because it allows the user to continue using the browser normally while the asynchronous operations are being processed.

As a JavaScript developer, you need to know how to work with asynchronous Web APIs and handle the response or error of those operations. In this article, you will learn about the event loop, the original way of dealing with asynchronous behavior through callbacks, the updated ECMAScript 2015 addition of promises, and the modern practice of using async/await.


## callback promises/ async await, what is Promise.all?

### Callback function 
what is a callback function why we are use callback function  
Let’s understand with one example

```ruby
function first(){
console.log(1)
}

function second(){
setTimeout(()=>{
console.log(2)
},1000)
}

function third(){
console.log(3)
}

first()
second()
third()
```
this code output is we now `1 3 2`

but we want to `1 2 3` how to do that 
The original solution to dealing with this problem is using callback functions. Callback functions do not have special syntax; they are just a function that has been passed as an argument to another function. The function that takes another function as an argument is called a higher-order function. According to this definition, any function can become a callback function if it is passed as an argument. Callbacks are not asynchronous by nature, but can be used for asynchronous purposes.

```ruby

function first(){
console.log(1)
}

function second(third){
setTimeout(()=>{
console.log(2);
third();
},1000)
}

function third(){
console.log(3)
}

first()
second(third)
```
### Promises
A promise represents the completion of an asynchronous function. It is an object that might return a value in the future.
Creating a Promise
You can initialize a promise with the new Promise syntax, and you must initialize it with a function. The function that gets passed to a promise has resolve and reject parameters. The resolve and reject functions handle the success and failure of an operation, respectively.
```ruby
const promise = new Promise((resolve, reject) => {})
```
#### State of Promises
- Pending - Initial state before being resolved or rejected
- Fulfilled - Successful operation, promise has resolved
- Rejected - Failed operation, promise has rejected

So far, nothing has been set up for the promise, so it's going to sit there in a pending state forever. The first thing you can do to test out a promise is fulfill the promise by resolving it with a value

```ruby 
const promise = new Promise((resolve, reject) => {
  resolve('We did it!')
})
```

So far, the example you created did not involve an asynchronous Web API—it only explained how to create, resolve, and consume a native JavaScript promise. Using setTimeout, you can test out an asynchronous request.

```ruby
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve('Resolving an asynchronous request!'), 2000)
})

// Log the result
promise.then((response) => {
  console.log(response)
})
```
