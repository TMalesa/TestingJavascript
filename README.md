# TestingJavascript

### 1.Fundamentals of Testing in JavaScript

* **automated tset** -is a code that throws an error when the actual result of something does not match the expected output

Example: 

     const sum = (a, b) => a - b
      result = sum(7, 3)
      expected = 10
      
      if (result !== expected){
       throw new Error(`${result} is not equal to ${expected}`)
      }

* the above code will throw an error because the expected value is not correct,you will get -4 is not equal to 10
* if you change   const sum = (a, b) => a - b to   const sum = (a, b) => a + b, then the script will pass without throwing an error
* The Javascript testing framework is to make that error message as useful as possible so we can quickly identify what the problem is and fix it.
* A testing framework's job is to help developers identify what's broken as quickly as possible

### 2. Javascript mocking fundamentals

* Jest- is a JavaScript-based framework for testing React, React Native and other JavaScript-based applications.
* In many cases, unit tests don't provide accurate results when run on the frontend of any software.
* Jest reduces this issue by allowing you to write faster, more effective front-end tests.

**To install jest**
* npm install --save-dev jest

**runs jest -o by default**
  * jest --watch 

**runs all tests**
  * jest --watchAll 
     
**Jest matches**

* **expect:** gives you access to a number of "matchers" that let you validate different things.
* **toEqual** to compare recursively all properties of object instances (also known as "deep" equality)
* **toBeGreaterThan:** to compare received > expected for number or big integer values.
* **toBeLessThan:** to compare received < expected for number or big integer values
* more information about the matches: https://jestjs.io/docs/expect

**npx jest**-will automatically pick up jest.test.js file based of that convention

**npx jest**is good because it will show you really helpful error messages and even code frame to show us exactly where our code thar error was been thrown

Sum function:
 
       function sum(a, b) {
       return a + b;
       }
      module.exports = sum;
      
Testing the sum function:

       const sum = require('./sum');

       test('adds 1 + 2 to equal 3', () => {
       expect(sum(1, 2)).toBe(3);
        });
        
Add the following section to your package.json:

         {
            "scripts": {
            "test": "jest"
             }
         }
         
