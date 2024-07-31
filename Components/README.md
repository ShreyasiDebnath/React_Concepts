### **What are components in React? How do functional components differ from class components?**

**Components in React:**

- **Definition:** Components are the fundamental building blocks in React. They allow you to break down the user interface into reusable pieces. Each component encapsulates its own structure, styling, and behavior.

- **Types:** React components can be implemented in two main ways:
  1. **Class Components:** 
     - **Definition:** ES6 classes that extend `React.Component`.
     - **Features:** Must have a `render` method that returns JSX. They can hold and manage local state using `this.state` and use lifecycle methods (e.g., `componentDidMount`, `componentDidUpdate`).
     - **Example:**
       ```javascript
       class MyClassComponent extends React.Component {
           constructor(props) {
               super(props);
               this.state = { count: 0 };
           }

           render() {
               return (
                   <div>
                       <p>Count: {this.state.count}</p>
                       <button onClick={() => this.setState({ count: this.state.count + 1 })}>
                           Increment
                       </button>
                   </div>
               );
           }
       }
       ```

  2. **Functional Components:** 
     - **Definition:** JavaScript functions that return JSX.
     - **Features:** Do not have a `render` method. They are simpler and used for stateless components. With the introduction of hooks in React 16.8, functional components can now manage state and side effects.
     - **Example:**
       ```javascript
       import React, { useState } from 'react';

       function MyFunctionalComponent() {
           const [count, setCount] = useState(0);

           return (
               <div>
                   <p>Count: {count}</p>
                   <button onClick={() => setCount(count + 1)}>
                       Increment
                   </button>
               </div>
           );
       }
       ```

### **Key Differences:**

1. **State Management:**
   - **Class Components:** Manage state using `this.state` and `this.setState`.
   - **Functional Components:** Manage state using the `useState` hook.

2. **Lifecycle Methods:**
   - **Class Components:** Use lifecycle methods like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`.
   - **Functional Components:** Use the `useEffect` hook to handle side effects that would typically be managed by lifecycle methods in class components.

3. **Syntax:**
   - **Class Components:** Involve more boilerplate code with classes and methods.
   - **Functional Components:** Simpler and more concise, especially with hooks.

4. **Performance:**
   - **Class Components:** May have more overhead due to class-based syntax and additional methods.
   - **Functional Components:** Tend to be more performant and easier to reason about, especially with hooks for state management.
