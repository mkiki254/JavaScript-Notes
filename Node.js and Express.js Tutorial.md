# Getting started with Node.js

### Introduction

* Node.js is an open source and cross-platform JavaScript runtime environment
* Node.js runs the V8 JavaScript engine, the core of Google Chrome, outside of the browser
* A node.js app runs in a single process, without creating a new thread for every request
* Node.js uses event driven, non blocking I/O model to handle concurrent requests with single thread

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

* Both Browser and Node.js use JavaScript as their programming language
* However, building apps that run in the browser is completely different thing from building a Node.js application
* Browser has access to the DOM and Web API while Node.js uses modules to provide access to the file system and OS
* Node.js support both the CommonJS require() and ES module systems import() while the browser implements ES modules standards
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
How to start a node.js project:
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

### Useful methods of the path module

```js
// Importing the path module
const path = require("path")
// Defining the file path
const filepath = "C:/Users/Charles/Documents/nodejs-tutorial/files/sample.txt"

// How to get directory name
console.log(path.dirname(filepath))

// Getting the root directory of the project
console.log(__dirname)

// How to get the base name
console.log(path.basename(filepath))

// Getting the name of the file we are currently working on
console.log(__filename)

// How to get the extension name
console.log(path.extname(filepath))
```

Using the join method:
```js
const path = require("path")
const filepath = "C:/Users/Charles/Documents/nodejs-tutorial/files/sample.txt"

const sampleFile = "sample.txt";
console.log(path.join(path.dirname(filepath), sampleFile))
```

### The file system module

```js
const fs = require("fs");
// lists all the methods of the fs module
console.log(fs)
```

```js
// Reading from a file -Asynchronously
fs.readFile(filepath, "utf-8", (err, data) => {
    if (err) throw new Error("Something went wrong!");
console.log(data);
})
// Outputs
// Peints the text in the file
```

```js
// Reading from a file -Synchronously
try{
    // the second way of finding the file path using dirname replaces using the full path
    const data = fs.readFileSync(path.join(__dirname, "files", "sample.txt"), "utf-8");
    console.log(data);
}catch (err){
    console.log(err);
}
```

```js
//  Using the fs promise
const fsPromise = require("fs").promises;
const fileReading = async() => {
    try{
        const data = await fsPromise.readFile(filepath, {encoding: "utf-8"})
        console.log("FS Promises: ", data);
    }catch(err){
        console.log(err)
    }
}
fileReading()
```

#### writing into a file

```js
const txtFile = path.join(__dirname, "files", "text.txt")
const content = "I love learning javascript programming"

// Writing into a file -Asynchronously
fs.writeFile(txtFile, content, (err) => {
    if (err) throw new Error("Something went wrong!");
console.log("Write operation completed successfully");

// Reading after writing on the file
fs.readFile(txtFile, "utf-8", (err, data) => {
    if (err) throw new Error(err);
    console.log(data)
	})
})
// Same approach to writeFileSync
```

If we want to do multiple operations like reading a file, writing a file, and appending a file, it will become very tedious because you will have a lot of callbacks. A better approach is to use fspromises.  Rewriting the code above with the fspromise:

```js
// A cleaner way is using fspromises
const txtFile = path.join(__dirname, "files", "text.txt")
const content = "I love learning javascript programming"

const fsPromise = require("fs").promises;
const writingInFile = async () => {
    try{
        await fsPromise.writeFile(txtFile, content);
        await fsPromise.appendFile(txtFile, "\nthis appending file")
        const data = await fsPromise.readFile(txtFile)
        console.log(data.toString())
    }catch(err){
        console.log(err)
    }
}

writingInFile()
```

```js
// Using the a+ flag to add smth at the end of the file
        await fsPromise.writeFile(txtFile, "\n its awesome", {
            flag: "a+",
        });
```

How to remain a file
```js
// To rename the file, first argument old name, second argument new name
        await fs.promises.rename(txtFile, path.join(__dirname, "files", "newtxt.txt"))
        const data = await fsPromise.readFile(path.join(__dirname, "files", "newtxt.txt"))
```


