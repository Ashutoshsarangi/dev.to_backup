## Introduction

In some scenarios lets assume you have to, use React hook concept in react class based components.

But as you know react hooks only going to work in functional component if you wish to directly using them in class based component. 

it will through an error.

So how to do it, there is a work around solution for the same.

**There are 3 step solution**

1. Create a custom Hook, (You can directly use hook, but there you won't get more benefit) 
2. Use the hook in a Higher order component
3. We need to wrap the Higher Order component in class based component.


**Create a custom Hook**

```javascript
import {useState} from 'react';
   
const useGreet = () => {
  const [text, setText] = useState('');

//... do any additional operation / hooks you want to add

return text;   
}
```

**Creating a Higher Order Component**

```javascript
// import useGreet

export const MyHigherOrderComponentDemo = (Component) => {

  return (props) => {
    const text = useGreet();
    
    return <Component text={text} {...props}/>;
  }
}
```

**Wrap Higher Order Component in class based component**

```javascript
// import useGreet

class MyClass extends React.component {

render() {
   return (
    <p>{this.props.text}</p>
  )
}
  
}

export default MyHigherOrderComponentDemo(MyClass);
``` 
