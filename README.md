# TestingJavascript

### 1.Fundamentals of Testing in JavaScript

**jest**-

**automated test**-code that throws an error when the actual result of something does not match expected output

      const sum = (a, b) => a - b
      result = sum(7, 3)
      expected = 10
      
      if (result !== expected){
       throw new Error(`${result} is not equal to ${expected}`)
      }

**Jest matches**

**expect:** gives you access to a number of "matchers" that let you validate different things.
 
**toEqual** to compare recursively all properties of object instances (also known as "deep" equality)

**toBeGreaterThan:** to compare received > expected for number or big integer values.

**toBeLessThan:** to compare received < expected for number or big integer values

more information about the matches: https://jestjs.io/docs/expect

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

