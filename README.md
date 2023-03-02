# ChatGPT generated code snippets that actually works

Some fragments has been edited by the author.

How to split string to char array by space?
```c
#include <stdio.h>
#include <string.h>

#define MAX_WORDS 10
#define MAX_LENGTH 20

int main() {
    char str[] = "The quick brown fox jumps over the lazy dog";
    char *words[MAX_WORDS];
    int i = 0;

    // split the string into words
    char *token = strtok(str, " ");
    while (token != NULL && i < MAX_WORDS) {
        words[i++] = token;
        token = strtok(NULL, " ");
    }

    // print out the words
    printf("Words in the string:\n");
    for (int j = 0; j < i; j++) {
        printf("%s\n", words[j]);
    }

    return 0;
}
```


C code that shows digit in given position from given number.
```c
#include <stdio.h>
#include <math.h>

int main() {
    int number, position, digit;
    
    printf("Enter a number: ");
    scanf("%d", &number);
    
    printf("Enter the position of the digit to extract: ");
    scanf("%d", &position);
    
    digit = (number / (int) pow(10, position - 1)) % 10;
    
    printf("The digit at position %d is %d\n", position, digit);
    
    return 0;
}

```

Make a HTML code for a website using CSS grid with three div levels:

header

left content right

footer
```html
<html>
  <head>
    <style>
      .grid-container {
        display: grid;
        grid-template-columns: 25% 50% 25%;
        grid-template-rows: auto;
        grid-template-areas: "header header header" "left content right" "footer footer footer";
      }

      .header {
        grid-area: header;
        background-color: #333;
        color: white;
        text-align: center;
      }

      .left {
        grid-area: left;
        background-color: #ccc;
        padding: 20px;
      }

      .content {
        grid-area: content;
        background-color: #fff;
        padding: 20px;
      }

      .right {
        grid-area: right;
        background-color: #ccc;
        padding: 20px;
      }

      .footer {
        grid-area: footer;
        background-color: #333;
        color: white;
        text-align: center;
      }
    </style>
  </head>
  <body>
    <div class="grid-container">
      <div class="header">Header</div>
      <div class="left">Left Content</div>
      <div class="content">Main Content</div>
      <div class="right">Right Content</div>
      <div class="footer">Footer</div>
    </div>
  </body>
</html>
```
Rewrite this code using CSS flexbox.

```html

<html>
  <head>
    <style>
      .flex-container {
        display: flex;
        flex-direction: column;
        height: 100vh;
      }

      .header {
        background-color: #333;
        color: white;
        text-align: center;
      }

      .content-container {
        display: flex;
        flex-direction: row;
        flex: 1;
      }

      .left {
        background-color: #ccc;
        padding: 20px;
        width: 25%;
      }

      .right {
        background-color: #ccc;
        padding: 20px;
        width: 25%;
      }

      .main-content {
        background-color: #fff;
        padding: 20px;
        width: 50%;
      }

      .footer {
        background-color: #333;
        color: white;
        text-align: center;
      }
    </style>
  </head>
  <body>
    <div class="flex-container">
      <div class="header">Header</div>
      <div class="content-container">
        <div class="left">Left Content</div>
        <div class="main-content">Main Content</div>
        <div class="right">Right Content</div>
      </div>
      <div class="footer">Footer</div>
    </div>
  </body>
</html>
```
Use Bootstrap to write this website.
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <link
      rel="stylesheet"
      href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
      integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T"
      crossorigin="anonymous"
    />
    <title>My Website</title>
  </head>
  <body>
    <header class="bg-primary text-white text-center p-3">
      <h1>Header</h1>
    </header>

    <div class="container my-5">
      <div class="row">
        <div class="col-sm-4 bg-secondary p-3 text-white">
          Left Content
        </div>
        <div class="col-sm-4 bg-light p-3">Main Content</div>
        <div class="col-sm-4 bg-secondary p-3 text-white">
          Right Content
        </div>
      </div>
    </div>

    <footer class="bg-primary text-white text-center p-3">
      <h3>Footer</h3>
    </footer>
  </body>
</html>
```

