# Asynchronous Code

Welcome to the ninth lesson! In this lesson, you learn about asynchronous code. You can use asynchronous code to perform time-consuming tasks without slowing down your application.

The browser reads your source code files from top to bottom. It reads each line one by one. The browser doesn't move to the next line until the current line it's reading is done executing. This is known as **synchronous** behaviour. This, however, can slow down your application if the line of code takes extra time to execute. You may not want to hold up the flow of your application while it waits for the time-consuming task to complete.  

To overcoem this, you can use asynchronous blocks of code tell the browser that the code inside will take extra time to execute and to move on to the next block of code. The browser responds by moving onto the next block of code while the time-consuming task executes in the background. When the time-consuming code is finally done, it tells the browser and provides the browser with the result of the task. Then, the browser incorporates the result into your application.  

In this lesson, you first will get an introduction to asynchronous code. Oftentimes when using asynchronous code, you are using it to retrieve information from third-parties. So, in this lesson, you also will learn about third-party APIs. 

Next, you will learn about some of the core concepts and tools from writing asynchronous blocks of code for fetching information from third parties. Specifically, you will learn about the `fetch` function, Promises, and Objects. You will see examples and learn how to incorporate them into your code.

At the end of this lesson, you see a live coding example. The live coding session reinforces what you learn in the lesson. This lesson also helps prepare you for making your personal portfolio site. The code from this session is included in this repository. You can use it however you like, but as with any code you get from someone else, make sure you understand it well enough to explain it to someone before putting it in your own projects.  

In this lesson, you learn:  

