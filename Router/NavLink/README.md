### `NavLink` in React Router

`NavLink` is a component from `react-router-dom` that provides enhanced functionality for navigation links in a React application. It is an extension of the `Link` component, adding features for active link styling.

#### Key Features

1. **Active Styling**:
   - Automatically applies specific styles or CSS classes to the link when the current URL matches the `to` prop. This helps in highlighting the active page in navigation menus.

2. **Custom Styling**:
   - You can specify custom styles or classes to be applied when the link is active, making it easy to create a visually distinct active state.

3. **Exact Matching**:
   - Supports exact route matching to ensure the link is styled as active only when the URL matches exactly. 

#### Basic Usage

1. **Installation**:
   ```bash
   npm install react-router-dom
   ```

2. **Setup Example**:
   ```javascript
   import React from 'react';
   import { BrowserRouter as Router, Route, Routes, NavLink } from 'react-router-dom';

   function Home() {
     return <h2>Home Page</h2>;
   }

   function About() {
     return <h2>About Page</h2>;
   }

   function Contact() {
     return <h2>Contact Page</h2>;
   }

   function App() {
     return (
       <Router>
         <nav>
           <ul>
             <li><NavLink to="/" end className={({ isActive }) => isActive ? "active-link" : ""}>Home</NavLink></li>
             <li><NavLink to="/about" className={({ isActive }) => isActive ? "active-link" : ""}>About</NavLink></li>
             <li><NavLink to="/contact" className={({ isActive }) => isActive ? "active-link" : ""}>Contact</NavLink></li>
           </ul>
         </nav>

         <Routes>
           <Route path="/" element={<Home />} />
           <Route path="/about" element={<About />} />
           <Route path="/contact" element={<Contact />} />
         </Routes>
       </Router>
     );
   }

   export default App;
   ```

#### Important Props

- **`to`**:
  - Specifies the target URL path for the link.

- **`end`**:
  - When set, ensures the link is active only when the URL exactly matches the `to` path.

- **`className`**:
  - A function that determines the class name based on whether the link is active or not. This allows dynamic styling.

**Example**:
```javascript
<NavLink 
  to="/" 
  end 
  className={({ isActive }) => isActive ? "active-link" : "inactive-link"}
>
  Home
</NavLink>
```

---

### Summary

`NavLink` enhances navigation by dynamically applying active styles based on the current route. This makes it easier for users to understand which page or section is currently active, improving the navigation experience in your application.