# Async vs Sync Programming

JavaScript is a synchronous single threaded language, but it can handle asynchronous tasks using callbacks, promises and async await.
Example of blocking code in a synchronous programming
```js
console.log("Start operation")

function sleep(milliseconds) {
    let startTime = new Date().getTime();
    console.log("Operation is running.")
    while (new Date().getTime() < startTime + milliseconds){
        console.log("In progress")
    }
    console.log("Operation is done!")
}

sleep(1000);

console.log("Do something else")

// Outputs
// Start operation
// Operation is running.
// 7383 In progress
// Operation is done!
// Do something else
```

In the above code, the Do something else console had to wait for the execution of the while loop to finish thus blocking the code execution.

### Converting the above synchronous code into asynchronous

```js
console.log("Start operation")

function sleep(milliseconds) {
    console.log("Operation is running.")
    // Using a setTimout function that gets executed asynchronously
    setTimeout(() => {
        console.log("Operation is done!")
    }, milliseconds)
}

sleep(1000);
console.log("Do something else")

// Outputs
// Start operation
// Operation is running.
// Do something else
// Operation is done!
```

However, in the asynchronous code above, the Do something else does not have to wait for the execution of the set Timeout function to finish, so it is executed and when the operation is done, the set Timeout function is also executed


# Callbacks and Callback hell

A callback function is a function which is passed as an argument into another function. The other function executes this callback function at a later point in time.
Callbacks by themselves are not asynchronous. Example:

```js
console.log("Task start");
function asyncTask(cb){
    console.log("Task running");
    cb();
}
asyncTask(() => console.log(name))
console.log("Task end");
const name = "Charles";

// When this code run it runs into an error
// Uncaught ReferenceError: Cannot access 'name' before initialization
// This shows that callbacks are synchronous in nature
```

So we have to make the callback function to be asynchronous
To do that, we can do things like setTimeout as shown below:

```js
console.log("Task start");
function asyncTask(cb){
    console.log("Task running");
    setTimeout(cb, 0);
}
asyncTask(() => console.log(name))
console.log("Task end");
const name = "Charles";
```

The callback function will then be taken out of the execution flow, when the complete js file has been compiled, then the callback function will be called.

Other ways include using promises and async await.

### Good ways of handling callback errors
We start by passing error as the first argument in the callback. It is called the error first callback
```js
function asyncTask(cb){
    setTimeout(() => {
        // If you have an error
        // cb("Error!");
        // If you dont have an error, the first argument will be null
        // The second argument will be your data
        cb(null, "This is the data from the Mkiki Server")
    }, 0);
}

asyncTask((err, data) => {
    if (err) {
        throw err;
    } else {
        console.log("data", data)
    }
})

// If cb("Error!"), it will print: Uncaught Error!
// if cb(null, "data"), it will print:
// data This is the data from the Mkiki Server
```

### Callback hell

Suppose we have these two functions:

```js
function asyncTask(cb){
    setTimeout(() => {      
        cb(null, "This is the data from the Mkiki Server")
    }, 0);
}

function makeAPICall(cb){
    setTimeout(() => {
        console.log("This is async task execution")
    }, 0)
}
```

The callback hell will occur callbacks are nested upon each other like this:
```js
makeAPICall(() => {
    makeAPICall(() => {
        asyncTask(() => {
            asyncTask(() => {
                asyncTask(() => {
                    asyncTask(() => {})
                })
            })
        })
    })
})
```

These nested callbacks are what is referred to as callback hell
It means that one need to remember the sequence in which all the callbacks closes
It is also very unreadable and hard to understand
We use promises or async await which have a better way of writing the code and making it simpler to understand

### Promises

In layman's language, A father promises to his son that he is going to gift him a car if he scores 90% in his academics.

There are two possible eventualities:

1. The father fulfils the promise to his son which is called resolve

2. The father fails to fulfil the promise. which is called reject or the fail

