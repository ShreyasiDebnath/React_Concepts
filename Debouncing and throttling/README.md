Debouncing and throttling are techniques used to control the rate at which a function is executed, particularly in response to high-frequency events like user input, scrolling, or resizing. They are useful in optimizing performance and preventing unnecessary operations.

### **Debounce**

**Debouncing** ensures that a function is executed only after a certain period has passed without the function being called again. It's useful for scenarios where you want to wait until a user has finished performing an action before executing a function.

**Example Use Case:**

- Waiting for a user to stop typing before sending an API request to search suggestions.

**How It Works:**

1. The function is delayed by a specified amount of time.
2. If the function is called again before the delay period ends, the timer resets.
3. The function is executed only after the delay period has passed with no additional calls.

**Code Example:**

Here’s how you might implement debouncing using a custom hook in React:

```jsx
import { useState, useEffect } from 'react';

// Custom useDebounce hook
export function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const handler = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => {
      clearTimeout(handler);
    };
  }, [value, delay]);

  return debouncedValue;
}

// Example Component
function SearchComponent() {
  const [query, setQuery] = useState('');
  const debouncedQuery = useDebounce(query, 500); // 500ms delay

  useEffect(() => {
    if (debouncedQuery) {
      // Fetch search results or perform action
      console.log('Searching for:', debouncedQuery);
    }
  }, [debouncedQuery]);

  return (
    <input
      type="text"
      value={query}
      onChange={(e) => setQuery(e.target.value)}
      placeholder="Search..."
    />
  );
}
```

### **Throttle**

**Throttling** ensures that a function is executed at most once within a specified time interval. It's useful when you want to limit the rate at which a function is called, regardless of how frequently the event occurs.

**Example Use Case:**

- Handling scroll events to update position or perform actions at a fixed rate.

**How It Works:**

1. The function is executed immediately upon the first call.
2. Subsequent calls are ignored until the specified time interval has passed.
3. After the interval, the function can be executed again.

**Code Example:**

Here’s how you might implement throttling using a custom hook in React:

```jsx
import { useCallback } from 'react';
import { useRef } from 'react';

// Custom useThrottle hook
export function useThrottle(callback, limit) {
  const lastCall = useRef(0);

  return useCallback((...args) => {
    const now = new Date().getTime();
    if (now - lastCall.current >= limit) {
      lastCall.current = now;
      callback(...args);
    }
  }, [callback, limit]);
}

// Example Component
function ScrollComponent() {
  const handleScroll = useThrottle(() => {
    console.log('Scroll event handler');
  }, 1000); // 1000ms throttle

  useEffect(() => {
    window.addEventListener('scroll', handleScroll);
    return () => {
      window.removeEventListener('scroll', handleScroll);
    };
  }, [handleScroll]);

  return <div style={{ height: '2000px' }}>Scroll me!</div>;
}
```

### **Summary**

- **Debounce:** Delays the function execution until a period of inactivity.
- **Throttle:** Limits the function execution to a fixed rate.

Both techniques help optimize performance and improve user experience by controlling how often certain functions are executed in response to user interactions or events.
