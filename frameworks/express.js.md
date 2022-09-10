# Express.js

## Installation

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

***

## Basic Routing

* API endpoint: a point at which an API connects with a software program.
* **Routing**: how an app responds to a client request to a particular _**endpoint**_, which is a _**URI (or path) and a specific HTTP request method**_
* The HTTP methods which are supported are, _**GET, POST, PUT, DELETE**_
*   Routes have the following structure:

    ```js
    app.METHOD(PATH, HANDLER)
    ```

    Where:

    ​ (_**app**_ is an instance of _**express**_; 'const app = express()'),

    ​ (_**METHOD**_ is an _**HTTP REQUEST METHOD**_),

    ​ (_**PATH**_ is a _**path on the server**_),

    ​ (_**HANDLER**_ is the _**callback function when the route is matched**_)

    ​ also called **Controller**
* Simple Routes for the Hello World App above:

```js
// Respond with 'Hello World!' on the homepage:
app.get('/', function (req, res) {
  res.send('Hello World!')
})

// Respond to POST request on the root route (/), the app’s home page:
app.post('/', function (req, res) {
  res.send('Got a POST request')
})

// Respond to a PUT request to the /user route:
app.put('/user', function (req, res) {
  res.send('Got a PUT request at /user')
})

// Respond to a DELETE request to the /user route:
app.delete('/user', function (req, res) {
  res.send('Got a DELETE request at /user')
})
```

***

## Serving Static Files

*   To serve static files such as images, CSS files, and JavaScript files, use the _`express.static`_ built-in middleware function in Express:

    ```js
    // formally,
    express.static(root, [options])
    // 'root': the root dir from which to serve static assets

    //  ie. to serve static files in a root dir named 'public'
    app.use(express.static('public'))
    ```

    Now, you can load the files that are in the `public` directory:

    ```
    http://localhost:3000/images/kitten.jpg
    http://localhost:3000/css/style.css
    http://localhost:3000/js/app.js
    http://localhost:3000/images/bg.png
    http://localhost:3000/hello.html
    ```

    To use multiple static assets directories, call the `express.static` middleware function multiple times:

    ```js
    // serve static files from 'static' and 'files' directories
    app.use(express.static('static'))
    app.use(express.static('files'))
    ```
*   If you run the express app from another directory, it’s safer to use the absolute path of the directory that you want to serve:

    ```js
    // same as above, but safer since it uses absolute path instead of relative.
    const path = require('path')
    app.use('/static', express.static(path.join(__dirname, 'public')))
    ```

***

## Routing In-Depth

