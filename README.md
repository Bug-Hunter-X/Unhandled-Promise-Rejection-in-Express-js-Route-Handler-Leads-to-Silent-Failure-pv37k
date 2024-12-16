# Unhandled Promise Rejection in Express.js Route Handler

This repository demonstrates a common, yet subtle, bug in Express.js applications: unhandled promise rejections within route handlers.  When an asynchronous operation inside a route handler throws an error, and that error isn't properly caught and handled within the promise chain, the request might hang indefinitely without sending a response to the client.  This can lead to frustrating debugging sessions.

## The Bug

The `bug.js` file contains an Express.js application with a route handler that performs an asynchronous operation.  This operation has a 50% chance of failing and throwing an error. If the error occurs, the error is logged to the console, but no response is sent back to the client, resulting in a timeout.

## The Solution

The `bugSolution.js` file demonstrates the correct way to handle this.  It shows how to catch the error within the `.catch()` block of the promise and send an appropriate error response to the client. This ensures a graceful response and prevents the silent failure.

## How to Reproduce

1. Clone this repository.
2. Navigate to the repository directory.
3. Run `node bug.js`.
4. Make several requests to `http://localhost:3000/`. You will observe that sometimes the request hangs.
5. Now run `node bugSolution.js` and repeat step 4. You will observe that you get a proper response even when an error occurs.