Finally, run yarn test or npm test and Jest will print this message:

          PASS  ./sum.test.js
          ✓ adds 1 + 2 to equal 3 (5ms)
          
  **mocking** -is also about creating faster and simpler tests
  
 * to mock the entire module you use jest.mock(1st argument is the path to the module that you are mocking and the 2nd argument is the module factory. function that will return the mocked version of the module

forEach.js: 

         export function forEach(items, callback) {
         for (let index = 0; index < items.length; index++) {
         callback(items[index]);
           }
         }
         
* To test this function, we can use a mock function, and inspect the mock's state to ensure the callback is invoked as expected.

forEach.test.js:

        const forEach = require('./forEach');

        const mockCallback = jest.fn(x => 42 + x);

        test('forEach mock function', () => {
        forEach([0, 1], mockCallback);

        // The mock function was called twice
        expect(mockCallback.mock.calls).toHaveLength(2);

        // The first argument of the first call to the function was 0
        expect(mockCallback.mock.calls[0][0]).toBe(0);

       // The first argument of the second call to the function was 1
       expect(mockCallback.mock.calls[1][0]).toBe(1);

       // The return value of the first call to the function was 42
       expect(mockCallback.mock.results[0].value).toBe(42);
       });


          
 * jest allows you to externalize your mock by using __mocks__ directort which jest can load automatically
 
  **How to mock an API call in function**
  
  * import the module you want to mock into your test file
  * jest.mock() the module
  * use .MockResolvedValue(<mocked response>) to mock the response
     
  Mock API Example:
     
          // index.test.js
         const getFirstAlbumTitle = require("./index");
         const axios = require("axios");
     
         jest.mock("axios");

     
 * After importing a module and running jest.mock(<module-name>), you have complete control over all functions from that module. You control these functions even if they're called inside another imported function.
     

          it("returns the title of the first album", async () => {
          axios.get.mockResolvedValue({
          data: [
          {
          userId: 1,
          id: 1,
          title: "My First Album",
          },
          {
         userId: 1,
         id: 2,
         title: "Album: The Sequel",
         },
        ],
        });

        const title = await getFirstAlbumTitle();
        expect(title).toEqual("My First Album");
        });
     
 * This sets the default value to return whenever the method is called. Simply put: you can make axios.get() return whatever you want
      
  **Mock implementations**
 
 * **mockImplementation**-Accepts a function that should be used as the implementation of the mock. The mock itself will still record all calls that go into and instances that come from itself – the only difference is that the implementation will also be executed when the mock is called.
  * **mockReset()**-This is useful when you want to completely reset a mock back to its initial state
  * **mockRestore()**- This is useful when you want to mock functions in certain test cases and restore the original implementation in others
      
 **Mock functions**-keeps track of what arguments get called with
      
* jest.fn(implementation with mock)
* jest.isMockFunction(fn)
* jest.spyOn(object,methodName)
* toHaveBeenCalledTimes(number)- to ensure that a mock function got called exact number of times
* toHaveReturnedWith(value)- to ensure that a mock function returned a specific value

* more mock functions: https://jestjs.io/docs/expect

### 3. Test Node.js Backends
     
### 4. Test Node.js Backends
     
### 5. Test Node.js Backends

### 6. Test Node.js Backends

* Testing pure functions is one of the nicest things that you can do because pure functions are pretty simple to test
* to run the test run "npm t"

   Example: Unit Tests for a Simple Pure Function
   
             auth.js//file name
             function isPasswordAllowed(password) {
             return (
             password.length > 6 &&
             // non-alphanumeric
             /\W/.test(password) &&
             // digit
             /\d/.test(password) &&
             // capital letter
             /[A-Z]/.test(password) &&
            // lowercase letter
            /[a-z]/.test(password)
            );
            }
            
Example: testing

         auth.exercise.js//test file
         import { isPasswordAllowed } from "../auth";//import auth function
         //We'll expect that to be true. It should return true because that's a valid password.
         test("isPasswordAllowed returns true for valid passwords", () => {
         expect(isPasswordAllowed("!aBc123")).toBe(true);
          });
            //We'll expect that to be false. It should return false because that's a invalid password.
          test("isPasswordAllowed returns false for invalid passwords", () => {
          expect(isPasswordAllowed("a2c!")).toBe(false);
          expect(isPasswordAllowed("123456!")).toBe(false);
          expect(isPasswordAllowed("ABCdef!")).toBe(false);
          expect(isPasswordAllowed("abc123!")).toBe(false);
          expect(isPasswordAllowed("ABC123!")).toBe(false);
          expect(isPasswordAllowed("ABCdef123")).toBe(false);
          });
          

**Improve Error Messages by Generating Test Titles**

* One of the most crucial things you can do when writing tests is ensuring that the error message explains the problem as clearly as possible so it can be addressed quickly
*  The error message that you will see it will look like you forgot to save this disallow. Now we have this disallows this particular password, makes it a little bit easier to see which one of these is failing. We don't have to look through the stack trays.

Example : testing
 
          auth.exercise.js//test file
          describe('isPasswordAllowed only allows some passwords', () => {
          const allowedPasswords = ['!aBc123']
          const disallowedPasswords = [
          'a2c!',
          '123456!',
          'ABCdef!',
          'abc123!',
          'ABC123!',
          'ABCdef123',
           ]
           }


         allowedPasswords.forEach(password => {
         test(`allows ${password}`, () => {
         expect(isPasswordAllowed(password)).toBe(true);
         });
         });

        disallowedPasswords.forEach(password => {
        test(`disallows ${password}`, () => {
         expect(isPasswordAllowed(password)).toBe(false);
         });
         });
         
 **jest-in-case**
 
 * to Reduce Duplication 
 * import cases from "jest-in-case";
 
 Example: testing using case
             
             import cases from 'jest-in-case'
             import {isPasswordAllowed} from '../auth'
             cases(
             "isPasswordAllowed: invalid passwords",
             options => {
              expect(isPasswordAllowed(options.password)).toBe(false);
              },
              {
              "too short": {
              password: "a2c!"
               },
              "no letters": {
               password: "123456!"
              },
              "no numbers": {
              password: "ABCdef!"
              },
              "no uppercase letters": {
              password: "abc123!"
              },
             "no lowercase letters": {
              password: "ABC123!"
              },
              "no non-alphanumeric characters": {
              password: "ABCdef123"
              }
              }
              );
              
* This will give us invalid passwords with the clear description for why they're invalid.

**Test Node Middleware**

**different types of middleware that Express has**

* **Application-level** middleware (our app isn't really using this kind)
* **Router-level** middleware (all our routes use this strategy of middleware)
* **Error-handling** middleware (this is what error-middleware.js is)
* **Built-in** middleware (we're not using any of these)
* **Third-party** middleware (we're using a few of these, like cors, body-parser, express-jwt, and passport).

* The one that we're going to be working with is the error handler, which accepts an error as the first argument, the request as the second response, and then the next function.
* The purpose of our errorMiddleware is to just catch errors which have happened throughout the app. It's like a fallback.

Function: error-middleware.js 
       
        function errorHandler(err, req, res, next) {
        console.error(err.stack);
        res.status(500).send("Something broke!");
        }
        
 Function: src/utils/error-middleware.js
 
          function errorMiddleware(error, req, res, next) {
          if (res.headersSent) {
          next(error);
          } else if (error instanceof UnauthorizedError) {
         res.status(401);
         res.json({ code: error.code, message: error.message });
         } else {
         res.status(500);
         res.json({
         message: error.message,
         // we only add a `stack` property in non-production environments
         ...(process.env.NODE_ENV === "production" ? null : { stack: error.stack })
         });
         }
         }
         
 Testing :error-middleware.exercise.js
            
         import {UnauthorizedError} from 'express-jwt'
         import `errorMiddleware` from '../error-middleware'
          test("responds with 401 for express-jwt UnauthorizedError", () => {
          const req = {};
           const next = jest.fn();
           const res = { json: `jest`.fn(() => res), status: `jest`.fn(() => res) };
            const code="some_error_code",
            const message= "some message"
            const error = new UnauthorizedError("some_error_code", {message});
             errorMiddleware(error, req, res, next);
             expect(next).not.toHaveBeenCalled();
             expect(res.json).toHaveBeenCalledWith({
             code:error.code,
              message: error.message})
              expect(res.status).toHaveBeenCalledWith(401);
              expect(res.status).toHaveBeenCalledTimes(1);
              expect(res.json).toHaveBeenCalledTimes(1);
              });
         
         
         
* **Important abouth what we are testing** is that when you call the error middleware with an unauthorised error that the next is not called,the status is called with 401 and is called once,the json is going to be called with the object that has code property that came from the error and the message property that came from the error abd we expect that is only called once.


* Unit Test for Handling headersSent in an Error Middleware
           
 Testing :error-middleware.exercise.js
         
         import `errorMiddleware` from '../error-middleware'
          test("call next if header is true", () => {
          const req = {};
           const next = jest.fn();
           const res = { json: `jest`.fn(() => res), status: `jest`.fn(() => res), headerset: true};
            const error = new Error("blah");
             errorMiddleware(error, req, res, next);
             expect(next).toHaveBeenCalledWith(error);
             expect(next).toHaveBeenCalled(1);
              expect(res.status).not.toHaveBeenCalled();
              expect(res.json).not.toHaveBeenCalled();
              });

**Improve Test Maintainability using the Test Object Factory Pattern**
     
     * we’ll apply the object factory pattern to reduce duplication and make it easier to maintain our tests.
     
     Example: Reducing duplication on the previous test
     
           function buildRes(overrides) {
            const res = {
            json: jest.fn(() => res),
            status: jest.fn(() => res),
            ...overrides
            };
            return res;
            }
     
      Testing :error-middleware.exercise.js
            
         import {UnauthorizedError} from 'express-jwt'
         import `errorMiddleware` from '../error-middleware'
          test("responds with 401 for express-jwt UnauthorizedError", () => {
          const req = {};
           const next = jest.fn();
          **const res = buildRes();**
            const code="some_error_code",
            const message= "some message"
            const error = new UnauthorizedError("some_error_code", {message});
             errorMiddleware(error, req, res, next);
             expect(next).not.toHaveBeenCalled();
             expect(res.json).toHaveBeenCalledWith({
             code:error.code,
              message: error.message})
              expect(res.status).toHaveBeenCalledWith(401);
              expect(res.status).toHaveBeenCalledTimes(1);
              expect(res.json).toHaveBeenCalledTimes(1);
              });
         
      Testing :error-middleware.exercise.js
         
         import `errorMiddleware` from '../error-middleware'
          test("call next if header is true", () => {
          const req = {};
           const next = jest.fn();
           **const res = buildRes({headerset: true});**
            const error = new Error("blah");
             errorMiddleware(error, req, res, next);
             expect(next).toHaveBeenCalledWith(error);
             expect(next).toHaveBeenCalled(1);
              expect(res.status).not.toHaveBeenCalled();
              expect(res.json).not.toHaveBeenCalled();
              });
     
 * we created this buildRes function that accepts some overrides. It creates our normal response object, and then spreads the overrides over the properties of this default response object that we are creating.
     
 **Test Node Controllers**
     
 * Controllers are a collection of middleware that applies business logic specific to your domain. 
 * Typically these are tested like any other middleware, but often they require mocking the database for unit tests.
