# Getting started with Node.js

### Introduction

* Node.js is an ==open source== and ==cross-platform== JavaScript runtime environment
* Node.js runs the ==V8 JavaScript engine==, the core of Google Chrome, outside of the browser
* A node.js app runs in a ==single process==, without creating a new thread for every request
* Node.js uses ==event driven, non blocking I/O model== to handle concurrent requests with single thread

### Why Node.js is popular

* JavaScript Everywhere (Client + Server)
* Fast performance
* Lightweight - build in event driven architectures
* Faster time to market (Reduces development time)
* Cross platform - creating APIs
* Vast number of libraries and packages (npm packages)
* Can be hosted anywhere

### Apps that can be build using Node.js

* Streaming web applications like Netflix
* Realtime web applications like Chat
* Microservices and IOT applications
* Any MERN stack application like ecommerce
* Social media and networking applications like LinkedIn
* Restful APIs - can be consumed by frontend or mobile apps

### Node.js vs Browser

* Both Browser and Node.js use ==JavaScript== as their programming language
* However, ==building apps== that run in the browser is ==completely different== thing from building a Node.js application
* Browser has access to the ==DOM and Web API== while Node.js uses modules to provide access to the ==file system and OS==
* Node.js support both the ==CommonJS require()== and ==ES module systems import()== while the browser implements ES modules standards
* 
## JavaScript Fundamentals one should Know

- Classes
- Arrays and objects
- Functions
- Scopes and Loops
- Variables
- Expressions
- Async and Await
- Closures
- Async programming and callbacks
- Event Loops
- Types

### Coding
How to start a node js project:
1. Create a new folder for the project
2. Navigate to the folder using terminal
3. Type `npm init` command and enter
4. In the package.json file, under scripts, add this line: `"start": "node index.js"`
5. Create the index.js file and add code. e.g. `console.log("Hello World")`
6. Use either `node index.js` or `npm start` to run 


When we make a change, node.js should automatically detect and execute it. To do that we install a package known as nodemon using the following command:
* `npm i -g nodemon` if you want to install globally
* `npm i --save-dev nodemon` as a dev dependency

Then change under scripts to: `"start": "nodemon index.js"`

### Working with Node JS
Process call for exiting Node JS: `process.exit(0)` - 0 means it will not exit. exit(1). means it will exit
Another way is writing `process.exitCode = 1` Example:
```js
console.log("My first node js tutorial")
console.log("Hi Charles")
console.log("Where are you?")
process.exit(1);
```
### How to Read environmental variables in Node Js

To pass the environmental variables in the terminal we do like this:
```powershell
$env:NAME="Charles"
$env:PROFESSION="Developer"
node env.js
```

Or
```powershell
$env:NAME="CHARLES"; $env:PROFESSION="DEVELOPER"; node env.js
```
Then we create a file named env.js and add the following code to print them:
```js
console.log(process.env.NAME);
console.log(process.env.PROFESSION)
```

Since we are not going to pass the environmental variables from the command line. We can create a .env file for the environment variables. It contents can look like this:
```powershell
NAME="Charles"
PROFESSION="Developer"
COURSE="NodeJS"
```
To make use of the .env file, we install a package called dotenv: npm i dotenv
Then we go to the env.js file, we do:
`require("dotenv").config();`
So when we run node env.js, we can use the environment variables  without passing them in the terminal. The code will look like this:
```js
require("dotenv").config()
console.log(process.env.NAME);
console.log(process.env.PROFESSION)
console.log("I am starting to learn ", process.env.COURSE)

// This will be the output
// CHARLES
// DEVELOPER
// I am starting to learn  NodeJS
```

If we dont include the first line of require("dotenv").config, we can alternatively do this in the terminal:
```powershell
node -r dotenv/config env.js
```

### Read, Evaluate, Print and Loop (REPL)
Means:
* Read - read line of code which is on the node console
* Evaluate - evaluate the line of code
* Print - Print the value
* Loop - Repeat the same thing for the next statement
Can be implemented like this:
```js
const repl = require("repl");
const local = repl.start("$ ");

// Adding an exit command
local.on("exit", () => {
    console.log("Exiting REPL");
    process.exit();
})
```
Takes one automatically to the node console
Can help one to do calculations on the fly or write functions on the node console

