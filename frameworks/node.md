# Node

## Nodejs

Node.js is a runtime environment and Express.js is a framework built on Node. These frameworks are used to _**execute Javascript code**_ on the server-side and to _**build fast and scalable server applications.**_

[Download Node](https://nodejs.org/en/download/), (check with 'node --version' in terminal)

To set up Express, create a Node project with:

```
# check is node is installed
node --version

# make node project
mkdir my-node-express-app
cd my-node-express-app
npm init

# install express.js (in the node project my-node-express-app)
npm install --save express
```

* Name: name of node.js project
* Version: start with 1.0.0 and go up with [semantic versioning](https://semver.org/)
* Main: name of the file that will be loaded when your module is required by another app. (The default name is index.js, but since we're using express, name the file app.js as the entry point to our application; it's kinda standard for express apps) (you still have to create the file)

***

#### Executing Node

Node.js files must be initiated in the command line (terminal).

```
node filename.js
```

***

#### Global Objects

Node.js global objects are global in nature and they are available in all modules.

We do not need to _include_ these objects in our application, rather we can use them _directly_

These objects are modules, functions, strings and object itself as explained below

*   _**process**_ - a global object that contains all the context you need about the current program being executed. Things from env vars, to what machine you're on. This object has many _events_, _methods_, and _useful variables_. See here for [references](https://www.tutorialspoint.com/nodejs/nodejs\_process.htm)

    ```js
    console.log(process.execPath);    // Getting executable path.
    console.log(process.platform);    // Platform Information.
    console.log(process.env.PORT);    // the current port the file's on.
    ```
*   _**\_\_filename**_ - global variable which represents the filename of the code being executed.

    ```js
    // (absolute path of this code file)
    // ie. /Users/dev/Documents/winter21/backend/my-node-express-app/app.js
    console.log(__filename)
    ```
*   _**\_\_dirname**_ - global variable which represents the name of the directory that the currently executing script resides in.

    ```js
    // ie. /Users/dev/Documents/winter21/backend/my-node-express-app
    console.log(__dirname)
    ```
*   _**setTimeout(cb, ms)**_ - global function which is used to run callback _cb_ after at least _ms_ milliseconds

    ```js
    function startPlay() {
       console.log( "180 HUT!");
    }

    // Now call above function after 2 seconds
    setTimeout(printHello, 2000);
    ```
* _**clearTimeout(t)**_ - global function is used to stop a timer that was previously created with setTimeout().
  *   Here **t** is the timer returned by the setTimeout() function.

      ```js
      function printHello() {
         console.log( "Hello, World!");
      }

      // Now call above function after 2 seconds
      var t = setTimeout(printHello, 2000);

      // Now clear the timer
      clearTimeout(t);
      ```
*   _**setInterval(cb, ms)**_ - global function is used to run callback cb repeatedly after at least ms milliseconds.

    ```js
    function printHello() {
       console.log( "Hello, World!");
    }

    // Now call above function after 2 seconds
    setInterval(printHello, 2000);
    ```

***

### Modules

* Node.js uses modules to to share your JavaScript with other JavaScript in your apps. No window or globals needed
* modules is the equivalent of JavaScript libraries- a set of functions you want to include in your app. [Built-in modules Reference](https://www.w3schools.com/nodejs/ref\_modules.asp)
* #### Include Modules
  *   To include a module, use the _**`require('moduleName')`**_ function.

      ```js
      const http = require('http');
      const express = require('express')
      ```
* #### Custom Modules
  * You can create your own modules and include them in apps.
  * You can either:
    1.  \[_**COMMONJS**_] Use the _**`exports.`**_ keyword with _**`require()`**_. (or you can do module.exports = {things you want to export} at the bottom of the utils file). Make sure 'type':'module; IS NOT in package.json (this sets it to ecma syntax)

        ```js
        // utils.js
        // only sayHi is exported
        const sayHi = function() { console.log('hi'); }
        const age = 18

        module.exports = {sayHi, age}

        // app.js
        const utils = require('./utils')
        utils.sayHi()
        console.log(utils.age)
        ```
    2.  _**\[ECMA]**_ Use the _**`export`**_ keyword with the _**`import`**_ keyword. For this, you must make sure the file you're importing from is .mjs (basically .js), and make sure you have ("type": "module",) in the package.json (from `npm init`)

        ```js
        // utils.mjs
        export const sayHi = function() { console.log('hi'); }
        export const age = 18

        // app.js
        import {sayHi, age} from './utils.mjs'
        sayHi()
        console.log(age)
        ```

        *   Usually if you only have to expose one bit of code, you should use the _**`default`**_ keyword. This allows you to import the module with whatever name you want: (still need the package.json thing from above ^)

            ```js
            // utils.mjs
            export default function() { console.log('hi'); }
            const secret = 18

            // app.js (no need for {})
            import whateverIWant from './utils.'
            whateverIWant() // 'hi'
            ```

***

### File System Module - 'fs'

*   allows you to work with the file system on your computer. It allows you to CRUD (create read update delete, and rename) operations on files.

    ```js
    const fs = require('fs');
    ```
* We'll be using ECMA practices as they make it simplest (so make sure the package.json has "type":"modules" and .mjs is used for any module files you import)

#### Reading Files

* To read a file, we'll use the _**`readFile`**_ method (assume a nfl.txt file in same dir).
* We have to use the `URL` global that takes a relative path and a base path and will create a URL object that is accepted by `readFile`
*   (Because we're using `.mjs` files, we don't have access to `__dirname` or `__filename` which is normally used with the `path` module to form an appropiate file path for fs.)

    ```js
    import { readFile } from 'fs/promises'

    let data = await readFile(new URL('./nfl.txt', import.meta.url), 'utf-8')
    ```

#### Writing to Files

* Writing a file is similar to reading a file, except you need some content to place in the file.
* If you pass a file path that doesn't exist, it will create the file and write to it.
*   If you pass a file path that does exist, it will overwrite it.

    ```js
    import { writeFile } from 'fs/promises'
    const newContent = 'You watch film too huh? Thats cool, watch this.';

    // write to nfl.txt
    await writeFile(new URL('./nfl.txt', import.meta.url), newContent)
    ```

***

### Error Handling

* The last thing you want is your entire server crashing because of an error. Node allows us to handle our errors how we see fit:

#### Process Exiting

*   When a exception is thrown in Node.js, the current process will exit with a code of `1`. This effectively errors out and stops your programing completely.

    You can manually do this with:

    ```js
    process.exit(1)
    ```

    Although you shouldn't. This is low level and offers no chance to catch or handle an exception to decide on what to do

#### Async Errors

*   When dealing with callbacks that are used for async operations, the standard pattern is:

    ```js
    fs.readFile(filePath, (err, data) => {
        // error could be null if there is no error
      if (err) {
        // handle error
      } else {
        // handle data
      }
    })
    ```

    For `async / await` you should use `try / catch`:

    ```js
    try {
      const result = await asyncAction()
    } catch (e) {
      // handle error
    }
    ```

#### Sync Errors

*   For sync errors, `try / catch` works just fine, just like with async await:

    ```js
    try {
      const result = syncAction()
    } catch (e) {
      // handle error
    }
    ```

#### Catch All

*   Finally, if you just can't catch those pesky errors for any reason. Maybe some lib is throwing them and you can't catch them. You can use:

    ```js
    process.on('uncaughtException', callback)
    ```

***

### Packages

### NPM

* Node Packet Manager hosts 1000s of free packages (like the custom module we made above). A package in node.js contains all the files you need for a module (modules like http, fs, url, or a custom one).
* **Init**
  * To consume a package, we must first turn our app into a package. We can do this with a simple file called `package.json` on the root of our app via: _**`npm init`**_
  * In package.json:
    * `"name"` - is the name of your package. Can be anything since we're local.
    * `"version"` - is the [Semantic Version Number](https://semver.org/) or semver
    * `"main"` - the main entry point into your package
    * `"scripts"` - object of custom scripts to be excuted with `npm` cli
* Call _**`npm init -y`**_ for the default values
* **Common Commands for NPM:**
  * `npm install <packageName>` - installs package(s) from remote registries or local sources
  * `npm test` - runs the `test` script in your package.json
  * `npm uninstall <packageName>` - will uninstall a give package
  * `npm info <packageName>` - provides info on a given package
  * note: add a -g flag for global installs (makes it available everywhere on your computer as opposed to nonglobal installs only existing in project folder where you called npm install )
*   **To download package(s) from** [**npm**](https://www.npmjs.com)**, use the terminal:**

    ```
    npm install package1 package2 package3 --save
    ```

    * The `--save` flag is to let NPM know to update the package.json's dependency field with all of these packages. We need this because we don't want to check in the downloaded packages into source code for many reason
      * This will create a folder named "node\_modules" where the package will be places. All future downloaded packages will be placed in this folder.
      * _**NOTE: YOU DON'T WANNA ADD NODE\_MODULES TO VERSION CONTROL (GIT) SO MAKE A .gitignore FILE AND INSIDE IT, ADD 'node\_modules'. SO NOW WHEN YOU GIT ADD -A, IT WILL SKIP OVER NODE\_MODULES CUZ ITS A MASSIVE FUCKING FILE.**_
      * _**WHEN ANY1 PULLS DOWN YOUR PROJECT FROM GITHUB, YOU DON'T NEED TO WORRY ABOUT NODE\_MODULES NOT BEING THERE AND YOUR PROJECT USING MODULES FROM IT; THE MODULES YOU USED ARE STORED IN package.json UNDER DEPENDENCIES. SO WHEN THEY RUN YOUR PROJECT, THEIR COMPUTER WILL CHECK package.json AND INSTALL THE REQUIRED DEPENDENCIES.**_
* **Using a Package**
  *   Once the package is installed, use it like how you would http, fs, or url:

      ```js
      const x = require('packageName');
      ```

Misc: Running npm scripts

* You can add custom scripts to the package.json file. The scripts could be used to build the package, start a development environment or create a local web server.
*   For instance, call 'npm test' for the script:

    `"test" : "echo \"Error: no test specified\" && exit 1"`
*   You can make your own custom scripts by doing:

    ```json
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "hi": "echo \"hi\""
      },

    // then in terminal to run this 'hi' script:
    // in general: npm run <scriptName like test or hi>
    npm run hi // echo's "hi"
    ```

***

### CLI

A _**C**_ommand _**L**_ine _**I**_nterface is a program designed to start and complete one off tasks. Like git or npm.

Node.js is a perfect runtime to create a CLI that will run on any machine that has Node.js isntalled.

_**`~ Reddit CLI`**_

* For this exercise, we'll create a CLI that opens a random reddit post in our browser. To start, we'll create a new folder and make it a package with npm init

#### Creating a CLI

* Creating a CLI in Node.js just takes a extra step or two because they are really just an ordinary Node.js app wrapped behind a bin command.

1. Create a file reddit.mjs (main file of CLI). At the top of the file, make sure there's a _hashbang_ (#! /path) where the /path is the path of node on your computer which you can retrieve by calling _`which node`_ in the terminal. It's needed to tell the machine where the interpreter is located that is needed to execute this file. For us, that will be Node.js.
   * \[Usually, its the same for everyone] _**`#! /usr/local/bin/node`**_
2.  Next we need to tell Node.js what the name of our CLI is so when can actually use it in our terminal. Just have to add a section to our package.json:

    ```json
    "bin": {
      "reddit": "./reddit.mjs"
    }
    ```
3.  Once installed, this package will have it's bin command installed into your machine's _bin folder_ allowing us to use the _**`reddit`**_ command. We must install our own package locally so we can test out the CLI. We can simply install with no args which tells npm to install the current directory (reddit project directory)

    ```
    npm install -g
    ```

    You should now be able to run `reddit` and see your log print.

#### Install Dependencies

1.  For this CLI, we want to be able to _**1) hit the Reddit API**_, _**2) process that info**_, then _**3) open up a random post from the API in our browser**_. So install some packages from npm which already do these things.

    ```
    npm install node-fetch open yargs --save
    ```

    * `node-fetch` - is a fetch client that we can use to _**1) hit the reddit API**_
    * `open` - will open _**3) our browser with a URL**_
    * `yargs` - will allow us to process any flags or arguments passed to the CLI
