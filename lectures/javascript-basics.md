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

### Variables and their types.

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
