React Hooks are functions that let you use state and other React features without writing a class. They were introduced in React 16.8 to enable state and lifecycle features in functional components, which were previously only available in class components. Hooks simplify the component logic, making it easier to share logic across components and improving readability and maintainability.

### Common React Hooks

1. **`useState`**
   - **Purpose**: Manages state in a functional component.
   - **Usage**: Returns a stateful value and a function to update it.
   - **Example**:
     ```javascript
     import React, { useState } from 'react';

     function Counter() {
       const [count, setCount] = useState(0);

       return (
         <div>
           <p>You clicked {count} times</p>
           <button onClick={() => setCount(count + 1)}>Click me</button>
         </div>
       );
     }
     ```

2. **`useEffect`**
   - **Purpose**: Performs side effects in functional components, such as data fetching, subscriptions, or manually changing the DOM.
   - **Usage**: Runs after every render by default, but can be controlled with a dependency array.
   - **Example**:
     ```javascript
     import React, { useState, useEffect } from 'react';

     function DataFetcher() {
       const [data, setData] = useState(null);

       useEffect(() => {
         fetch('https://api.example.com/data')
           .then(response => response.json())
           .then(data => setData(data));
       }, []); // Empty array means this effect runs once, similar to componentDidMount

       return <div>{data ? JSON.stringify(data) : 'Loading...'}</div>;
     }
     ```

3. **`useContext`**
   - **Purpose**: Accesses context values in functional components, simplifying context usage.
   - **Usage**: Allows you to consume context values without needing to use the `Context.Consumer` component.
   - **Example**:
     ```javascript
     import React, { createContext, useContext } from 'react';

     const ThemeContext = createContext('light');

     function ThemedComponent() {
       const theme = useContext(ThemeContext);
       return <div>The current theme is {theme}</div>;
     }

     function App() {
       return (
         <ThemeContext.Provider value="dark">
           <ThemedComponent />
         </ThemeContext.Provider>
       );
     }
     ```

4. **`useReducer`**
   - **Purpose**: Manages complex state logic in functional components, similar to `useState` but for more complex state interactions.
   - **Usage**: Ideal for managing state transitions with a reducer function.
   - **Example**:
     ```javascript
     import React, { useReducer } from 'react';

     const initialState = { count: 0 };
     function reducer(state, action) {
       switch (action.type) {
         case 'increment':
           return { count: state.count + 1 };
         case 'decrement':
           return { count: state.count - 1 };
         default:
           throw new Error();
       }
     }

     function Counter() {
       const [state, dispatch] = useReducer(reducer, initialState);

       return (
         <div>
           <p>Count: {state.count}</p>
           <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
           <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
         </div>
       );
     }
     ```

5. **`useMemo`**
   - **Purpose**: Memoizes the result of a computation to avoid expensive recalculations on every render.
   - **Usage**: Returns a memoized value.
   - **Example**:
     ```javascript
     import React, { useMemo, useState } from 'react';

     function ExpensiveCalculationComponent({ num }) {
       const [count, setCount] = useState(0);

       const computedValue = useMemo(() => {
         // Some expensive calculation
         return num * 2;
       }, [num]);

       return (
         <div>
           <p>Computed Value: {computedValue}</p>
           <button onClick={() => setCount(count + 1)}>Increase Count</button>
         </div>
       );
     }
     ```

6. **`useCallback`**
   - **Purpose**: Memoizes callback functions to prevent unnecessary re-creations on every render.
   - **Usage**: Returns a memoized version of the callback that only changes if one of the dependencies has changed.
   - **Example**:
     ```javascript
     import React, { useCallback, useState } from 'react';

     function Button({ onClick }) {
       console.log('Button rendered');
       return <button onClick={onClick}>Click me</button>;
     }

     function App() {
       const [count, setCount] = useState(0);

       const handleClick = useCallback(() => {
         setCount(count + 1);
       }, [count]);

       return (
         <div>
           <p>Count: {count}</p>
           <Button onClick={handleClick} />
         </div>
       );
     }
     ```


