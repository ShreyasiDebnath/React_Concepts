The `useContext` hook in React provides a way to access the value of a context directly from a component without needing to use a `Context.Consumer` component. It is part of React's Context API, which is used for managing and sharing global state or data across a React application.

### **When to Use `useContext`**

`useContext` is typically used when you want to share data or state between components without having to pass props manually through each level of the component tree. This is especially useful for global data such as user authentication, theme settings, or application configuration.

### **How `useContext` Works**

1. **Create a Context:**
   You first create a context object using `React.createContext()`. This object will hold the data you want to share.

   ```javascript
   import React, { createContext, useState } from 'react';

   // Create a Context
   const MyContext = createContext();
   ```

2. **Provide Context Value:**
   Use the `Context.Provider` component to wrap parts of your component tree and provide the context value to them.

   ```javascript
   function App() {
     const [theme, setTheme] = useState('light');

     return (
       <MyContext.Provider value={{ theme, setTheme }}>
         <ComponentA />
       </MyContext.Provider>
     );
   }
   ```

3. **Consume Context Value:**
   Use the `useContext` hook to access the context value in functional components.

   ```javascript
   import React, { useContext } from 'react';

   function ComponentA() {
     const { theme, setTheme } = useContext(MyContext);

     return (
       <div>
         <p>Current theme: {theme}</p>
         <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
           Toggle Theme
         </button>
       </div>
     );
   }
   ```

### **Example**

Here’s a complete example demonstrating `useContext`:

1. **Create Context:**

   ```javascript
   import React, { createContext, useState } from 'react';

   // Create a Context
   const ThemeContext = createContext();
   ```

2. **Provide Context Value:**

   ```javascript
   function App() {
     const [theme, setTheme] = useState('light');

     return (
       <ThemeContext.Provider value={{ theme, setTheme }}>
         <ThemeToggle />
         <ThemeDisplay />
       </ThemeContext.Provider>
     );
   }
   ```

3. **Consume Context Value in Components:**

   ```javascript
   import React, { useContext } from 'react';

   function ThemeToggle() {
     const { theme, setTheme } = useContext(ThemeContext);

     return (
       <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
         Toggle Theme
       </button>
     );
   }

   function ThemeDisplay() {
     const { theme } = useContext(ThemeContext);

     return <p>Current theme is {theme}</p>;
   }
   ```

### **Key Points**

- **Initialization:** `createContext()` creates a context object with a default value.
- **Provider:** `Context.Provider` allows you to specify the context value to be passed down the component tree.
- **Consumer:** `useContext(Context)` provides access to the context value in functional components.
- **Default Value:** If a component does not have a matching `Context.Provider` above it in the tree, it will use the default value provided to `createContext()`.

Using `useContext` helps manage state or data that needs to be accessed by multiple components in a clean and efficient way, avoiding the need for prop drilling (passing props through many layers of components).
