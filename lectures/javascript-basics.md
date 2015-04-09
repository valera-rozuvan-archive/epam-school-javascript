# Lecture 1
## JavaScript Basics

### Development environment

For this lecture we will be using
[Google Chrome browser](http://www.google.com/chrome/) to test our code. You can
write your code in any text editor or IDE.

### Getting your code to run

Create a file called `index.html` with the following contents:

    <html>
      <head>
        <title>Sample JavaScript code</title>
      </head>
      <body>
        <div id="some_text">Hello, world</div>

        <script type="text/javascript">
          // Execute a callback function when DOM is loaded.
          function ready(callback) {
            if (document.readyState != 'loading'){
              callback();
            } else {
              document.addEventListener('DOMContentLoaded', callback);
            }
          }

          // Main entry point of our code. All sample code should be placed
          // in this function.
          function main() {
            alert('We are in main() function.');
          }

          // Call the function main() when DOM is loaded.
          ready(main);
        </script>
      </body>
    </html>

Open this file with the Chrome browser, and see that you get a pop-up message
`We are in main() function.`.

For the rest of this document, only the contents of the `main()` function will
be shown when we discuss a new concept.

### Debugging and checking for errors

To see any runtime errors (warnings, etc.), please open the JavaScript Console.
To do this, either press the hot-key combination `Ctrl+Shift+j` or select from
the Chrome menu `More Tools -> JavaScript console`.

### Basic functions

We will create a function which will output a message to the user. We will use
this function, so that the user will see the message.

    function main() {
      // Function definition.
      function outputMessage() {
        alert('Hello, user!');
      }

      // Invoke the function defined above.
      outputMessage();
    }

### Functions with parameters

What if we want our function to behave differently in some cases? We can make
it accept arguments which will provide different behavior.

    function main() {
      // Function that accepts a parameter `messageForUser`, and outputs
      // the parameter for the user to see.
      function outputMessage(messageForUser) {
        alert(messageForUser);
      }

      // Greet the user.
      outputMessage('Hello, user!');

      // Tell him what programming language he should use.
      outputMessage('You should use JavaScript.');
    }

### For loops

If we want to do something many-many times, for example tell the user 20 times
that he should save his work periodically, we can do something like this:

    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');
    outputMessage('Please save your files!');

However, this seems rather inefficient, especially if you have to write code to
do something 1000 times (or more). The `for loop` comes to the rescue!

    function main() {
      function outputMessage(messageForUser) {
        alert(messageForUser);
      }

      // Use a loop. Iterate 20 times.
      for (var i = 1; i <= 20; i += 1) {
        outputMessage('Please save your files!');
      }
    }

Much better.

### Variables and their types

In practice you need variables to store the data you are working with. In
JavaScript there are several types that a variable (data) can be:

- boolean
- null
- undefined
- number
- string
- array
- object

Examples of how to define and store each type in a variable:

    function main() {
      function outputMessage(messageForUser) {
        alert(messageForUser);
      }

      var bool = true;

      var nullVariable = null;

      var undefVar = undefined;
      var undefVar2;

      var num = -23;
      var num2 = 45.1;

      var str = 'Hello, world';

      var myArray = ['asfd', 0, null];
      var myArray2 = [];

      var myObj = {
        property1: 123,
        property2: {
          subProp: 'Hello'
        }
      };
      var myObj2 = {};
    }

### Scope and hoisting

This is a tricky concept in JavaScript. I will take the explanation from the
Mozilla resource
[Variable Scope (JavaScript)](https://msdn.microsoft.com/en-us/library/ie/bzt2dkta%28v=vs.94%29.aspx).

JavaScript has two scopes: global and local. A variable that is declared outside
a function definition is a global variable, and its value is accessible and
modifiable throughout your program. A variable that is declared inside a
function definition is local. It is created and destroyed every time the
function is executed, and it cannot be accessed by any code outside the
function. JavaScript does not support block scope (in which a set of braces
`{. . .}` defines a new scope), except in the special case of block-scoped
variables.

A local variable can have the same name as a global variable, but it is entirely
separate; changing the value of one variable has no effect on the other. Only
the local version has meaning inside the function in which it is declared.

    function main() {
      // Global definition of aCentaur.
      var aCentaur = "a horse with rider,";

      // A local aCentaur variable is declared in this function.
      function antiquities(){

         var aCentaur = "A centaur is probably a mounted Scythian warrior";
      }

      antiquities();
      aCentaur += " as seen from a distance by a naive innocent.";

      alert(aCentaur);

      // Output: "a horse with rider, as seen from a distance by a naive innocent."
    }

In JavaScript, variables are evaluated as if they were declared at the beginning
of the scope they exist in. Sometimes this results in unexpected behavior, as
shown here.

    function main() {
      var aNumber = 100;
      tweak();

      function tweak(){

          // This prints "undefined", because aNumber is also defined locally below.
          alert(aNumber);

          if (false)
          {
              var aNumber = 123;
          }
      }
    }

When JavaScript executes a function, it first looks for all variable
declarations, for example, `var someVariable;`. It creates the variables with an
initial value of `undefined`. If a variable is declared with a value, for example,
`var someVariable = "something";`, then it still initially has the value `undefined`
and takes on the declared value only when the line that contains the declaration
is executed.

JavaScript processes all variable declarations before executing any code,
whether the declaration is inside a conditional block or other construct. Once
JavaScript has found all the variables, it executes the code in the function.
If a variable is implicitly declared inside a function - that is, if it appears
on the left side of an assignment expression but has not been declared with
`var` - it is created as a global variable.

### Closures

In JavaScript, an inner (nested) function stores references to the local
variables that are present in the same scope as the function itself, even after
the function returns. This set of references is called a closure. In the
following example, the second call to the inner function outputs the same
`message ("Hello Bill")` as the first call, because the input parameter for the
outer function, `name`, is a local variable that is stored in the closure for the
inner function.

    function main() {
      function send(name) {
          // Local variable 'name' is stored in the closure
          // for the inner function.
          return function () {
              sendHi(name);
          }
      }

      function sendHi(msg) {
          alert('Hello ' + msg);
      }

      var func = send('Bill');
      func();
      // Output:
      // Hello Bill
      sendHi('Pete');
      // Output:
      // Hello Pete
      func();
      // Output:
      // Hello Bill
    }

Another example of a closure:

    function main() {
      var newCount = 0;

      var counterStorage = function () {
        var _counter = 0;
        return {
          increase: function () {
            _counter += 1;
          },
          get: function () {
            return _counter;
          }
        };
      };

      var counterObj = counterStorage();

      // Increase count of user clicks.
      counterObj.increase();
      counterObj.increase();
      counterObj.increase();
      counterObj.increase();
      counterObj.increase();
      counterObj.increase();
      counterObj.increase();

      // Show hoe many clicks user made. Should be 7.
      alert(counterObj.get());

      // ...
    }