### How to pass arguments to your node application
The arguments refer to the all the commands typed on the terminal to run a node application.
These arguments can be printed using the `process.argv` command in node. The code can look like this:
```js
process.argv.forEach((val, index) => {
console.log(`${index}: ${val}`)
})
// Output will look like this
// 0: C:\Program Files\nodejs\node.exe
// 1: C:\Users\Charles\Documents\nodejs-tutorial\argument.js
// 2: name=charles
```
The `process.argv` command returns the arguments as array. The first two are the location of the executable program and the file to be run. The third is passed by the user. To get only the one added by the user, we can do like this:
```js
console.log(process.argv.slice(2)[0])
```

### How to output to the command line using Nodejs

Simplest way:
```js
const x = "1";
const y = "2"
console.log(x, y)
//Outputs
// 1 2
```

Format specifiers
1. `%s` formats variable to a string
2. `%d` for number
3. `%i` for integer
4. `%o` for object
Example:
```js
console.log("I am %s and my age is %d", "charles", 23)
```

For clearing the console.
```js
console.clear()
```
Counting number of times a string is printed
```js
console.count("My name is Charles")
console.count("My name is Charles")
console.count("My name is Kariuki")
console.countReset("My name is Charles")
console.count("My name is Charles")
// Outputs
// My name is Charles: 1
// My name is Charles: 2
// My name is Kariuki: 1
// My name is Charles: 1
```

Tracing execution. Can be used to trace errors
```js
const function1 = () => console.trace();
const function2 = () => function1()
function2()
```
Calculating the time span of a function
```js
const sum = () => console.log(`The sum of 2 and 3 is: ${2+3}`);
const multiply = () => console.log(`The multiplication of 2 and 3 is: ${2*3}`);
const measureTime = () => {
    console.time("sum()");
    sum();
    console.timeEnd("sum()");
    console.time("multiply()");
    multiply();
    console.timeEnd("multiply()");
}
measureTime();
// Outputs
// The sum of 2 and 3 is: 5
// sum(): 6.598ms
// The multiplication of 2 and 3 is: 6
// multiply(): 0.328ms
```

### Accepting input from users in the command Line

We can accept input using the `readline` module. 
Then create a `readline` interface that takes input from `process.stdin`, the standard input(keyboard) and outputs to `process.stdout`, the standard output (terminal)
Then, use the `readline.question()` method to prompt the user to provide their name and provide a callback function that will be executed when the user enters their name.
```js
const readline = require("readline")
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
})
rl.question(`What is your name? `, name =>{
    console.log(`Hi ${name}`);
    rl.close();
});
// The Output
// What is your name? Charles
// Hi Charles
```

An alternative is installing a package called `prompt-sync`: 
```powershell
npm i prompt-sync
```
Then use it like this:
```js
// Prompt-sync is a function, so added brackets
const prompt = require("prompt-sync")();
const name = prompt("What is your name: ");
console.log(`Hi ${name}`)

// Outputs
// What is your name: Charles
// Hi Charles
```




# Node.js Package Manager & Built-ins

* NPM is a standard package manager for NodeJS
* Provides a way of downloading and managing dependencies for both the frontend and backend applications using JavaScript
* Alternatives of NPM include yarn and pnpm
### Most significant NPM cli commands
1. `npm init`
2. `npm install`
3. `npm install <package_name> [-g, --save-dev, --no-save, --save-optional, --no-optional]`
4. `npm install <package_name>@version`
5. `npm update`
6. `npm update <package_name>`
7. `npm run <task-name>`
8. `npm list`
9. `npm view <package_name> version`
10. `npm uninstall <package_name>`
11. `npm help`

### Semantic versioning
"express": ^4.18.1
x: the first digit is the major version
y: the second digit is the minor version
z: the third digit is patch version

^4.18.1 - means only update the minor or patch version
~4.18.1 - means only update only patch version

### How to export a functionality from a Node.js file
A NodeJS file can export its functionality by adding module export or export property
Adding module export in car.js file:
```js
const ford = {
    branch: "Ford",
    model: "Fiesta"
};
module.exports = ford;
```
In the index.js file:
```js
const car = require("./car")
console.log(car)
// Outputs
// { branch: 'Ford', model: 'Fiesta' }
```

