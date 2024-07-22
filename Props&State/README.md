## What is State?

State in React is a plain JavaScript object that represents the part of the component that can change over time. It is used to store information that might change during the lifecycle of a component, such as user inputs, selections, or any data that needs to be tracked dynamically.

## Using State in Functional Components

Functional components use the `useState` hook to manage state. The `useState` hook returns an array with two elements: the current state value and a function to update that state.

### Example

```javascript
import React, { useState } from 'react';

const Counter = () => {
    const [count, setCount] = useState(0);

    const increment = () => {
        setCount(prevCount => prevCount + 1);
    };

    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={increment}>Increment</button>
        </div>
    );
};

export default Counter;
```
## In React, state updates can be asynchronous. This means that when you call a state update function, the update does not happen immediately. Instead, React batches multiple state updates together for performance reasons, which can lead to state values not being updated immediately after a call to a state update function.
```javascript
import React, { useState } from 'react';

const Counter = () => {
    const [count, setCount] = useState(0);

    const increment = () => {
        setCount(count + 1);
        console.log(count); // Might log the previous value due to async update
    };

    return (
        <div>
            <p>{count}</p>
            <button onClick={increment}>Increment</button>
        </div>
    );
};

export default Counter;

```

## What are Props?

Props are read-only data passed from parent components to child components. They allow data to flow through the component tree and enable components to be dynamic and reusable.

## Using Props in Functional Components

In functional components, props are passed as an argument to the function:

### Example

```javascript
import React from 'react';

const Greeting = (props) => {
    return <h1>Hello, {props.name}!</h1>;
};

export default Greeting;
```
## Passing Props
 Props are passed to components similarly to how attributes are passed to HTML elements:

```javascript

import React from 'react';
import Greeting from './Greeting';

const App = () => {
    return <Greeting name="World" />;
};

export default App;
```
## Default Props
 Default props can be set using the defaultProps property, ensuring that a component has default values for props not provided:
```javascript

import React from 'react';

const Greeting = (props) => {
    return <h1>Hello, {props.name}!</h1>;
};

Greeting.defaultProps = {
    name: 'Stranger',
};

export default Greeting;
```
## Prop Types
Prop types are used to specify the types of props that a component should receive, helping to catch bugs and improve code readability. React provides the prop-types library for this purpose.
```javascript

import React from 'react';
import PropTypes from 'prop-types';

const Greeting = (props) => {
    return <h1>Hello, {props.name}!</h1>;
};

Greeting.propTypes = {
    name: PropTypes.string,
};

export default Greeting;
```





### Difference Between State and Props
## State:

Managed within the component.<br>
Mutable (can be changed with setState or useState).<br>
Represents the component's local data and behavior.<br>
Used for dynamic data that affects the rendering and behavior of the component.<br>
## Props:

Passed to the component by its parent.<br>
Immutable (cannot be changed by the component itself).<br>
Used to pass data and event handlers down the component tree.<br>
Represents fixed values or callbacks passed from parent to child components. <br>