Similarly in JavaScript, we have promises which take two arguments, a resolve or a reject.

```js
// Simple form of a promise in JavaScript
const promise = new Promise((resolve, reject) => {
    console.log("Async task execution");
    if (true){
        resolve()
    }else{
        reject()
    }
})
```

To interact with the promise, we use promise.then() method which accepts 2 functions. the first for the promise being resolved and the second for the promise being rejected.

```js
promise.then(
    () => {console.log("Passed!")},
    () => {console.log("Failed!")}
)
```


We can also actually pass the values of the resolve method. Suppose we made an API call which gave us some data

```js
const promise = new Promise((resolve, reject) => {
    console.log("Async task execution");
    if (false){
        const person = {name: "Charles"}
        resolve(person)
    }else{
        const error = {errCode: "1001"}
        reject(error)
    }
})

promise.then(
    (val) => {console.log(val)},
    (err) => {console.log(err)}
)

// If true it will log: {name: 'Charles'}
// If false it will log: {errCode: '1001'}
```

We can also make a catch of an error. This can work only if we missed adding error function in the .then method

```js
promise.then(
    (val) => {console.log(val)},
    // (err) => {console.log(err)}
).catch(() => {console.log("Failed")})
```

We can also add .finally which will always be called when we interact with the promise

```js
promise.then(
    (val) => {console.log(val)},
).catch(() => {console.log("Failed")})
.finally(() => {
    console.log("Clean up")
})
```

If your promise throws an error, its going to call the reject method by default and be automatically catched. Example:
```js
const promise = new Promise((resolve, reject) => {
    console.log("Async task execution");
    throw "Err"
    ...
})

  

promise.then(
    (val) => {console.log(val)},
).catch((err) => {console.log(err)})
.finally(() => {
    console.log("Clean up")
})

// Output 
// Async task execution
// Err
// Clean up
```

###  Interacting with promise that is already resolved

Even though the promise is resolved, we can still interact with it using the then handler. We cannot do the same with the callback function.
Once the callback function is executed, we cannot attach anything to it and cannot interact with it.
That's where the promises have advantage over the callback functions. Example:

```js
let p = Promise.resolve("Execution is done");
p.then((val) => {console.log(val)})

// Outputs
// Execution is done
```


###  Promises are by default asynchronous

Remember this example of the callback function being synchronous and how it threw an error of Uncaught ReferenceError: Cannot access 'name' before initialization:

```js
function asyncTask(cb) {
    cb();
}
asyncTask(() => console.log(name))
const name = "Charles"
```

The equivalent  Promise will look like this:
```js
function asyncTask() {
    return Promise.resolve();
}

asyncTask().then(() => {console.log(name)})
const name = "Charles"
```

The code will execute without error showing that Promises are asynchronous in nature.

### Chaining in Promises

Previously, we saw in the callback function that when we have to do, the logical sequence, one after the other, we result into the nesting of callback functions which give us the callback hell.
So lets see how we do the chaining in promises:

```js
const p = Promise.resolve("done")
// const p = Promise.reject("Failed")

p.then((val) => {
    console.log(val);
    return "done2"
}).then((val) => {
    console.log(val)
    return "done3"
}).then((val) => {
    console.log(val)
}).catch((val) => {console.log(val)})

// When promise is resolved and every .then returns something, the output is:
// done 1
// done 2
// done 3

// Supposing done3 is not returned, then the output is:
// done 1
// done 2
// undefined

// If the promise is already rejected, the output will be: Failed
```

When we use chaining in promises, every then has to return something, so that the other then handle will be accepted.
For instance, when we return done2, it will be accepted  as argument of the next then function.
If you dont return anything from the then method, then your chain will get broken.

Suppose that there is a case we get an error, unlike the callbacks where we have the error first callbacks, we dont have to write the error method in each of the then method. We can write the .catch after the last .then.
This is the advantage since the code will be more readable and understandable by the developers compared to the one in the callback hell

### Promise.all

