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

## [Fetch Promises and Objects](#fetch-promises-and-objects)    

## [Live Coding](#live-coding)   

The live coding session continues working on the live code from the previous lessons. Here are the tasks:  

1. 
