# TestingJavascript

### 1.Fundamentals of Testing in JavaScript

**jest**-

     jest --watch #runs jest -o by default
     jest --watchAll #runs all tests

**automated test**-code that throws an error when the actual result of something does not match expected output

      const sum = (a, b) => a - b
      result = sum(7, 3)
      expected = 10
      
      if (result !== expected){
       throw new Error(`${result} is not equal to ${expected}`)
      }

**Jest matches**

* **expect:** gives you access to a number of "matchers" that let you validate different things.
* **toEqual** to compare recursively all properties of object instances (also known as "deep" equality)
* **toBeGreaterThan:** to compare received > expected for number or big integer values.
* **toBeLessThan:** to compare received < expected for number or big integer values
* more information about the matches: https://jestjs.io/docs/expect

**testing framework's** job is to help developers identify what's been broken as quickly as possible

**npx jest**-will automatically pick up jest.test.js file based of that convention

**npx jest**is good because it will show you really helpful error messages and even code frame to show us exactly where our code thar error was been thrown


**A callback**is a function passed as an argument to another function

**example**

         function greeting(name) {
          alert(`Hello, ${name}`);
         }

      function processUserInput(callback) {
       const name = prompt("Please enter your name.");
       callback(name);
        }

      processUserInput(greeting);
      
      
  ### 2. Javascript mocking fundamentals
  
  **mocking** -is. also about creating faster and simpler tests
  
 * to mock the entire module you use jest.mock(1st argument is the path to the module that you are mocking and the 2nd argument is the module factory. function that will return the mocked version of the module
    * Example: 
    
          banana.js //file name
          module.exports = () => 'banana';
          
         
          __tests__/test.js // test file name
          jest.mock('../banana');
          const banana = require('../banana'); // banana will be explicitly mocked.
          banana(); // will return 'undefined' because the function is auto-mocked.
          
 * jest allows you to externalize your mock by using __mocks__ directort which jest can load automatically
 
  **How to mock an API call in function**
  
  * import the module you want to mock into your test file
  * jest.mock() the module
  * use .MockResolvedValue(<mocked response>) to mock the response
      
  **Mock implementations**
      
  * **mockReset()**-This is useful when you want to completely reset a mock back to its initial state
  * **mockRestore()**- This is useful when you want to mock functions in certain test cases and restore the original implementation in others
      
 **Mock functions**-keeps track of what arguments get called with
      
* jest.fn(implementation with mock)
* jest.isMockFunction(fn)
* jest.spyOn(object,methodName)
* toHaveBeenCalledTimes(number)- to ensure that a mock function got called exact number of times
* toHaveReturnedWith(value)- to ensure that a mock function returned a specific value

* more mock functions: https://jestjs.io/docs/expect