* You define routing using methods of the Express `app` object that correspond to HTTP methods; for example, _`app.get()`_ to handle _**GET**_ requests and _`app.post`_ to handle _**POST**_ requests.
* You can also use [app.all()](https://expressjs.com/en/4x/api.html#app.all) to handle all HTTP methods and [app.use()](https://expressjs.com/en/4x/api.html#app.use) to specify middleware as the callback function.

### Route Methods

*   A route method is derived from one of the HTTP methods, and is attached to an instance of the `express` class (usually 'app'). Some basic routes:

    ```js
    // GET method route
    app.get('/', function (req, res) {
      res.send('GET request to the homepage')
    })

    // POST method route
    app.post('/', function (req, res) {
      res.send('POST request to the homepage')
    })
    ```
*   There is a special routing method, _`app.all()`_, used to load middleware functions at a path for _**all**_ HTTP request methods. Ie. the following handler is executed for requests to the route “/secret” for any HTTP verb:

    ```js
    app.all('/secret', function (req, res, next) {
      console.log('Accessing the secret section ...')
      next() // pass control to the next handler
    })
    ```

### Route Paths

*   Route paths, in combination with a request method, define the endpoints at which requests can be made. Query strings _**are not**_ part of the route path. Some route paths:

    ```js
    // This route path will match requests to the root route, /
    app.get('/', function (req, res) {
      res.send('root')
    })

    // This route path will match requests to /about
    app.get('/about', function (req, res) {
      res.send('about')
    })

    // This route path will match requests to /random.text
    app.get('/random.text', function (req, res) {
      res.send('random.text')
    })
    ```

### Route Parameters

* Route parameters are named URL segments that are used to capture the values specified at their position in the URL
*   The captured values are populated in the _**`req.params`**_ _object_, with the name of the route parameter specified in the path as their respective keys.

    ```
    ie.

    Route path:         /users/:userId/books/:bookId
    Request URL:         http://localhost:3000/users/34/books/8989
    req.params:         { "userId": "34", "bookId": "8989" }
    ```
*   To define routes with route parameters, simply specify the route parameters in the path of the route as shown below:

    ```js
    app.get('/users/:userId/books/:bookId', function (req, res) {
      res.send(req.params)
    })
    // ie. /users/123/books/456
    // req.params = { "userId": 123, "bookId": 456 }
    ```
*   Since the hyphen (`-`) and the dot (`.`) are interpreted literally, they can be used along with route parameters for useful purposes:

    ```
    using hyphen (-):
        Route path: /flights/:from-:to
        Request URL: http://localhost:3000/flights/LAX-SFO
        req.params: { "from": "LAX", "to": "SFO" }

    using dot (.):
        Route path: /plantae/:genus.:species
        Request URL: http://localhost:3000/plantae/Prunus.persica
        req.params: { "genus": "Prunus", "species": "persica" }
    ```

### Route Handlers

* Also called controllers, route handlers are the callback functions that behave like _middleware_ to handle a request. Route handlers can be in the form of a function, an array of functions, or combinations of both ([see here](https://expressjs.com/en/guide/routing.html)).
* Handlers usually have 3 parameters: a _**response object**_, a _**request object**_, and a _**next()**_.

#### Response Methods

* The methods on the response object (`res`) in the following table can send a response to the client, and terminate the request-response cycle.
*   If none of these methods are called from a route handler, the client request will be left hanging

    | Method                                                                  | Description                                                                                                                                                                                                                                                              |
    | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
    | [res.download()](https://expressjs.com/en/4x/api.html#res.download)     | <p>Prompt a file to be downloaded.<br><em><strong>res.download('/report-12345.pdf')</strong></em></p>                                                                                                                                                                    |
    | [res.end()](https://expressjs.com/en/4x/api.html#res.end)               | <p>End the response process.<br><em><strong>res.end()</strong></em><br><em><strong>res.status(404).end()</strong></em></p>                                                                                                                                               |
    | [res.json()](https://expressjs.com/en/4x/api.html#res.json)             | <p>Send a JSON response.<br><em><strong>res.json({ user: 'tobi' })</strong></em><br><em><strong>res.status(500).json({ error: 'message' })</strong></em></p>                                                                                                             |
    | [res.redirect()](https://expressjs.com/en/4x/api.html#res.redirect)     | <p>Redirect a request.<br><em><strong>res.redirect('http://example.com')</strong></em><br>r<em><strong>es.redirect(301, 'http://example.com')</strong></em></p>                                                                                                          |
    | [res.render()](https://expressjs.com/en/4x/api.html#res.render)         | Render a view template.                                                                                                                                                                                                                                                  |
    | [res.send()](https://expressjs.com/en/4x/api.html#res.send)             | <p>Send a response of various types.<br>(When parameter is <code>String</code>, the method sets the <code>Content-Type</code> to “text/html”)<br>(When the parameter is an <code>Array</code> or <code>Object</code>, Express responds with the JSON representation)</p> |
    | [res.sendStatus()](https://expressjs.com/en/4x/api.html#res.sendStatus) | <p>Set the response status code and send its string representation as the response body.<br><em><strong>res.sendStatus(404)</strong></em></p>                                                                                                                            |
    | [res.set()](https://expressjs.com/en/4x/api.html#res.set)               | <p>Sets the response’s HTTP header <code>field</code> to <code>a given value</code>.<br><em><strong>res.set('Content-Type', 'text/plain')</strong></em></p>                                                                                                              |
*   _**app.route()**_ - used to create chainable route handlers for a given route path. Organizes the code with the routes:

    ```js
    app.route('/book')
        // GET request
      .get(function (req, res) {
        res.send('Get a random book')
      })

    // POST request
      .post(function (req, res) {
        res.send('Add a book')
      })

        // PUT request
      .put(function (req, res) {
        res.send('Update the book')
      })
    ```

#### express.Router (SUB ROUTING)

* Use the `express.Router` class to create modular, **mountable** route handlers
* A `Router` instance is a complete middleware and routing system; referred as a “mini-app”
* This helps with abstraction and organizing code.
*   The following example creates a router as a module, loads a middleware function in it, defines some routes, and mounts the router module on a path in the main app:

    ```js
    // name.js (can be done in main file app.js, but it helps organize) router file

    // create Router instance
    const express = require('express')
    const router = express.Router()

    // middleware that is specific to this router
    router.use(function timeLog (req, res, next) {
      console.log('Time: ', Date.now())
      next()
    })

    router
            // define the root route for mini app
            .get('/', function (req, res) {
              res.send('Hello')
            })
            // define the /name route for mini app
            .get('/name', function (req, res) {
              res.send('James Bond')
            })

    // export this sub route
    module.exports = router
    ```

    You would load ('_mount_') the sub route onto the main app much like you load a middleware: with the app.use function. But now, you pass in the route to load it onto, then pass the subroute.

    ```js
    // Then in app.js, import and load the sub router module from name.js
    var birds = require('./name')
    ...
    app.use('/api', birds)

    // The main app will now be able to handle requests to /api/name, as well as call the timeLog middleware function that is specific to the route.
    ```

***

## CRUD

*   Create-Read-Update-Delete operations work perfectly with REST since there's a one-to-one correspondence with the HTTP verbs and CRUD:

    **\[C]reate = app.post()**

    **\[R]ead = app.get()**

    **\[U]pdate = app.put()**

    **\[D]elete = app.delete()**

(.post and .put only differ in their intentions; both post data, but .put expects to cause an update not a creation)

***

## Route Order

*   If you have 2 endpoints/routes with the same verb, the one higher up will be executed since Node is top-down execution.

    ```js
    // both are GET on the '/' route
    // the higher up one will run (so {data: 1} will be sent)
    app.get('/' (req, res) => {
      res.send({ data: 1})
    })

    app.get('/' (req, res) => {
      res.send({ data: 2})
    })
    ```

***

## Sub Routing

* You can have branches of routes (sub routes)

***

## Middleware

* _Middleware_ functions are functions that have access to the [request object](https://expressjs.com/en/4x/api.html#req) (`req`), the [response object](https://expressjs.com/en/4x/api.html#res) (`res`), and the `next` function in the application’s request-response cycle.
* The `next` function is a function in the Express router which, when invoked, executes the middleware succeeding the current middleware.
* Middleware functions can perform the following tasks
  * Execute any code, Make changes to the req\&res objects, End the request-response cycle, Call the next middleware in the stack.

**If the current middleware function does not end the request-response cycle, it must call `next()` to pass control to the next middleware function. Otherwise, the request will be left hanging**

*   ie. a middleware function called _myLogger_ simply prints “hi” on GET requests:

    ```js
    const express = require('express')
    const app = express()

    // MIDDLEWARE FUNCTION
    var requestTime = function (req, res, next) {
      // changes the request object for the entire app
      req.requestTime = Date.now()
      next()
    }

    // load the middleware function
    app.use(requestTime)

    app.get('/', function (req, res) {
      var responseText = 'Hello World!<br>'
      responseText += '<small>Requested at: ' + req.requestTime + '</small>'
      res.send(responseText)
    })

    app.listen(3000)
    ```

There are many useful third party middlewares you can download namely body-parser.

***

## Template (View) Engines with Express

A _template engine_ enables you to use static template files in your application.

At runtime, the template engine replaces variables in a template file with actual values, and transforms the template into an HTML file sent to the client. This approach makes it easier to design an HTML page.

Some popular template engines that work with Express are [Pug](https://pugjs.org/api/getting-started.html) (formerly known as _Jade_), [Mustache](https://www.npmjs.com/package/mustache), and [EJS](https://www.npmjs.com/package/ejs).

* _**`res.render('filename')`**_ - used to render (ie. upload an html file) to the client side. This function assumes a Model-View-Controller Structure (MCV) project structure, so when you call res.render('index'), it will look inside a _**views**_ folder for a filename of 'index' (index.html; don't include file extension in function call). So now, you can render different HTML pages for different routes using this method.

To use EJS:

1. install ejs: _**`npm i ejs --save`**_
2. create a folder named '_**views**_' with file you want to render (ie. nfl.ejs); the _**file extension must be .ejs**_ (it's still HTML but with a little programming language in it- kinda like jsx)
3. app.set('view engine', 'ejs')
4. _**res.render('nfl')**_

```
app.set('view engine', 'ejs')

app.get('/', (req, res) => {
        res.render('nfl')
    res.end()
})
```

!\[Screen Shot 2021-12-12 at 9.24.33 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2021-12-12 at 9.24.33 PM.png)

***

## Middleware References

### > body-parser ( deprecated; now use -> express.json() )

* allows us to read the "body" of an incoming JSON object. But it's deprecated.
*   Now, we can simply use _**`express.json()`**_:

    ```js
    const express = require('express');
    const app = express();

    app.use(express.urlencoded()); // Parse URL-encoded bodies
    app.use(express.json());
    ```

### > cors

* CORS stands for _**`Cross-Origin Resource Sharing`**_. It allows us to relax the security applied to an API. This is done by bypassing the _**`Access-Control-Allow-Origin`**_ headers, which specify which _`origins`_ can access the API.
*   The three parts that form an [origin](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Origin) are protocol, domain, and port. (http \[protocol] localhost \[domain] :3000 \[port]). There are servers that host APIs and ensure that info is delivered to websites and other end points. Therefore, making _**cross-origin**_ calls. [read more here](https://www.section.io/engineering-education/how-to-use-cors-in-nodejs-with-express/).

    ```
    npm install cors --save
    ```

    ```js
    // Simple Usage (Enable All CORS Requests)

    var express = require('express')
    var cors = require('cors')
    var app = express()

    app.use(cors())

    app.get('/products/:id', function (req, res, next) {
      res.json({msg: 'This is CORS-enabled for all origins!'})
    })

    app.listen(80, function () {
      console.log('CORS-enabled web server listening on port 80')
    })
    ```

    ```js
    // Enable CORS for a Single Route

    var express = require('express')
    var cors = require('cors')
    var app = express()

    app.get('/products/:id', cors(), function (req, res, next) {
      res.json({msg: 'This is CORS-enabled for a Single Route'})
    })

    app.listen(80, function () {
      console.log('CORS-enabled web server listening on port 80')
    })
    ```

### > morgan

*   simplifies the task of logging HTTP requests and errors to and from your application.

    ```
    npm install morgan --save
    ```

    And now all you need in your app is (either 'dev' or 'tiny'):

    ```js
    // import the module
    const morgan = require('morgan')

    // load the middleware so now it will log all requests and errors.
    // JUST USE 'dev' (EASIEST)
    app.use(morgan('dev'))
    ```

    the 'dev' parameter can be swapped with 'combined', 'common', 'short', 'tiny'- each is a different format of the log:

    ```
    'combined' - Standard Apache combined log output.
        :remote-addr - :remote-user [:date[clf]] ":method :url HTTP/:http-version" :status :res[content-length] ":referrer" ":user-agent"

    'common' - Standard Apache common log output
        :remote-addr - :remote-user [:date[clf]] ":method :url HTTP/:http-version" :status :res[content-length]

    'dev' - Concise output colored by response status for dev. use
        :method :url :status :response-time ms - :res[content-length]

    'short' - Shorter than default, also including response time
        :remote-addr :remote-user :method :url HTTP/:http-version :status :res[content-length] - :response-time ms

    'tiny' - The minimal output
        :method :url :status :res[content-length] - :response-time ms
    ```