- Hour 1: [Intro to Asynchronous Code and Third-Party APIs](#intro-to-asynchronous-code-and-third-party-apis)      
- Hour 2: [Fetch Promises and Objects](#fetch-promises-and-objects)   
- Hour 3: [Live Coding](#live-coding)   

The topics below outline what you learn in the live session. After the live session, you can use this material as a resource for guided self-learning. This document will serve you as a roadmap for gaining repetition with the material that you learned during the live session.   

## [Intro to Asynchronous Code and Third-Party APIs](#intro-to-asynchronous-code-and-third-party-apis)      

### Intro to Asyncrhonous Code  
- Asynchronous blocks of code allow the browser to run time-consuming tasks without waiting for the result before the browser reads subsequent lines of code  
- By default, browsers read code files from top to bottom and wait to continue reading until the current line is done executing  
- Blocks of code that prevent an application from continuing are called [blocking code](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts#blocking_code)  
  -- Examples of blocking code are `for` loops that iterate through huge arrays, [the `setTimeout` function](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Timeouts_and_intervals), and `fetch` requests  
  -- These tasks take time to complete, enough time that they prevent your application from doing other things until these tasks are done executing  
- To create [an asynchronous block of code](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing#asynchronous_javascript), you can use JavaScript's a built-in `Promise` object, use a built-in method that returns a `Promise`, like the `fetch` function, or use [callback functions](https://www.w3schools.com/js/js_callback.asp)  
- Using `Promise` is the more modern approach compared to callback functions; this lesson focuses on using `Promise` objects for asynchronous behavior
  -- A callback function is a function that is passed as an argument to another function  
  -- The function that receives the callback function calls that callback function when the receiving function has completed its task  
  -- Callback functions are an important concept to know but not the focus in this lesson; spend time [reading about them](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing#async_callbacks) on your own    
- A [`Promise` is a placeholder](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) for a value that does not yet exist in your project  
- A `Promise` can be in one of three states: pending, rejected, and fulfilled  
- While a pending, the code inside the promise is executing  
- When the code is done, the `Promise` is either fulfilled and contains a value or is rejected and contains an error message  
- To access the information returned by the promise, you have to **handle** the promise  
- The `async / await` method is the modern way to handle promises; another important way to know is using the `.then` method  

### Third-Party APIs

- An Application Programming Interface (API) is third-party software that you can access through the internet using HTTP   
- You can send a request from your browser to a URL for an API, and receive a response containing data from the third-party API  
- The third-party API will have documentation that instructs you how to access and consume the API, and that's where you can find the URL  
-- For instance, Github has an API that you can use to access your Github information, including your name, profile, repository information, and more  
-- Many other companies and services have APIs, like Facebook, Spotify, Google, Amazon, Twitter and more  
-- Here is one for [dog photos](https://dog.ceo/dog-api/)  
-- Punch [this into your browser](https://dog.ceo/api/breeds/image/random) to see what the API returns to you  
- You should write asynchronous blocks of code for communications between your browser and third-party APIs because the time it takes to send a request and receive a response is much longer than it takes for your browser to execute other lines of code  
-- Although fetching information can take a long time relative to other lines of code, to you it'll happen usually very fast; sometimes so fast that you can't perceive a delay  
- When sending a request from a browser, you can send an HTTP GET request, POST requst, or other type of HTTP request; those two are your focus for now  
- A GET request asks the third party for specific information, like a list of all songs, all users who liked a photo, or the text from a Google Doc  
- A POST request is used for submitting information to the third party, like a form containing signup information, a file, or some other type of data  
- After processing your request, the API will send a response to your browser  
- A response to a GET request, if successful, will contain the requested information; otherwise, the response returns an error message  
- A response to a POST request usually contains a message saying whether the submission was successful  
- [Response codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) can be used to signal to the browser the results of the requst 
  -- Examples of response codes: 200 means success, 400 means some sort of error with the request, and 500 means internal server error  
- The moden way to send requests in JavaScript is using the `fetch` function  
- Using fetch, you can send an HTTP request from your browser to a third-party and receive a response inside of the `fetch` function, 
- To access the HTTP response data, you have to handle the `Promise` returned by the `fetch` function (see below for more on how to do this)

## [Fetch Promises and Objects](#fetch-promises-and-objects)    

### Fetch  

- When writing asynchronous code that sends HTTP requests to third-party APIs, you can use the [built-in JavaScript function called `fetch`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)  
- Calling the `fetch` function looks like this, where `URL` is the address for the third-party API:  

```javascript
const URL = "https://dog.ceo/api/breeds/image/random"

fetch(URL)
```
- The `fetch` function takes one argument, which is the address of the API  
- The function returns a `Promise`  
- To handle the `Promise`, you can use the [`.then()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)  

```javascript
const URL = "https://dog.ceo/api/breeds/image/random"
fetch(URL)
  .then(response => response.json())
  .then(data => console.log(data));
```
- The example above uses the `.then()` method to access the HTTP response object returned by a fulfileed `Promise`  
- The `.then()` method accepts a function as an argument  
- The HTTP response contains the data in JSON format that your browser requestsed  
- To access the JSON data, use the [`json()` method](https://developer.mozilla.org/en-US/docs/Web/API/Body/json)  
- The `.json()` method reads the response message inside the HTTP response and returns a `Promise` containing it  
- To access the JSON data in that fulfilled `Promise`, the example uses the `.then()` method again, which also returns a `Promise` that resolves to a JavaScript object  
- In the example, the varaible `data` represents that JavaScript object, and inside the function body of the argument second `.then()` method, you can access that data and do with it what you want; the example just console logs the result  
- The code below is inspired by [MDN's Intro to Asynchronous Code](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing#the_nature_of_asynchronous_code) and contains console logs that show the timing of the events of a `fetch` function  

```javascript
console.log ('Starting');
const URL = "https://dog.ceo/api/breeds/image/random"

fetch(URL).then((response) => {
  console.log('Got the HTTP response)')
  return response.json();
}).then((data) => {
  console.log ('Got the data: ', data);
}).catch((error) => {
  console.log('There has been a problem with your fetch operation: ' + error.message);
});

console.log ('All done!');
```

### Promise

- The `fetch` function is just one example of a function that returns a `Promise`  
- You can write your own functions that return a `Promise` by using [the `Promise` object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)  

- Here is a good basic example of a [`Promise` from MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise#basic_example) 

```javascript
let myFirstPromise = new Promise((resolve, reject) => {
  // We call resolve(...) when what we were doing asynchronously was successful, and reject(...) when it failed.
  // In this example, we use setTimeout(...) to simulate async code.
  // In reality, you will probably be using something like XHR or an HTML5 API.
  setTimeout( function() {
    resolve("Success!")  // Yay! Everything went well!
  }, 250)
})

myFirstPromise.then((successMessage) => {
  // successMessage is whatever we passed in the resolve(...) function above.
  // It doesn't have to be a string, but if it is only a succeed message, it probably will be.
  console.log("Yay! " + successMessage)
});
```

- From [W3Schools](https://www.w3schools.com/js/js_promise.asp), here is an example of the syntax for creating your own `Promise` object:  

```javascript
let myPromise = new Promise(function(myResolve, myReject) {
// "Producing Code" (May take some time)

  myResolve(); // when successful
  myReject();  // when error
});

// "Consuming Code" (Must wait for a fulfilled Promise)
myPromise.then(
  function(value) { /* code if successful */ },
  function(error) { /* code if some error */ }
);
```

- The examples create a new `Promise` object and save it to a variable (e.g., `myPromise`)  
- The argument passed into the `new Promise ()` object is a function definition  
- This `Promise` object represents the eventual completion of the argument function inside it  
- That argument function definition has two arguments of its own, both of which are functions    
- Inside the the body of the argument function, you can call one or both functions and write whatever other code you want  
- This code inside the body of the argument function is called when the `Promise` is created  
- In the `MDN` example above, you see the `setTimeout` takes time to execute, and when it's done, it calls the `resolve` argument, which is the function that contains the data you want    
- Now, to consume the `Promise`, you use the `.then()` method to access the data returned inside the `Promise`  
- The `.then()` method, like you saw above with `fetch`, takes a function as an argument (here, it actually takes two arguments)  
- The argument inside those argument functions are the data you want, in the example above, it's the `value` and `error` variables  
- Those variables contain the actual data that you want to use in your app    
- It's okay if you don't yet understand `Promises`; they are complicated and take time to understand; this is intended only as an introduction to get you some initial exposure to the topic    
- For now, know how to use the `fetch` function  
- In addition to the other links in this section, here are [more examples](https://www.w3schools.com/js/js_promise.asp), [more reading and examples](https://javascript.info/promise-basics), and here is [more reading](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Promises#improvements_with_promises)  

### Objects

- The `fetch` function returns an HTTP request, and you can use the `json()` method to access the JSON data from third-party APIs 
- When you use that `json()` function, it returns a `Promise` containing a JavaScript object  
- It's good practice to console log that object to see its structure  
- Here is an example of a JavaScript object from a third-party API's JSON data:  


## [Live Coding](#live-coding)   

The live coding session continues working on the live code from the previous lessons. Here are the tasks:  

1. 
