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