There is a scenario where we want to make multiple API calls and all those API calls should call simultenously. We should not have where one API call get executed, then the second one, and so on.
How can we do that? Example:

```js
// function assumes after making an API call, results get back after some time
const makeApiCall = (time) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("This API executed in: " + time)
        }, time)
    })
}
```

We save all the API calls we want to make in an array

```js
let multiApiCall = [makeApiCall(1000), makeApiCall(2000), makeApiCall(500)]
```

Then use promise.all

```js
Promise.all(multiApiCall).then((values) => {
    console.log(values)
})

// Outputs
// ['This API executed in: 1000', 'This API executed in: 2000', 'This API executed in: 500']
```

This enables us to interact with all the promises, only once the execution of the API is done.
These API calls in the array were executed simultenously and didn't wait for one to finish for the other to execute. 

We can use the promise.race to see which was the first promise to be resolved:

```js
Promise.race(multiApiCall).then((value) => {
    console.log(value)
})

// When this code runs, it outputs:
// This API executed in: 500
// It makes sense because 500 milliseconds is the shortest amount of time
```


### Async and Await

Consider the following code using Promises to handle user login

```js
const userLogin = () => {
    console.log("Enter Username and Password");
    let username = prompt("Enter username: ");
    let password = prompt("Enter password: ");

    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log("Performing user authentication");
            if (username === "charles" && password === "kariuki"){
                resolve("User Authenticated!");
            }else{
                reject("Authentication Failed!");
            }
        }, 1000)
    })
}

function goToHomePage(userAuthStatus){
    return Promise.resolve(`Go to HomePage as: ${userAuthStatus}`)
}
```

 The user login function prompts for username and password and returns a promise. The promise contains a setTimeout function just executed after a 1000 milliseconds, which checks whether the username and the password matches. If they match, the promise is resolved If it fails the promise gets rejected

Calling the userLogin Function
```js
userLogin().then((response) => {
    console.log("Validated User")
    return goToHomePage(response)
}).then((userAuthStatus) => {
    console.log(userAuthStatus)
}).catch((err) => {
    console.log(err)
})

// If user enters the correct details, this is logged:
// Enter Username and Password
// Performing user authentication
// Validated User
// Go to HomePage as: User Authenticated!

// If user enters the wrong details, this is logged:
// Enter Username and Password
// Performing user authentication
// Authentication Failed!
```


Async Await provides a more concise and readable approach to achieve the same thing

When using async await, we need to wrap the async execution into the function

```js
async function performTask() {
    const response = await userLogin();
    console.log("Validated User")
    const userAuthStatus = await goToHomePage(response)
    console.log(userAuthStatus)
}

performTask()

// If user enters the correct details, the output is the same as above
// But the syntax is more concise and more readable compared to the 
// userLogin function being called above
// If we enter the wrong details, the execution gets into an uncaught error showing authentication failed
```

To handle the uncaught error in the async await, we can wrap the code with a try catch. We can add all our execution code in the try block. In the catch we can simply add an error and log it. Like this:

```js
  

async function performTask() {
    try {
        const response = await userLogin();
        console.log("Validated User")
        const userAuthStatus = await goToHomePage(response)
        console.log(userAuthStatus)
    }catch(err){
        console.log(err)
    }
}

performTask()

// If user enters the wrong details, the code will not break due to errors, instead it will log:
// Enter Username and Password
// Performing user authentication
// Authentication Failed!
```



Do you remember Promise.all where we did this example:

```js
const makeApiCall = (time) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("This API executed in: " + time);
        }, time)
    })
}

const apiRequests = [makeApiCall(1000), makeApiCall(2000), makeApiCall(500)]

Promise.all(apiRequests).then((values) => {
    console.log(values)
})
```

These requests are performed simultenously where one API request does not have to wait for another to finish executing
The equivalent async await will look like this:

```js
const makeApiCall = (time) => {
    // We need to return a function instead of a promise
    return () =>
    new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("This API executed in: " + time);
        }, time)
    })
}

const apiRequests = [makeApiCall(1000), makeApiCall(2000), makeApiCall(500)]
// We use an anonymous self executing function. Like this:
(async function() {
    for(let request of apiRequests) {
        console.log(await request())
    }
})()
```

