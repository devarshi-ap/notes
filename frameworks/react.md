# React

React is a JavaScript library created by Facebook. It's a tool for building UI components.

React creates a virtual DOM in memory, where it does all the necessary manipulating, before making the changes in the browser DOM

## Setting up

* You can either use a temporary method or a production method of setting up a react environment.
  1.  Temporary: Use CDN's

      ```html
      <!--The first 2 let us write React code in javascripts, the 3rd lets us write JSX syntax and ES6 in older browsers.-->
      <script src="https://unpkg.com/react@16/umd/react.production.min.js"></script>

      <script src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>

      <script src="https://unpkg.com/babel-standalone@6.15.0/babel.min.js"></script>
      ```
  2.  Production: npm

      ```
      npm install -g create-react-app
      npx create-react-app <project_name>
      cd <project_name>
      npm start
      ```
  3. npm start will create a local server on _**localhost:3000**_.

***

## React Render HTML

* React's primary goal is to render HTML in a webpage. It accomplishes this by using a function called _**`ReactDOM.render(<HTML_CODE>, <HTML_ELEMENT_>)`**_.
*   It will display the specified HTML code inside the specified HTML element

    ```
    ReactDOM.render(<p>Hello</p>, document.getElementById('root'));

    // you can also use JSX variables as an argument for render():
    const myelement = <p>Hello</p>
    ReactDOM.render(myelement, document.getElementById('root'));
    ```

### The Root Node

* The root node is the HTML element where you want to display the result.
*   It does NOT have to be a _**`<div>`**_ element and it does NOT have to have the _**`id='root'`**_:

    ```jsx
    <body>
      <header id="whatever"></header>
    </body>

    ReactDOM.render(<p>Hi</p>, document.getElementById('whatever'));
    ```

***

## React JSX

* JSX stands for JavaScript XML.
* Allows us to write and add HTML in React without the need of _**`createElement()`**_ or _**`appendChild()`**_ methods.
*   JSX isn't required but it makes things a lot easier so just use it.

    ```js
    const myelement = <h1>This is JSX</h1>;
    ReactDOM.render(myelement, document.getElementById('root'));
    ```

### Comments

*   put comments inside JSX, with the `{/* */}` to wrap around the comment text:

    ```js
    const JSX = (
      <div>
        {/*comment here*/}
        <h1>Bazinga</h1>
      </div>
    );
    ```

### Self-Closing Tags

