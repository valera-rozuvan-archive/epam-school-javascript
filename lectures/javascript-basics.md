# Lecture 1
## JavaScript Basics

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