These requests will be performed one after the other.
Thus, when we use async await, there are some drawbacks.
Replacing promises with async await will make you have good readable code but decrease the performance of the application.
So the secret is to balance between using the two

# Nodejs - Build Rest API CRUD PROJECT

### Restful Api Convection

<u>CRUD Actions</u>                               <u>HTTP Methods </u>                       <u> Endpoints</u>

Get all movies                                GET                                         /api/movies

Get movie                                       GET                                        /api/movies/:id

Create movie                                  POST                                       /api/movies

Update movie                                 PUT                                         /api/movies/:id

Delete movie                                   DELETE                                   /api/movies/:id


In this project, we are not going to use any of the framework or the library or the middleware. We are going to build it with pure Nodejs. The only packages we are going to use are nodemon and dotenv.


# Getting Started with Express Framework

## Express.js 
* It is a popular node.js web application framework which provides robust set of features for building web and mobile applications.
* It provides a thin layer of fundamental web application built on top of Nodejs features

## Features offered by Express JS

* Faster server-side application development
* Provides different middleware functions that have access to the request and the response object and a next callback which is a middleware function in the application of a request response cycle

```js
var express = require('express');
var app = express();

app.get('/', function(req, res, next) {
	next();
})

app.listen(3000);
```

* The middleware function also helps do the chaining of the routing. ie having one route that you redirect to another one
* Routing - refers to how application endpoints url respond to the client request
* Templating engine - Enables us to use the static template files in our application. At runtime, each template engine replaces the variables in a template file with the actual values and transforms the template into a html file that can be sent to the client. The client can see it on the browser
* Debugging - Express uses debug module internally to log the information about the route matches, middleware functions that we use in the application mode, and the flow of the request response cycle.


### Getting Started with Express in Coding
* To install express in our node application, we do: `npm i express` 
* We can create the simplest express app using a single file that is index.js or a full project using the express generator to create a sample project

#### Creating simplest express app using a single file
Example
```js
const express = require('express');
const app = express();

const port = 3001;

// Setting the first route
app.get("/", (req, res) => {
    // res.send("Hello Charles");
    // Sending response as a Json
    res.json({ message: "Hello World" })
})

app.listen(port, () => {
    console.log(`Example app listening on port ${port}`);
})

// When we search "localhost:3001" on browser or thunderclient, we get:
// The browser or thunderclient displays: {"message":"Hello World"}
```


#### Adding some routes to the simple express app
* To do some basic routing, you have the app, then provide the http method and provide the path the client should use as an endpoint and then provide the handler
* Example:

```js
app.get("/", (req, res) => {
    res.json({ message: "This is Home Page" });
})

app.get("/users", (req, res) => {
    res.json({ message: "Get all the users" });
})

app.get("/users/:id", (req, res) => {
    res.json({ message: `Get user with ID: ${req.params.id}` });
})

app.post("/users", (req, res) => {
    res.json({ message: "Create new users" });
})

app.put("/users/:id", (req, res) => {
    res.json({ message: `Update user with ID: ${req.params.id}` });
})

app.delete("/users/:id", (req, res) => {
    res.json({ message: `Delete user with ID: ${req.params.id}` });
})
```


#### Using the express generator

* Creates a full project of the express with template views and template engine
* To create a project we write on the terminal `npx express-generator project-name`
* If the generator fails to work because npm folder is missing in the App Data, you have to create it and set it to be used for global configurations and packages by running following command on terminal, `npm config set prefix c:\...\AppData\Roaming\npm`
* Then we enter inside the project-name folder and make an npm install
* To run the project, we use the command, `DEBUG=express-app:* npm start`
* If it fails to run in windows, we can alternatively run it this way: `$env:DEBUG="express-app:*"; npm start`
* Express can develop a fullstack web application


# Understanding Express Middleware and Types


