# Redux (Toolkit)

**Redux Toolkit (RTK)** is the "official, opinionated, batteries-included toolset for efficient Redux development".

RTK resolves many of the arguments against Redux related to _boilerplate_ and _unnecessary code_.

![redux-store.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1632621691258/wbX022y2RJ.png?auto=compress,format\&format=webp)

## Redux Flow

!\[Screen Shot 2022-05-05 at 8.19.25 AM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-05-05 at 8.19.25 AM.png)

**The Redux Flow** is made up of **3 main components**:

1. **Actions** –– JS objects with a required **type** property (among others)
   * **type** is simply a string that describes the action (what happened to the state) (ie. ADD\_TODO).
   * They aren't responsible for changing state.
   *   An action is dispatched via the **store.dispatch(action)** method

       ```jsx
       // action to add a todo item
       {
         	type: 'ADD_TODO',
           text: 'This is a new todo'
       } 

       //action that pass a login payload 
       {
         	type: 'LOGIN',
           payload: {
             	username: 'foo',
             	password: 'bar' 
           }
       }
       ```
2. **Reducers** –– pure functions that handle updating the state
   * performs the operations on it as instructed by the **action**
   * responsible for changing the value of the state
   *   SWITCH-CASE for the **action's type**

       ```jsx
       // takes in the current state and action
       // updates the value based on the action's type
       function counterReducer(state = { value: 0 }, action) {
         switch (action.type) {
           case 'INCREASE':
             return { value: state.value + 1 }
           case 'DECREASE':
             return { value: state.value - 1 }
           default:
             return state
         }
       }
       ```
3. **Store** –– where all the states are managed.
   * Finally, the state will be updated in the **Store**
   * The components must be subscribed to the **Store** to listen for state updates to render the states correctly in the UI.
   *   It can be created in a single line:

       ```jsx
       const store = createStore(myComponent);
       ```

## Step 1: Installation + Setup

You can either install RTK:

1.  along side **create-react-app** at a project's initial setup, OR

    ```bash
    # Redux + Plain JS template
    $ npx create-react-app my-app --template redux
    ```
2.  into an **existing** app:

    ```bash
    # NPM
    $ npm install --save react-redux
    $ npm install @reduxjs/toolkit

    # Yarn
    $ yarn add @reduxjs/toolkit
    ```

## Step 2: Create + Init Store

Now create a store to hold our states.

```jsx
// src/store/store.js
import { configureStore } from '@reduxjs/toolkit'

export default configureStore({
  reducer: {} //add reducers here
})
```

**configureStore** replaces the original **createStore** from Redux. It not only **creates** a store, but it can also accept **reducer functions** as arguments.

## Step 3: Provide Store to React Components

We need every component to have access to the Store created. This is achieved using **Provider** in **index.js** (topmost component) (much like _useContext_)

```jsx
// index.js
import store from './store';
import { Provider } from 'react-redux';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    <Provider store={store}>
        <React.StrictMode>
            <App />
        </React.StrictMode>
    </Provider>
);
```

## Step 4: Write Reducers + Actions

You can now write **reducer functions** (responsible for updating state based on action.type) and **actions** (JS objects with _type-property_) for our **Redux Store**.

Typically, you would **write reducers + actions separately**. But in RTK, both can be written in what's called a **slice**.

**Slice** –– collection of actions + reducers wrapped up inside the same file.

```js
// src/store/counterSlice.js
import { createSlice } from '@reduxjs/toolkit';

export const counterSlice = createSlice({
  name: 'counter',
  initialState: {
    value: 0,
  },
  reducers: {
    increase: (state) => {
      state.value += 1;
    },
    increaseByN: (state, action) => {
      state.value += action.payload;
    },
    decrease: (state) => {
      state.value -= 1;
    },
    decreaseByN: (state, action) => {
        state.value -= action.payload;
    },
    reset: (state) => {
      state.value = 0;
    },
  },
});

// each case under reducers becomes an action
export const { increase, increaseByN, decrease, decreaseByN, reset } = counterSlice.actions;

export default counterSlice.reducer;
```

Note, in RTK:

* **SWITCH-CASES are no longer needed** to manage the **action** with its corresponding **reducer**.
* we are now **directly mutating the state's value in the reducer function** instead of returning a new value to update the state (_thanks to **Immer library**_)

## Step 5: Import Reducer

We have exported our reducers and actions from our **counterSlice.js**, so let's **import the reducer** into our **store.js**:

```jsx
// src/store/store.js
import { configureStore } from '@reduxjs/toolkit'
import counterReducer from './counterSlice' // reducer

export default configureStore({
  reducer: {
    counter: counterReducer //add our reducer from step 4
  }
})
```

## Step 6: Add Dispatch Functions in UI

Recall from Redux Flow Diagram: our **View triggers an action** to be dispatched (received) in order to update a state.

With **React-Redux**, we can use hooks:

* **useDispatch** –– to _dispatch actions_
* and **useSelector** –– to _read data from the store_.

In the component that usually calls state and renders it into view, (ie. Counter.js for a Counter app), import:

1. **useDispatch** + **useSelector** hooks
2. **actions** from **counterSlice.js**

Then, the same Counter.js functional component will **init our 2 hooks** and return UI elements with our **dispatch(action)** triggered when clicked:

```jsx
// Counter.js
import { useState } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increase, increaseByN, decrease, decreaseByN, reset } from '../counterSlice';

export default function Counter() {
    /*
    In our slice, we set:
        name: 'counter',
        initialState: {
            value: 0
        }
    thus, to read our state in the store, we need useSelector to return state.counter.value
    */
    const count = useSelector(state => state.counter.value)
    
    // gets the dispatch function to dispatch our actions
    const dispatch = useDispatch()
    
    // use local state for holding increaseN amount
    const [ increaseAmount, setIncreaseAmount ] = useState(0);
    const [ decreaseAmount, setDecreaseAmount ] = useState(0);

    return (
      <div>
        <h1>Count value = {count}</h1>
        <button onClick={() => dispatch(increase())}>++</button>
        <button onClick={() => dispatch(decrease())}>--</button>
        <button onClick={() => dispatch(reset())}>reset</button>

        <div>
            <input
                type="text"
                value={increaseAmount}
                onChange={(e) => setIncreaseAmount(e.target.value)}
            ></input>
            
            <button
                onClick={() => {
                    dispatch(increaseByN(Number(increaseAmount)));
                }}
            >Add Amount</button>
        </div>

        <div>
            <input
                type="text"
                value={decreaseAmount}
                onChange={(e) => setDecreaseAmount(e.target.value)}
            ></input>
            
            <button
                onClick={() => {
                    dispatch(decreaseByN(Number(decreaseAmount)));
                }}
            >Subtract Amount</button>
        </div>

      </div>
    );
}
```
