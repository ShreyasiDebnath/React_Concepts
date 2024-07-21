 `React.memo` and `PureComponent` in React for optimizing component rendering.

## 1. What is PureComponent?

`PureComponent` is a base class in React for class components that implements a `shouldComponentUpdate` method with a shallow prop and state comparison. It helps to prevent unnecessary re-renders of the component when the props and state have not changed.



To use `PureComponent`, extend your class component from `React.PureComponent` instead of `React.Component`. The shallow comparison of props and state is handled automatically.

## 2. What is React.memo?

`React.memo` is a higher-order component for functional components that prevents re-renders if the props have not changed. It performs a shallow comparison of the component's props and only re-renders if there are changes.


`React.memo` helps by optimizing the performance of functional components in React. It skips rendering the component and reusing the last rendered result if the props are the same as the previous render, thus avoiding unnecessary re-renders.



## 3.Using PureComponent

```javascript
import React, { PureComponent, useState } from 'react';

class MyClassComponent extends PureComponent {
    render() {
        console.log('Rendering MyClassComponent');
        return (
            <div>
                <h1>{this.props.title}</h1>
            </div>
        );
    }
}

const App = () => {
    const [title, setTitle] = useState('Hello, World!');
    const [name, setName] = useState('Javascript');

    const changeTitle = () => {
        setTitle('Hello, React!');
    };

    console.log('parent rerender');

    return (
        <div>
            <MyClassComponent title={title} />
            <button onClick={changeTitle}>Change Title</button>
            <h1>I am learning {name}</h1>
            <button onClick={() => setName('Reactjs')}>Change Name</button>
        </div>
    );
};
export default App;
```
## 4. Using React.memo


```javascript
import React, { useState } from 'react';

const MyComponent = React.memo(({ title }) => {
    console.log('Rendering MyComponent');
    return (
        <div>
            <h1>{title}</h1>
        </div>
    );
});

const App = () => {
    const [title, setTitle] = useState('Hello, World!');
    const [name, setName] = useState(' Javascript');

    const changeTitle = () => {
        setTitle('Hello, React!');
    };

    console.log('parent rerender');

    return (
        <div>
            <MyComponent title={title} />
            <button onClick={changeTitle}>Change Title</button>
            <h1>I am learing {name}</h1>
            <button onClick={() => setName('Reactjs')}>Change Name</button>
        </div>
    );
};

export default App;

```
## Console Output
# Initial Render:
parent rerender<br>
Rendering MyComponent
## When "Change Title" Button is Clicked:
parent rerender<br>
Rendering MyComponent
## When "Change Name" Button is Clicked:
parent rerender