Using the exports property as an object in car.js file:
```js
// Objects
const ford = {
    branch: "Ford",
    model: "Fiesta"
};
const tesla = {
    branch: "Tesla",
    model: "Model 3"
};

exports.data = {ford, tesla};
```

In the index.js file:
```js
const car = require("./car")
console.log(car)
// Outputs
// {
//   data: {
//     ford: { branch: 'Ford', model: 'Fiesta' },
//     tesla: { branch: 'Tesla', model: 'Model 3' }
//   }
// }
```

We can also destructure the data exports property in index.js by doing:
```js
const { data } = require("./car")
console.log(data)

// Outputs
// {
//   ford: { branch: 'Ford', model: 'Fiesta' },  
//   tesla: { branch: 'Tesla', model: 'Model 3' }
// }
```

We can export each object individually in the car.js file like this:
```js
exports.ford = {
    branch: "Ford",
    model: "Fiesta"
};
exports.tesla = {
    branch: "Tesla",
    model: "Model 3"
};
```

And then in the index.js file, we use them like this:
```js
const {ford, tesla} = require("./car")
console.log(ford)
console.log(tesla)

// Outputs
// { branch: 'Ford', model: 'Fiesta' }
// { branch: 'Tesla', model: 'Model 3' }
```

# Node.js Error Handling

Errors in NodeJS are handled through exceptions with the keyword throw. 6 different ways to handle the errors:
1. Using Error Object
2. Using Custom Error objects
3. Using try and catch
4. Uncaught exceptions
5. Exceptions in promises
6. Using Async and Await

### Using the Error Object

```js
const error = new Error("Something went wrong")
console.log(error.stack)
// Shows the error stacktrace
```
```js
const error = new Error("Something went wrong")
console.log(error.message)
// show only the error message
```

An alternative to console.log is using the throw keyword
```js
// Starts with error message and shows the stack trace
throw new Error("I am error object")
```

### Using Custom Error Object

We can create a custom error object by extending the error object.
We can do so by creating a new file called CustomError.js and write the following code:
```js
class CustomError extends Error {
    constructor(message){
        super(message);
    }
}

module.exports = {CustomError}
```

Then in we can import the CustomError object and use it like this:
```js
const { CustomError } = require('./CustomError');
throw new CustomError("This is a custom error");
// It will show a stack trace beginning with:
// CustomError: This is a custom error
```

### Handling the exception using try and catch

```js
try{
    doSomething();
}catch (e){
    console.log("Error occurred");
    console.log(e);
}
// When this code runs, it will throw an error with following message
// Error occurred
// ReferenceError: doSomething is not defined
// Followed by stack trace
```


When I define the doSomething function, as below, the code will not throw an error:
```js
try{
    doSomething();
}catch (e){
    console.log("Error occurred");
    console.log(e);
}

function doSomething(){
    console.log("I am from doSomething function")
}

// Outputs
// I am from doSomething function
```

If there is an error while executing the function, the try catch will throw an exception. For example, the code below tries to use fetch method but an error occurs:

```js
try{
    doSomething();
}catch (e){
    console.log("Error occurred");
    console.log(e);
}

function doSomething(){
    const data = fetch("localhost:300/api");
}
// This code will throw an error showing fetch failed
```

### Uncaught Exceptions

This catches errors which are not known. Example code:

```js
function doSomething(){
    const data = fetch("localhost:300/api");
}

// Uncaught exception
process.on("UncaughtException", (err) => {
    console.log("There was uncaught exception", err);
    // exiting the flow of the code
    process.exit(1);
})

doSomething()
```

### Exceptions with Promises

```js
const promise = new Promise((resolve, reject) => {
    if(false){
        resolve(doSomething());
    }
    else {
        reject(doSomething());
    }
})

promise.then((val) => {
    console.log(val)
}).catch((err) => {
    console.log("Error Occurred");
    console.log(err);
});
```

The promise is resolved [accepted] when the promise is true. If false, the promise is rejected. IF resolved, the .then part is executed. Otherwise, the .catch part is executed.

### Exceptions with Async and Await

```js
function doSomething(){
    // console.log("I am from doSomething function")
    const data = fetch("localhost:300/api")
}

const someFunction = async () => {
    try{
        await doSomething();
    }catch(err) {
        throw new CustomError(err.message);
    }
}

someFunction();
```


# Node.js File System and  Path Modules