2.  So now in the reddit.mjs:

    ```js
    #! /usr/local/bin/node
    // reddit.mjs

    // import the modules installed in step 4. (ECMA syntax)
    import fetch from "node-fetch"
    import open from 'open'
    import yargs from 'yargs'
    ```
3.  Process any flags or arguments passed to the CLI call using `yargs`:

    ie. 'reddit --username=devp3 --age=18' -t

    * where _username_ and _age_ are '**arguments**' and _t_ is a '**flag**'
    * This will cause argv = { \_: \[ '/usr/local/bin/node', '/usr/local/bin/reddit' ], username: 'dev.p3', age: 18, t: true, '$0': 'reddit' }

    ```js
    // So now you can access the flags and arguments passed
    const { argv } = yargs(process.argv)
    ```
4.  Now you want to make an API call to the _**front page of reddit json**_ (on https://www.reddit.com/.json):

    ```js
    // get the response object and convert it to json
    const res = await fetch('https://www.reddit.com/.json')
    const data = await res.json()
    ```
5.  Process response json and get a random post.

    * 'children' is an array in the json, where each element is an object about a reddit post.
    * Then generate a random number between 0 - #redditPosts (data.data.children.length).
    * This will be the index of the reddit post we access in the children array.

    ```js
    const randomIndex = Math.floor(Math.random() * data.data.children.length)
    const randomPost = data.data.children[randomIndex]
    ```
6.  log to terminal if --print flag is passed in the CLI call, otherwise, use the open() to open the url in a browser.

    ```js
    if (argv.print) {
      console.log(`
        Title: ${randomPost.data.title}\n
        Link: ${randomPost.data.permalink}
      `)
    } else {
      // open in browser if not
      open(`${randomPost.data.url}`)
    }
    ```

***

### Server

Node.js has access to OS level functionality, like networking tools. This allows us to build very capable servers.

Mixed with the fact that Node.js is single threaded and runs an even loop for async tasks, Node.js is widely used for API's that need to respond fast and don't require heavy CPU intensive work.

**HTTP MODULE (HARD WAY)**

*   Compared to other node stuff, the `http module` is very low level; there's very little reason to choose this module over Express. But just for the sake of covering it, below is an example server using the http module:

    ```js
    import http from 'http'
    const port = 8000

    const server = http.createServer((req, res) => {
      if (req.method === 'POST') {
        // if a JSON is sent up to server, it's sent as a buffer (stream of bits of data)
        let body = ''

        // convert stream of chunks of buffer data to string and append to total data
        req.on('data', chunk => {
          body += chunk.toString()
        })

        // when no more data left, log the data sent, write a status code, and send an 'ok' msg & end.
        req.on('end', () => {
          if (req.headers['content-type'] === 'application/json') {
            body = JSON.parse(body)
          }
          console.log(body)
          res.writeHead(201)
          res.end('ok')
        })

      // if you didn't POST; just a regular GET. write the status code, and send a 'hello' msg & end
      } else {
        res.writeHead(200)
        res.end('hello from my server')
      }

    })

    // listen on port PORT=(8000) specified above
    server.listen(port, host, () => {
      console.log(`Server is running on http://localhost:${port}`)
    })
    ```

**EXPRESS (EASY WAY)**

*   Express makes creating servers in Node.js a breeze. For this example, we're going to use 3 total modules:

    ```
    npm install express body-parser morgan --save
    ```

    * `express` - a framework (node module) for building servers.
    * `body-parser` - a middleware that parses incoming requests.
    * `morgan` - a middleware for logging incoming requests.
*   A simple to-do app with Express:

    ```js
    // server.mjs
    import express from 'express'
    import morgan from 'morgan'
    import bp from 'body-parser'

    const { urlencoded, json } = bp

    const db = {
      todos: [],
    }

    const app = express()

    // parses the query string for us
    app.use(urlencoded({ extended: true }))
    app.use(json())
    app.use(morgan('dev'))

    app.get('/todo', (req, res) => {
      res.json({ data: db.todos })
    })

    app.post('/todo', (req, res) => {
      const newTodo = { complete: false, id: Date.now(), text: req.body.text }
      db.todos.push(newTodo)

      res.json({ data: newTodo })
    })

    app.listen(8000, () => {
      console.log('Server on http://localhost:8000')
    })
    ```

    This to-do server has 2 routes:

    1. `GET /todo` - get all todos
    2. `POST /todo` - create a new todo

    To test this, have 2 servers open: one will run the server with nodemon, and the other will use HTTPie to send GET and POST requests on the /todo routes for GET and POST, respectively.
*   Every time you make a GET/POST request on terminal 2 with HTTPie, the morgan module will console.log a neat message denoting ie. `POST /todo 200 2.936 ms - 72`.

    ```
    # terminal 1
    nodemon server.mjs
    ```

    ```
    # terminal 2
    http :8000/todo # shows the current state of the API
    # adds to db array of to do things
    http POST :8000/todo text='sleep more'
    http POST :8000/todo text='code more'
    http POST :8000/todo text='work out more'
    http :8000/todo # shows the updated state of the API (with 3 things in it)
    ```

***

### HTTPie

* A simple yet powerful command-line HTTP and API testing client.
* Install with: _**`brew install httpie`**_

#### Basic Commands:

*   _**GET**_ - At its simplest, HTTPie can be passed a URL to immediately make a `GET` request (`http <url>`):

    ```js
    http example.com/a/b
    ```
*   _**POST**_ - To send data, specify the appropriate HTTP verb and then pass your key/value pairs as additional command-line parameters (`http POST <url> key=value key=value`):

    ```js
    http POST example.com foo=bar hello=world
    /* This essentially sends:
    {
        foo: bar,
        hello: world
    }
    and it's the same as ----------> http://example.com?foo=bar&hello=world
    */
    ```

#### Working with Files

*   You can upload and download files using standard shell redirects:

    ```js
    http GET example.com/download.pdf > ~/download.pdf
    http POST example.com/upload < ~/example.pdf
    ```

#### Sessions

* HTTPie has built-in support for persistent sessions. These allow you to reuse request components, such as HTTP headers and cookies, between requests made to the same host.
*   You create and use sessions by setting the `--session` parameter. As its value, specify the path to a file which will be used to store your new session.

    ```js
    http --session=./my-session.json GET example.com Authorization:foobar
    ```
* Data which is supported by sessions, such as the `Authorization` header in the above request, will now be saved into the file. On subsequent requests, you may now omit the `Authorization`header – it’ll be included automatically as it’s defined in your session
* Instead of specifying a session file, you may also use a simple name (`--session=example`). In this case, HTTPie will automatically save the session to an internally managed file. Each session is tied to the host it originates from, so `http --session=example example1.com` and `http --session=example example2.com` will exist independently of each other

***

### Testing

* One of the most common usecases for Node.js is writing test for Node.js and Frontend apps. Because Node.js can run outside the browser, it's perfect for CI environments and testing automations.

#### Basic Unit Testing

* Unit test will test little chunks of your code in isolation to ensure they behave has intended.
* Node.js ships with the _**`assert`**_ module which gives us many utilities to create _expectations_ of our code. When those expectations aren't met, assert will _throw an error_ telling us why. This is perfect for testing!

```js
// myLib.mjs
export const add = (num1, num2) => num1 * num2
```

```js
// test.mjs
import assert from 'assert'
import { add } from './myLib.mjs'    // import the function to be tested

