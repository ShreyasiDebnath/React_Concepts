Passing methods as props in React is a common practice to allow child components to communicate or interact with their parent components. Here’s a basic example to illustrate how to do this:

### Example

1. **Parent Component**

   ```jsx
   import React, { useState } from 'react';
   import ChildComponent from './ChildComponent';

   const ParentComponent = () => {
     const [message, setMessage] = useState('Hello from Parent');

     // Method to be passed to child
     const handleMessageChange = (newMessage) => {
       setMessage(newMessage);
     };

     return (
       <div>
         <h1>{message}</h1>
         <ChildComponent onMessageChange={handleMessageChange} />
       </div>
     );
   };

   export default ParentComponent;
   ```

2. **Child Component**

   ```jsx
   import React from 'react';

   const ChildComponent = ({ onMessageChange }) => {
     const changeMessage = () => {
       onMessageChange('Hello from Child');
     };

     return (
       <div>
         <button onClick={changeMessage}>Change Message</button>
       </div>
     );
   };

   export default ChildComponent;
   ```

### Explanation

- **Parent Component**: Defines a method `handleMessageChange` and passes it to the `ChildComponent` as a prop named `onMessageChange`.
- **Child Component**: Receives the `onMessageChange` method as a prop and calls it when the button is clicked, passing a new message.

This setup allows the child component to invoke the parent component’s method and update the parent’s state.