* almost all tags have both an opening and closing tag: `<div></div>`
* Self-closing tags are tags that don’t require both an opening and closing tag before another tag can start.
* ie. the line-break tag can be written as: _**`<br>`**_ or _**`<br />`**_ but _never_ _**`<br></br>`**_ since it doesn't have any content.
* In JSX, any element can be written with a self-closing tag, and every element must be closed. A, on the other hand, can be written as(but with this one, you can't include anything inside it) or

### Expressions in JSX

*   Use curly braces `{}` to write expressions inside (react variable, property, or any JavaScript expression). JSX will execute the expression and return the result:

    ```jsx
    const myelement = <h1>React is {5 + 5} times better with JSX</h1>;
    // React is 10 times better with JSX
    ```

### Large Blocks of HTML

*   If the HTML gets too long (multiline), put it inside parentheses `()`:

    ```jsx
    const myelement = (
      <ul>
        <li>Apples</li>
        <li>Bananas</li>
        <li>Cherries</li>
      </ul>
    );
    ```

### One Top Level Element

*   The HTML code must be wrapped in ONE top level element. (Ie. two

    ## 's must be inside something like a').
*   JSX will throw an error if the HTML is missing a parent element!

    ```jsx
    const myelement = (
      // must have a parent element, in this case, the div.
      <div>
        <h1>I am a Header.</h1>
        <h1>I am a Header too.</h1>
      </div>
    );
    ```

### class, now className

* since JSX is rendered as JavaScript, and the _**`class`**_ keyword is a reserved word in JavaScript, use attribute _**`className`**_ instead.
*   JSX translates className ---> class afterwards.

    ```js
    const myelement = <h1 className="myclass">Hello World</h1>;
    ```

### Ternary Expressions

* React supports `if` statements, but not _inside_ JSX. So you can either:
  1. Use an if-statment _outside_ JSX, or
  2.  Use a ternary expression _inside_ `{}` 's in the JSX:

      ```jsx
      const x = 5;
      const myelement = <h1>{(x) < 10 ? "True" : "False"}</h1>;
      ```

***

## React Components

* Components are like functions that return HTML elements.
* They are independant and reusable bits of code. They serve the same purpose as JavaScript functions, but work in isolation and return HTML via a render() function.
* There are two types of components:
  1. _**`Class Components`**_ (can be stateful/stateless if it internally uses `state`)
  2. _**`Stateless Functional Components`**_

### Class Components

* When creating a React component, the component's name must:
  1. Start with an _**upper case letter**_
  2. _**extends Component**_, _**imports Component from "react"**_
  3. Include a _**render()**_ method

```jsx
import { Component } from "react";

class Greet extends Component {
  render() {
    return (
      <div>
          <h1>Hello, {this.props.name}</h1>
      </div>
    )
  }
}

export default Greet
```

### Functional Components

*   A function is pretty much like a class component, but they don't require the extends or render() method:

    ```jsx
    export default function Greet(props) {
      return <h1>Hello, {props.name}</h1>;
    }

    // OR OR OR
    function Greet(props) {
      return <h1>Hello, {props.name}</h1>;
    }
    export default Greet;

    // OR OR OR ES6 arrow functions (multi-line ex.)
    const Greet = (props) => (
        <div>
            <h1>Hello, {props.name}</h1>
                <p>Have a nice day!</p>
        </div>
    )
    export default Greet;
    ```

### Component Constructor

* If there is a `constructor()` method in your component, this function will be called when the component gets initiated.
* It's used to initiate the component's properties.
* In React, component properties should be kept in an object called _**`state`**_.
*   Include the _**`super()`**_ statement in the constructor which executes the parent components' constructor(), and your component has access to all the functions of the parent component (React.Component)

    ```js
    class Car extends React.Component {
      constructor() {
        // call super()
        super();
        // add properties to 'state' object
        this.state = {color: "red"};
      }
      render() {
        // to use properties in the render(): this.state.<propertyName>
        return <h2> I am a {this.state.color} Car!</h2>;
      }
    }
    ```

### Props

* Short for properties, props are _**like JS function arguments**_, and you send them into the _**component as HTML attributes**_:
* to use prop in **functional component**: _**`props.<property>`**_
*   to use prop in **class component**: _**`this.props.<property>`**_

    ```jsx
    // functional component
    export default function Profile(props) {
        return <h1>Name: {props.firstname} {props.lastname}</h1>
    }

    // class component
    class Profile extends Component {
      render() {
        return <h2>Name {this.props.firstname} {this.props.lastname}</h2>;
      }
    }
    ```
*   #### Passing an array as a Prop

    To pass an array to a JSX element, it must be treated as JavaScript and wrapped in curly braces:

    ```jsx
    <Parent>
      <Child colors={["green", "blue", "red"]} />
    </Parent>

    // now to use the array prop in a component, arr methods ie. join():
    const List = (props) => {
      // green-blue-red
      return <p>{props.tasks.join('-')}</p>
    };
    ```
*   #### Default Props

    You can assign default props to a component as a property on the component itself and React assigns the default props if no value is provided. You can set default props by:

    ```js
    const ComponentName = (props) => {
      // Toronto and 416
      return <h1>{props.city} and {props.area}</h1>
    }

    // default props syntax
    ComponentName.defaultProps = {
      city: "Toronto",
      area: 416,
    }
    ```

    You can override the default values by just passing a value in the component call ie.
*   #### Passing Children HTML as Props

    * _**props.children**_ is a special property of React components which contains any child elements defined within the component.
    * The below example component contains an  that received some props and then displayed it with _**{props.children}**_

    ```jsx
    // Picture.js
    export default function Picture(props) {
      return (
        <div>
              <img src={props.src}/>
              {props.children}    {/*this is the same as: <p>Image Caption</p> */}
        </div>
      )
    }

    // App.js
    ...
    <Picture key={picture.id} src={picture.src}>
      {/*what is placed here is passed as props.children*/}
      <p>Image Caption</p>
    </Picture>
    ```

### Pass Data

*   Props are also how you pass data from one component to another, as parameters:

    ```
    // Send the "brand" property from the Garage comp. to the Car comp:
    class Car extends React.Component {
      render() {
        // Car received the prop from garage here
        return <h2>I am a {this.props.brand}!</h2>;
      }
    }

    class Garage extends React.Component {
      render() {
        return (
          <div>
            <h1>Who lives in my garage?</h1>
            {/*the prop is passed here to Car component*/}
            <Car brand="Ford" />
          </div>
        );
      }
    }

    ReactDOM.render(<Garage />, document.getElementById('root'));
    ```
*   If your sending a _**Variable/Object**_ instead of a string, just put the attribute-prop inside a curly brace `{}`:

    ```
    class Garage extends React.Component {
      render() {
        const carname = "Ford";
        // or: const carname = {name: "Ford", model: "Mustang"};
        return (
          <div>
            {/*Prop variable is inside {}'s*/}
            <Car brand={carname} />
          </div>
        );
      }
    }
    ```
*   If your component has a `constructor()`, the props should always be passed into it and also to the `super()` inside the constructor:

    ```
    class Car extends Component {
      constructor(props) {
        super(props);
      }
      render() {
        return <h2>I am a {this.props.model}!</h2>;
      }
    }
    ```

_**Note: React Props are read-only! You will get an error if you try to change their value.**_

### PropTypes

*   You can use the PropTypes import to verify components receive props of the correct type.

    _**`import PropTypes from 'prop-types';`**_
* This will throw a useful warning when the data is of any other type.
*   You define PropTypes the same way as default props:

    ```jsx
    // MyComponent.propTypes = { <target>: PropTypes.<type>.isRequired}

    // handleClick - checks for this prop
    // func - checks that prop handlClick is of this type
    // isRequired - tells React this prop is required for the component
    MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }
    ```
* _**Types**_: bool, null, undefined, number, bigint, string, symbol

### Components in Components

*   You can use one component inside another by referencing it's HTML-esque syntax:

    ```jsx
    class Car extends React.Component {
      render() {
        return <h2>I am a Car!</h2>;
      }
    }

    class Garage extends React.Component {
      render() {
        return (
          <div>
            <h1>Who lives in my Garage?</h1>
            <Car />           {/*Car component is called here*/}
          </div>
        );
      }
    }

    // Who lives in my Garage?
    // I am a Car!
    ```

### Destructuring Props

* Destructuring is an ES6 feature that allows us to extract sections of data from objects, then assign them to new variables.
* This way, we don't need to call **props.foo** / **this.props.bar** . Instead, we can directly call **foo** / **bar**.
*   Note: variables in destructure statement must match the prop names in the component call

    ```jsx
    // Profile.js (functional)
    export default function Profile(props) {
        const { first, last } = props;    // destructured props
        return <h1>Name: {first} {last}</h1>    // call {first} instead of {props.first}
    }

    // or Profile.js (class) --> just call "const {..} = props" in render(), but above return().

    // App.js
    <Profile first="Dev" last="Patel"/>
    ```

### Components in Files

* React is all about re-using code, and it can be smart to insert some of your components in separate files. (ie. a navbar in mutliple pages). To do that:

1. ensure component you're exporting has: "export default" statment 2. In the file you're importing the component to:

```js
import ComponentName from './path_to_component.js';
```

***

## A Word on Styling

* the main style sheet is the one imported in index.js (the file whichever renders App.js into the root node). You can optionally use sass partials and imports with this style sheet.
* For _inline styles_, use the same **`style=`** attribute, but instead, use a JS object inside of a curly brace `{}` allowing for JSX expressions:
*   camelCase for properties inside the inline style {}. ie. backgroundColor, fontSize, borderColor.

    **style= { {**

    ​ **\<css\_property>: "\<css\_style>",**

    **} }**

```
// if you don't add unit after number for ie. fontSize, it assumes px. If you choose to add px, then encase the number and unit in quotes ie. fontSize="72px"
<p style={{color: "white", backgroundColor: "#f1356d", fontSize:72}}>Hi</p>
```

*   If you have a large set of styles, you can assign a style `object` to a constant to keep your code organized. Declare your styles constant as a global variable at the top of the file:

    ```
    // global styles object
    const styles = {
      color: "purple",
      fontSize: 40,
      border: "2px solid purple",
    }

    class Colorful extends React.Component {
      render() {
        return (
          // assign style={styles} object
          <div style={styles}>Winter is Coming</div>
        );
      }
    };
    ```

***

## Events

* React has the same events as HTML: click, change, mouseover etc. They're written in camelCase ie. `onClick` instead `onclick`.
* React event handlers are written inside curly braces: _**`onClick={_handler_}`**_
*   Note: don't include ()'s for the eventhandler function (you don't want to call it, just reference it)

    ```
    <button onClick={shoot}>Take the Shot!</button>
    ```

### Event Handlers

*   A good practice is to put the event handler as a method in the component class:

    ```
    // FUNCTIONAL COMPONENT - call <handler>
    export default function FunctionEvent(props) {
        const handleClick = () => console.log("trigger");                    // event handler
        return <button onClick={handleClick}>Click Here</button>    // onClick={handleCLick}
    }

    // CLASS COMPONENT - call this.<handler>, above render()
    class FunctionEvent extends Component {
      const handleClick = () => console.log("trigger");                    // event handler

      render() {
        // this.<handler> references <handler> method in the same class
        return <button onClick={() => this.shoot}>Take the shot!</button>    // onClick={() => this.handleClick}
      }
    }
    ```

### Bind `this` for EventHandlers (only for Class Components)

* Note: **There's no need to bind functions in functional components since there's no 'this' in functions**
* There are 3 ways to bind functions:

1.  bind the eventhandler function (_**non-arrow**_) using **.bind()** in the **class component’s constructor**:

    ```jsx
    // class constructor needs .bind()
    constructor(props) {
        super(props)
        this.increment = this.increment.bind(this);
    }

    // regular function
    increment() {
        this.setState({
          count: this.state.count+1
        });
    }

    // this.<handler>
    <button onClick={this.increment}>++</button>
    ```
2.  (RECOMMENDED) or use **arrow function**

    ```jsx
    // class constructor doesn't need .bind()

    // arrow function
    increment = () => {
        this.setState({
            count: this.state.count+1
        });
    }

    // this.<handler>
    <button onClick={this.increment}>++</button>
    ```
3.  use **regular function** + **arrow syntax on call**

    ```jsx
    // class constructor doesn't need .bind()

    // arrow function
    increment() {
        this.setState({
            count: this.state.count+1
        });
    }

    // () => this.<handler>()
    <button onClick={() => this.increment()}>++</button>
    ```

***

## State

* `State` is a built-in object where you store property values that belong to the component. When the `state` object changes, the component re-renders.
* State consists of any data your application needs to know about, that can change over time. (since you can't change props)
* **`State` can only be used in a Class Component**
* Props vs. State:
  1. Props are passed to the component –– State is contained in the component
  2. Props are immutable –– State is mutable

### Create State

*   The `state` object is initialized in the `constructor()`:

    _**`this.state = {<property-values>};`**_

    ```
    class Car extends Component {
      constructor(props) {
        super(props);             // must call super(props)
        this.state = {        // define state object in constructor    
          brand:'Ferrari',
          color: 'red',
          year: 1985
        };
      }
      render() {
        return (
            <div>
            {/* 1985 red Ferrari */}    
              <p>{this.state.year} {this.state.color} {this.state.brand}</p>
          </div>
        );
      }
    }
    ```

### Using the `state` object

* Refer to the `state` anywhere in the component by: **`this.state.<propertyname>`**

### Changing the `state` object

*   To change a value in the state object, use the `this.setState()` method. Called inside a component so _**`this`**_ refers to the component. Changes to the state object will re-render the component.

    _**`this.setState({<new-key-value-pairs})`**_

    ```
    class Counter extends Component {
        constructor(props) {
            super(props);
            this.state = { // state initially has count:0
                count: 0,
            }
        }

        increment = () => {
            this.setState({count: this.state.count+1}); // increments count in state ++
        }

        render() {
            return (
                <div>
                    <h1>Count value = {this.state.count}</h1>
                    <button onClick={() => this.increment()}>++</button>  {/*calls increment() onClick*/}
                </div>
            )
        }
    }

    export default Counter;
    ```
*   Note: if you want to access `state` in:

    1. `render()`, call _**`this.state`**_.
    2. the `return` of the render(), call _**`{this.state}`**_. (Since it's in JSX)

    ```
    // ie, there's a state with a name: 'dev'. To access this, you can either do {this.state.name} in the return statement, or:
    render() {
      // write javascript here and define a const that accesses data from the state
      const name = this.state.name;
      return (
          <div>
          {/*dev (block-scope variable 'name'*/}
            <h1>{name}</h1>
        </div>
      );
    }
    ```

Note: Just before the return statement in the `render()`, you can write JavaScript directly ie. declare functions, access data from `state` or `props`, perform computations on this data, and so on. Then, you can assign any data to variables, which you have access to in the `return` statement.

NOTE: If you make a _stateful component_, no other components are aware of it's `state`; it's completely local to the component. That is, unless you pass state data to a child component as a prop.

### Use State to Toggle Elements

* Sometimes you might need to know the previous state when updating the state. Since React updates state asynchronously (may batch multiple `setState()` calls into a single update), you can't rely on the previous value of `this.state` or `this.props` when calculating the next value.
  * ie. don't do this in a `setState()`: _**counter: this.state.counter + this.props.increment**_
*   Instead, pass `setState` a function that allows you to access state and props (guarantees most current values for state and props):

    ```
    this.setState((state, props) => ({
      counter: state.counter + props.increment
    }));
    ```
*   You can also use a form without `props` if you need only the `state`:

    ```jsx
    this.setState(state => ({
      counter: state.counter + 1
    }));
    ```
* NOTICE that you have to wrap the object literal in parentheses, otherwise JavaScript thinks it's a block of code.

SIMPLE PROJECT: COUNTER

```jsx
class Counter extends Component {
  constructor(props) {
    super(props);
    // create stateful component with initial count value
    this.state = {
      count: 0
    };
  }

  // arrow functions, so you don't need to bind
  increment = () => {
    this.setState(state => ({
      count: state.count + 1
    }))
  }

  decrement = () => {
    this.setState(state => ({
      count: state.count - 1
    }))
  }

  reset = () => {
    this.setState(state => ({
      count: 0
    }))
  }

  render() {
    return (
      <div>
        <button className='inc' onClick={this.increment}>Increment!</button>
        <button className='dec' onClick={this.decrement}>Decrement!</button>
        <button className='reset' onClick={this.reset}>Reset</button>
        <h1>Current Count: {this.state.count}</h1>
      </div>
    );
  }
};
```

### Pass State as Props to Child Components

* A common pattern is to have a stateful component containing the `state` important to your app, that then renders child components. You want these components to have access to some pieces of that `state`, which are passed in as props.
* ie, you may have an App component that renders Navbar and other child components. In your `App`, you have `state` that contains a lot of user information, but the `Navbar` only needs access to the user's username so it can display it. You pass that piece of `state` to the `Navbar`component as a prop
* This patter reflects 2 ideas:
  1. _**unidirectional data flow**_ - State flows in one direction down the tree of your application's components, from the stateful parent component to child components.
  2. complex stateful apps can be broken down into just a few, or maybe a single, stateful component. The rest of your components simply receive state from the parent as props, and render a UI from that state
*   To pass data from a state in a parent component to a child component, pass it as a prop when you call the chlid component in the parent's render:

    ```jsx
    // MyApp.js
    class MyApp extends Component {
      constructor(props) {
        super(props);
        // Stateful
        this.state = {
          name: 'CamperBot'
        }
      }
      render() {
        return (
           <div>
               {/*calls the navbar child component and passes data from state*/}
             <Navbar name={this.state.name}/>
           </div>
        );
      }
    };

    // Navbar.js
    class Navbar extends React.Component {
      constructor(props) {
        super(props);
      }
      render() {
        return (
        <div>
          {/*the state data 'name' is in props, so access it there*/}
          <h1>Hello, my name is: {this.props.name} </h1>
        </div>
        );
      }
    };
    ```
*   NOTE: you can also pass callback and/or handler functions as props like so:

    ```jsx
    // inside the render return of a parent component, where handleChange() is a function in the parent component. The child now has handleChange() in the props object (it can call it via this.props.handleChange)
    <Child handleChange={this.handleChange}/>
    ```

***

## React Hooks

* Hooks allow **function components to access state** (renders class components obsolete)
* Remember: **State** –– generally refers to **application data** (properties) that need to be tracked
* You can also **build your own custom Hooks**

### Hook Rules

1. Hooks can only be called inside **functional components**. (won't work in class components; already has access to state)
2. Hooks can only be called at the **top level of a component**.
3. Hooks **cannot be conditional**

### useState

* lets you use **state in a functional component**.
  1.  **Import** (note the destructure with {}'s)

      ```jsx
      import { useState } from "react";
      ```
  2.  **Initialize useState**

      * We initialize our state by calling **useState** in our function component.
      * You pass the initial state to this function and it returns two values:
        1. A **variable** with the **current state**.
        2. A **function** to **update the state**.

      ```jsx
      // 1. Set each individual state
      export default function MyComponent() {
        // brand, model, color                     = variables
        // setBrand, setModel, setColor = functions
          const [brand, setBrand] = useState("Ford");                // brand: "Ford"
        const [model, setModel] = useState("Mustang");        // model: "Mustang"
        const [color, setColor] = useState("Red");                // color: "Red"
      }
      ```

      // 2. \*RECOMMENDED) use 1 state and include an object: export default function MyComponent() { const\[car, setCar] = useState({

      ```
      brand: "Ford",
      model: "Mustang",
      color: "red"
      ```

      }) }

      ```
      ```

1. **Read State**
   * Use the state variable in the functional component like: **{state-variable}**
   *   (for individual ones: return

       My {brand} is a {color} {model}

       )

       ```jsx
       export default function MyComponent() {
         const[car, setCar] = useState({
           brand: "Ford",
           model: "Mustang",
           color: "red"
         })

         // <state-var>.<property> --> car.brand gives "Ford"
         return <p>My {car.brand} is a {car.color} {car.model}</p>
       }
       ```
2. **Update State**
   * (for individual ones: setColor("blue")) \[DONT: do color = "blue", use the setColor function]
   * When state is updated, the **entire state gets overwritten**, what if we only want to update one property of the car state.
   * _DONT DO:_ **setCar({color: "blue"})** –– this would remove the rest (brand + model) from our state.
   *   Use the JavaScript **spread operator** to update only one state property:

       ```jsx
       // between initial-useState & return-statement
       const updateColor = () => {
         setCar(previousState => {
               return { ...previousState, color: "blue" }
           });
       }

       return (
         <div>
           <p>My {car.brand} is a {car.color} {car.model}</p>

           {/*onClick, it updates the color-state*/}
           <button type="button" onClick={updateColor}>Blue</button>
           <div/>
       )
       ```

### useEffect

* _**Side Effect**_ –– any execution that affects something outside the scope of the function being executed.
  * ie. Data Fetching, Updating global variables from inside a function, and manually changing the DOM in React components are all examples of **side effects**.
* **useEffect** lets you perform **side effects** in functional components.
* **useEffect** runs on **every render** (which may be caused by changes in state)

Generally, there are 3 ways to use useEffect, through overloading:

1.  _**No Dependency Passed**_

    ```jsx
    import { useState, useEffect } from "react";

    useEffect(() => {
      // Runs on every render
    });
    ```
2.  _**An empty array**_:

    ```jsx
    import { useState, useEffect } from "react";

    useEffect(() => {
      // Runs only on the first render
    }, []);
    ```
3.  _**Props or state values:**_

    ```jsx
    import { useState, useEffect } from "react";

    useEffect(() => {
      // Runs on the first render
      // + and any time any dependency value changes
    }, [prop, state]);
    ```

!\[Screen Shot 2022-05-04 at 6.59.19 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-05-04 at 6.59.19 PM.png)

### useContext

*   it's a way to **manage state globally**.

    **The Problem**
* **State** should be held by the **highest parent component** that needs access to it.
* Imagine you have 10 components, and the **top (1)** and **bottom (10)** of the stack need access to **state**.
* **without useContext**, you would need **"prop drilling"** –– pass the state as props through each nested component from 1 –> 10.
*   Even components that didn't need state had to act as holders of state so that it could reach **component 10**

    **The Solution**
*   **create Context**, which provides data to components no matter how deep they are in the components tree. (usually used to manage global data/state)

    (assume **Component1** > Component2 > Component3 > **Component4**)

1.  **Create Context**

    Import **createContext** and initialize it

    ```jsx
    // Component1.js (Parent)
    import { useState, createContext } from "react";
    import ReactDOM from "react-dom/client";

    const UserContext = createContext()
    ```
2.  **Context Provider**

    wrap the child components in the **Context Provider** instantiated above (UserContext) and **supply state value**.

    ```jsx
    // Component1.js (Parent)
    function Component1() {
      const [user, setUser] = useState("Dev Patel");

      return (
        <UserContext.Provider value={user}>
              <h1>{`Hello ${user}!`}</h1>
              <Component2 user={user} />
        </UserContext.Provider>
      );
    }
    ```
3.  **useContext**

    use the **useContext** hook in the Child component (import + access user Context)

    ```jsx
    // Component4.js (Child)
    import { useState, createContext, useContext } from "react";

    function Component5() {
      const user = useContext(UserContext);

      return (
        <>
          <h1>Component 5</h1>
          <h2>{`Hello ${user} again!`}</h2>
        </>
      );
    }
    ```

***

## Conditional Rendering

### ...with IF-ELSE

* use an if-else in the render() method to control the rendered view.
*   when the condition is true, one view renders –––– vs. –––– when it's false, it's a different view.

    ```
    render() {
      if(...){
         // render display 1 if true
         return (...);
      } else {
         // render display 2 if false
         return (...);
      }
    }
    ```

### ...with &&

* A more consice approach to conditional rendering is using the && logical operator.
*   when the condition is true, it **returns**

    –––– vs. –––– when it's false, it will evaluate to false and **return nothing**

    ```jsx
    {condition && <p>Is True</p>}

    // ie. returns the <h1> since condition is TRUE
    const x = 1
    { x > 0 && <h1>positive</h1>}
    ```
*   You can include these &&'s directly in your JSX and chain multiple && together. This allows you to handle more complex conditional logic in your `render()` method without repeating if-else statements.

    ```
    // assume a button which toggles the value of 'display' to true/false in state.

    render() {
        return (
           <div>
             <button onClick={this.toggleDisplay}>Toggle Display</button>
                {/* when display=true, h1 is returned and rendered; otherwise returns nothing */}
             {this.state.display && <h1>Displayed!</h1>}
           </div>
        );
    }
    ```

### ...with Ternary Operator

*   You can also use a ternary opertor (same as is in Java): _**condition ? true : false**_

    ```jsx
    function MissedGoal() {
        return <h1>MISSED!</h1>;
    }

    function MadeGoal() {
        return <h1>GOAL!</h1>;
    }

    function Goal(props) {
      const isGoal = props.isGoal; // isGoal is BOOLEAN prop
        return (
            <div>
                { isGoal ? <MadeGoal/> : <MissedGoal/> }
            <div/>
        );
    }
    ```

***

## List Rendering

*   _**`map()`**_ –– used to iterate over an array and manipulate or change data items.

    ```jsx
    const numbers = [1, 2, 3, 4, 5];
    // (individual array item) => some operation/manipulation
    const doubled = numbers.map((number) => number * 2);

    // doubled = [2, 4, 6, 8, 10]
    ```

    We can use .map( ) to dynamically transform arrays into lists of elements.

    When doing so, it's important to provide a **key** prop to each element item to be used by React when rendering that element.

    ```jsx
    // ie render an array of product objects into a list:
    export default function Product() {
        const products = [
            {id:1,name:"Laptop",price:500},
            {id:2,name:"Phone",price:200},
            {id:3,name:"Modem",price:50},
            {id:4,name:"Laptop",price:900}, // 'key' prop from id-key allows for duplicate p.name's
        ]

        const productsList = products.map((p) => (
            <li key={p.id}>{p.name}: ${p.price}</li>
        ));

        return <ul>{productsList}</ul>
    }
    ```
*   (NOT RECOMMENDED) When you don’t have stable IDs for rendered items, you may use the **item index** as a key as a last resort:

    ```jsx
    const productsList = products.map((p, index) => (
            <li key={index}>{p.name}: ${p.price}</li>
    ));

    return <ul>{productsList}</ul>
    ```

***

## User Input Form Handling

```jsx
const { Component } = require("react");
class Form extends Component {
    // create a state to hold input-field values
      state = {
        firstname: "",
        lastname: "",
    }

      // eventhandler required to update state holding the form input value
    handleFirstnameChange = (event) => {
        // "event.target.value" holds value in form field, so update state accordingly
        this.setState({
            firstname: event.target.value,
        })
    }

      // identical to handleFirstNameChange
      handleLastNameChange = (event) => {
        this.setState({
            lastname: event.target.value,
        })
    }

      // eventhandler for when forms are submitted
       handleSubmit = (event) => {
        event.preventDefault();
        console.log(this.state.firstname);
        console.log(this.state.lastname);
    }

    render() {
        return (
            <div>
                <form onSubmit={this.handleSubmit}>
                      {/*FIRSTNAME INPUT FIELD*/}
                    {/*should always have onChange attribute with event handler passed*/}
                                        {/*use current state of form field value as input-tag value*/}
                      <input
                          type="text"
                          value={this.state.firstname}
                          onChange={this.handleFirstnameChange}
                    ></input>

                      {/*LASTNAME INPUT FIELD*/}
                      <input
                             type="text"
                                                value={this.state.lastname}
                          onChange={this.handleLastNameChange}
                    ></input>

                      {/*BUTTON FOR FORM SUBMISSION*/}
                      <button type="submit">Submit</button>
                </form>
            </div>
        )
    }
}

export default Form;
```

***

## Fragments

*   **React Fragments** allow you to wrap or group multiple elements without adding an extra node (ie. a parent div) to the DOM.

    ```jsx
    // PROBLEM: what if we don't want that extra <div> wrapper to be rendered?
    function Parent () {
      return (
        <div>
           <h1>Heading</h1>
           <h2>Subheading</h2>
        </div>
      );
    }

    /* ENDS UP RENDERING:
    <div>
            <h1>Heading</h1>
            <h2>Subheading</h2>
    </div>
    */
    ```

    There is no problem with `div` containers if they serve a purpose like adding styles to the JSX. However, they are not always needed to wrap our JSX. In this case, when we do, they become extra nodes that clutter the DOM tree. (Do note that child elements no longer have that DIV container.)

### \<React.Fragment> or <>

**You can also use the shorthand for \<React.Fragment>, which is simply an empty tag: <>\</>**

```jsx
// SOLUTION: React.Fragment
function Parent () {
  return (
    <React.Fragment>
       <h1>Heading</h1>
       <h2>Subheading</h2>
    </React.Fragment>
  );
}

// OR SHORTHAND:
function Parent () {
  return (
    <>
       <h1>Heading</h1>
       <h2>Subheading</h2>
    </>
  );
}

/* ENDS UP RENDERING:
<h1>Heading</h1>
<h2>Subheading</h2>
*/
```

***

## Memos

Using _**memo**_ will cause React to **skip** rendering a component if its props have not changed. This MAY **improve performance**.

_Memo_ derives from **memoization** –– meaning, the result of the functional component wrapped in React.memo is saved in memory and **returns the cached result** if it's being called with the **same input (props)** again.

[![Inforgraphic explaining when to use React.memo()](https://dmitripavlutin.com/static/c07d2ce4ede6301197b9605a75ae9b4e/b60ba/when-to-use-react-memo-infographic.jpg)](https://dmitripavlutin.com/static/c07d2ce4ede6301197b9605a75ae9b4e/5fd6b/when-to-use-react-memo-infographic.jpg)

```jsx
import React from "react";

function Movie({ title, releaseDate }) {
  return (
    <>
      <h1>Movie title: {title}</h1>
      <h2>Release date: {releaseDate}</h2>
    </>
  );
}

// export a the "memoized" component
export default React.memo(Movie);
```

***

## Portals

**React Portals** provide a way to render an element outside of its component hierarchy (outside of its parent component’s DOM node), in a separate component.

USE-CASE: consider you want to render a **modal** (alert thingy), or really any other component, in a div other than the "root" div.

```jsx
// index.html - say you want to render a component into the 'modal' div
<div id="root"></div>
<div id="modal"></div>

// Modal.js
import { createPortal } from "react-dom"

export default function Modal() {
    // createPortal(child, container) --> renders child into container
      return createPortal(
        <div>Modal</div>, // child
        document.getElementById("modal") // container (in index.html)
    )
}

// App.js - you still have to add the Modal component in App.js (which renders into 'root' div). dw tho, when it comes time to render <Modal />, React will see the portal and render it in the 'modal' div
<div className="App">
    ...
  <Modal />
</div>
```

***

## Lifecycle

* Each component in React has a lifecycle which you can monitor and manipulate during its three main phases:

1. _**Mounting**_ - Putting elements into the DOM
   * React has 4 built-in methods which get called when mounting (inserting into dom) a component:
     1. **`constructor()`**
        * called before anything else, when the component is initiated, and it's where you set up the initial `state` and other initial values
        * called with the `props`, as arguments (`constructor(props) {...}`)
        * first line in constructor should be passing the props to parent via `super(props);`
        * **`getDerivedStateFromProps()`**
          * called right before rendering the element(s) in the DOM. (after constructor and before render)
          * This is where you set the `state` object based on the initial `props`.
          * It takes `state` as an argument, and returns an object with changes to the `state`
          *   static method

              ```
              class Header extends React.Component {
               constructor(props) {
                 super(props);
                 this.state = {favouritecolor: "red"};
               }

               // sets the state object based on props below
               static getDerivedStateFromProps(props, state) {
                 return {favouritecolor: props.favcol };
               }

               render() {
                 return (
                   // My favourite color is yellow
                   <h1>My Favourite Color is {this.state.favouritecolor}</h1>
                 );
               }
              }

              // shows 'yellow' instead of 'red' (state.favouritecolor is overrided)
              ReactDOM.render(<Header favcol="yellow"/>, document.getElementById('root'));
              ```
        * **`render()`**
          * _**required method**_ and will always be called, the others are optional and will be called if you define them.
          *   outputs the HTML to the DOM

              ```
              class Header extends React.Component {
               render() {
                 return (
                   <h1>This is the content of the Header component</h1>
                 );
               }
              }

              ReactDOM.render(<Header />, document.getElementById('root'));
              ```
     2. **`componentDidMount()`**
        * called after the component is rendered.
        * This is where you run statements that requires that the component is already placed in the DOM.
        * Most web developers, at some point, need to call an API endpoint to retrieve data. The best practice with React is to place API calls or any calls to your server in this method because any calls to `setState()` here will trigger a re-rendering of your component.
        * When you call an API in this method, and set your state with the data that the API returns, it will automatically trigger an update once you receive the data.
        *   It's also the best place to attach any event listeners you need to add for specific functionality

            ```
            // in this example, after the component is mounted (placed into the DOM), the componentDidMount() is called and changes data in the state (live changes)

            class Header extends React.Component {
              constructor(props) {
                super(props);
                this.state = {favoritecolor: "red"};
              }
              // called 1 sec after component is mounted
              componentDidMount() {
                setTimeout(() => {
                  this.setState({favoritecolor: "yellow"})
                }, 1000)
              }
              render() {
                return (
                  <h1>My Favorite Color is {this.state.favoritecolor}</h1>
                );
              }
            }

            ReactDOM.render(<Header />, document.getElementById('root'));
            ```
2. _**Updating**_ - component is _updated_ whenever there is a change in the component's `state` or `props`.
   * React has five built-in methods that get called, in this order, when a component is updated:
     1. **`getDerivedStateFromProps()`**
        * first method that is called when a component gets updated
        * Also in the mounting stage of the lifecycle (scroll up for further detail and example), this is where you set the `state` object based on the initial props
        * **`shouldComponentUpdate()`**
          * In this method, you can return a Boolean value that specifies whether React should continue with the rendering or not.
          *   The default value is `true`.

              ```
              class Header extends React.Component {
               constructor(props) {
                 super(props);
                 this.state = {favoritecolor: "red"};
               }

                  // since this is false, it won't allow for the changeColor method to work. It will only show: My favourite Color is red. The button will show but won't work.
               shouldComponentUpdate() {
                 return false;
               }
               changeColor = () => {
                 this.setState({favoritecolor: "blue"});
               }
               render() {
                 return (
                   <div>
                   <h1>My Favorite Color is {this.state.favoritecolor}</h1>
                   <button type="button" onClick={this.changeColor}>Change color</button>
                   </div>
                 );
               }
              }

              ReactDOM.render(<Header />, document.getElementById('root'));
              ```
        * **`render()`**
          * _**required method**_ and will always be called, the others are _still_ optional and will be called if you define them.
          * of course called when a component gets _updated_, it has to re-render the HTML to the DOM, with the new changes.
     2. **`getSnapshotBeforeUpdate()`**
        * In this method, you have access to the `props` and `state` _before_ the update, meaning that even after the update, you can check what the values were _before_ the update.
        *   If you use this method, you must also use the `componentDidUpdate()` method, or else you'll get an error.

            ```
            /* All this does is:
              1. When the component is mounting it is rendered with the favorite color "red".
              2. When the component has been mounted, after 1 sec, the favorite color becomes "yellow".
                  - This action triggers the update phase and executes the getSnapshotBeforeUpdate(), and writes in the empty DIV1
                  - Then the componentDidUpdate() is executed and writes in the empty DIV2:
            */ 
            class Header extends React.Component {
              constructor(props) {
                super(props);
                this.state = {favoritecolor: "red"};
              }
              componentDidMount() {
                setTimeout(() => {
                  this.setState({favoritecolor: "yellow"})
                }, 1000)
              }
              getSnapshotBeforeUpdate(prevProps, prevState) {
                document.getElementById("div1").innerHTML =
                "Before the update, the favorite was " + prevState.favoritecolor;
              }
              componentDidUpdate() {
                document.getElementById("div2").innerHTML =
                "The updated favorite is " + this.state.favoritecolor;
              }
              render() {
                return (
                  <div>
                    <h1>My Favorite Color is {this.state.favoritecolor}</h1>
                    <div id="div1"></div>
                    <div id="div2"></div>
                  </div>
                );
              }
            }

            ReactDOM.render(<Header />, document.getElementById('root'));
            ```
     3. **`componentDidUpdate()`**
        * called after the component is updated in the DOM
        * look in the example directly above for the componentDidUpdate() method call.
3. _**Unmounting**_ - when a component is removed from the DOM
   * React has only one built-in method that gets called when a component is unmounted:
     1.  **`componentWillUnmount()`**

         * called when the component is about to be removed from the DOM

         ```
         class Container extends React.Component {
           constructor(props) {
             super(props);
             this.state = {show: true};
           }
           delHeader = () => {
             this.setState({show: false});
           }
           render() {
             let myheader;
             if (this.state.show) {
               myheader = <Child />;
             };
             return (
               <div>
                 {myheader}
                 <button type="button" onClick={this.delHeader}>Delete Header</button>
               </div>
             );
           }
         }

         class Child extends React.Component {
           componentWillUnmount() {
             alert("The component named Header is about to be unmounted.");
           }
           render() {
             return (
               <h1>Hello World!</h1>
             );
           }
         }

         ReactDOM.render(<Container />, document.getElementById('root'));
         ```

***

### Optimize Re-Renders with shouldComponentUpdate

* So far, if any component receives new `state`or new `props`, it re-renders itself and all its children- even if the state and props are the same.
* The default behavior is that your component re-renders when it receives new `props`, even if the `props` haven't changed. You can use `shouldComponentUpdate()` to prevent this by comparing the `props`. The method must return a `boolean` value that tells React whether or not to update the component. You can compare the current props (`this.props`) to the next props (`nextProps`) to determine if you need to update or not, and return `true` or `false` accordingly
*   The method is _**`shouldComponentUpdate()`**_, and it takes _**`nextProps`**_ and _**`nextState`**_ as parameters.

    ```
    shouldComponentUpdate(nextProps, nextState) {
        console.log('Should I update?');
        // Some logic below that must return boolean (will only update component if returned true)
          return true;
      }
    ```

***

## Event Listeners

* The `componentDidMount()` method is also the best place to attach any event listeners you need to add for specific functionality.
* React provides a _**synthetic event system**_ which wraps the _**native event system**_ present in browsers. This means that the synthetic event system _behaves exactly the same regardless of the user's browser_ - even if the native events may behave differently between different browsers.
* See list of synthetic events [here](https://reactjs.org/docs/events.html)
* If you want to attach an event handler to the document or window objects, you have to do this directly
*   Basic syntax: `<element>.addEventListener('<eventName>', function (event) {...})`

    ie. document.addEventListener('keydown', function(event) {...})
* Then, in `componentWillUnmount()`, remove this same event listener. You can pass the same arguments to `<element>.removeEventListener()`. It's good practice to use this lifecycle method to do any clean up on React components before they are unmounted and destroyed. Removing event listeners is an example of one such clean up action

***

### Dynamically Render Elements with Array.map()

* Conditional rendering is useful, but you may need your components to render an unkown number of elements (often predecated by the user's input)
* Programmers need to write their code to correctly handle that unknown state ahead of time
*   ie. for a simple 'to do list', the programmer has no way of knowing how many items a user might add at once ("separate items with commas" can be 1 item or 20 items).

    ```
    // make an array with the csv user input:
    const arr = this.state.userInput.split(',');

    // then in the render, map over the array and dynamically render a li for each item:
    const items = this.state.arr.map(
      item => <li>{item}</li>
    );

    // optionally, add a unique index key <li>'s:
    const items = this.state.arr.map(
        (item, i) => <li key={i}>{item}</li>
    );
    ```

### Dynamically Filter Elements with Array.filter()

* .filter() - filters the contents of an array based on a condition, then returns a new array. Using arrow func for this is best:

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      users: [
        {
          username: 'Jeff',
          online: true
        },
        {
          username: 'Alan',
          online: false
        },
      ]
    };
  }
  render() {
    // this will filter all user objects inside the users[] and only return those whose 'user.online: true'.
    const usersOnline = this.state.users.filter(user => user.online);

    // map over the filtered array, and return a <li> for each user's name:
    const renderOnline = usersOnline.map((user, i) =>
      <li key={i}>{user.username}</li>);

    return (
      <div>
        <h1>Current Online Users:</h1>
        <ul>{renderOnline}</ul>
      </div>
    );
  }
}
```

*