try {
  console.log('add() should add two numbers ')
  // assert.strictEqual(a, b) throws and error if a ≠ b. In this case, if add(2, 5) ≠ 7
  assert.strictEqual(add(2, 5), 7)
  console.log('  ✅ passed')
} catch (err) {
  console.log('  🚫 fail')
  console.error(err)
}
```

* Run the test.mjs file with: _**`node test.mjs`**_
*   You should get an output that describes how this assertion fails. Because our add function actully multiplies two numbers and instead of adding them. So either our tests is off or the code is wrong. Let's say the code is wrong, so lets fix that and run the test again and we should see that it passes now.

    Assert is great but there are some amazing tools and libs built around it that make writing and reading tests satisfying. One of those tools that the comminity has adopted is called _**`jest`**_.

***

### Deployment

#### Packages

* For CLI's, Libraries, Plugins, etc, you would publish these to NPM so othere devs can install it. The NPM CLI makes this easy.

1. First thing is to make sure you have a _**unique package name**_ in the _**"name"**_ field of _`package.json`_. NPM will let you know when you try to publish.
2. Next, _**create a NPM account**_.
3. Once you've done that, you need to login to NPM from your terminal with: _**`npm login`**_
4. And now to publish a package, simply run: _**`npm publish`**_

And that's it. Your CLI can now be installed with _**`npm install [name]`**_.

#### Servers

* For API's and background tasks that operation on API's or databases, you'd deploy these to a hosting provider like AWS, Heroku, Google Cloud, etc. See online for steps for these hosting providers.

***

## API DESIGN IN NODEjs

### API

* Applicatoin Programming Interface
* In the context of REST API, an API, is a server that creates an HTTP interface for interacting with some data.
* Basic data operations like create, retrieve, update, delete (CRUD).

### REST

* Most popular API design pattern, but it's very blurry.
* An API design that combines DB resources, route paths, and HTTP verbs (GET, POST, ...) to allow apps describe what action they're trying to perform.
* Works for basic data models (relational); hard to scale with complex models and client requirements (graph db)
* **RE**presentational **S**tate **T**ransfer is a method of implementing a web service.
* It's the ideology that everythign is a resource, and all resources are identified by a **URI (uniform resource indicator)**.
* REST is stateless; so when you interact with a REST webservice to get some data, you will recieve only the most currrent state of the resource (recall React). So if you send two requests, the data received may be different for each request (state may have changed).
* Benefits of REST:
  * Flexibility (data isn't tied to resources or methods)
  * Scalable (can suppot large numbers of requests)
  * Reliable (no single point of failure)
  * Handles common data formats for APIs like JSON

**Node.js + Express for APIs**

* Express is the standard API framework for Node.js (albeit there are other ways)
* Handles all tedious tasks like managing sockets, route matching, error handling, and more.

**MongoDB**

* It's the go-to non-relational DB, works like a dream in Node
* Non-relational document store that is easy to get started and scales well.
* Tons of hosting solutions (Mlab, Atlas, Compass, and more)
* ORM (object relational mapper) and other libs are some of the best for any DB (called Mongoose)

***

### Insomnia

* Used for API development and testing; deskptop app GUI is very easy to use when you need to send HTTP Requests to a server.
* You can send JSON data in POST requests by pasting a JSON instead of key value pairs like in URL (postman does this).
* Side terminal logs what data is sent back (res.send()).
* Simplistically fucking beautiful to use.

***

### Nodemon

* allows you to refresh the node server to view any changes (live, kinda like live-server or watch-sass).
* To install:
  * `npm init` - creates package.json
  * `npm i nodemon --save-dev` - installs nodemon as a dependency
  *   /package.json/under "scripts"/ add:

      `"watch": "nodemon ./nodeFileName.js",`
  *   Then to run nodejs file with nodemon, in the terminal:

      `nodemon ./nodeFileName.js`
* **`Ctrl + C`** to kill the node server
* Open the server in the browser at `http://localhost:port#`, where port# is specified in the nodejs file with the _**`.listen(port#)`**_ (usually 8080).
