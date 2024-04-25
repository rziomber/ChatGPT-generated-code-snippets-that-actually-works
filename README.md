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

Write an Arduino function that takes callback function and any number of optional parameters for them. Don't use templates.
```c
typedef void (*callback)(void *params[], int num_params); // Define callback function type

// Function that takes a callback function and any number of optional parameters
void myFunction(callback func, void *params[], int num_params)
{
  // Store the callback function and its parameters in a variable
  // so that it can be called later
  callback myCallback = func;

  // Call the callback function with the parameters
  myCallback(params, num_params);
}

// Example usage:
void myCallbackFunction(void *params[], int num_params)
{
  // Loop through the parameters and print them to the serial monitor
  for (int i = 0; i < num_params; i++) {
    if (params[i] != NULL) {
      Serial.print("Parameter ");
      Serial.print(i+1);
      Serial.print(": ");
      
      // Handle different parameter types
      if (sizeof(params[i]) == sizeof(int)) {
        Serial.println(*((int *)params[i]));
      } else if (sizeof(params[i]) == sizeof(float)) {
        Serial.println(*((float *)params[i]));
      } else if (sizeof(params[i]) == sizeof(double)) {
        Serial.println(*((double *)params[i]));
      } else if (sizeof(params[i]) == sizeof(char *)) {
        Serial.println(*((char **)params[i]));
      } else {
        Serial.println("(unknown type)");
      }
    }
  }
}

void setup()
{
  // Define parameters to pass to the callback function
  int int_param = 42;
  float float_param = 3.14;
  char *string_param = "Hello world!";

  // Create an array to hold the parameters
  void *params[] = {&int_param, &float_param, &string_param};

  // Call myFunction with the callback function and its parameters
  myFunction(myCallbackFunction, params, 3);
}

void loop()
{
  // Do something
}
```
Write a Qt C++ function that receives data from QBluetooth and stores it in QBitArray.
Slot for  connect(Bluetooth::socket, &QBluetoothSocket::readyRead, this, &MainWindow::receiveReadings);
```cpp
void MainWindow::receiveReadings()
{
    QByteArray data = Bluetooth::socket->readAll();
    QBitArray bits(data.count() * 8);
    for (int i = 0; i < data.count(); ++i) {
        for (int b = 0; b < 8; ++b) {
            bits.setBit(i * 8 + b, data.at(i) & (1 << b));
        }
    }
    // Use the 'bits' QBitArray as needed
}
```
Write a C++ class. Member function should take callback function and optional parametrs of any type for that callback. Store them in member variable, so they could be callback later.
(own code)
```cpp
#include <iostream>
#include <functional>

//https://vittorioromeo.info/index/blog/passing_functions_to_functions.html
class MyClass
{
public:
  template < typename T = decltype ([]()constexpr{}), typename ... Types >
  void addFunction (T g = {}, Types ... args)
  {
    callBack =[g, args ...] ()
    {
      (g) (args ...);
    };
  }

  void run ()
  {
    callBack ();
  }

private:
  std::function < void () > callBack;
};

void test ()
{
  std::cout << "Hello!\n";
}

void test2 (int r)
{
  std::cout << "Hello! " << r << "\n";
}

int main ()
{
  auto test3 = [](int r) { std::cout << "Hello " << r << "\n"; };
  MyClass obj;
  obj.addFunction (test3,6);
  obj.run ();
}
```
```cpp
#include <functional>
#include <iostream>

class MyClass {
  public: template <typename Callback, typename...Args>
  void setCallback(Callback callback, Args && ...args) {
    callback_ = std::bind(callback, std::forward <Args> (args)...);
    //callback_ = [callback, args...]() mutable {callback(args...);};
  }

  void invokeCallback() {
    if (callback_) {
      callback_();
    }
  }

  private: std::function <void()> callback_;
};

void callbackFunction(const std::string & message) {
  std::cout << "Callback message: " << message << std::endl;
}

void anotherCallback(int a, double b, const char * c) {
  std::cout << "Callback message: a = " << a << ", b = " << b << ", c = " << c << std::endl;
}

void andAnotherCallback() {
  std::cout << "Callback without arguments" << std::endl;
}

int main() {
  MyClass obj;
  obj.setCallback(callbackFunction, "Hello from callback!");
  obj.invokeCallback();

  obj.setCallback(anotherCallback, 10, 3.14, "world");
  obj.invokeCallback();

  obj.setCallback(andAnotherCallback);
  obj.invokeCallback();
  return 0;
}
```

Custom method to mix strings and variables for Arduino.
```cpp
template <typename C> void universal_print(C print_class) {}
template <typename C, typename T, typename... Args>
void universal_print(C print_class, T value, Args... args) {
  print_class->print(value);
  universal_print(print_class, args...);
}

void setup() {
  Serial.begin(9600);
}

void loop() {
  float temp = 12.3;
  float hum = 23.4;
  universal_print(&Serial,"temperature ", temp, " C\n");
  universal_print(&Serial,"temperature ", temp, " C humidity ", hum, "%\n");
  delay(1000);
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

