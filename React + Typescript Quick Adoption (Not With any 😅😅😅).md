What would be your approach to type script adaptation if you have some old code base with JavaScript?

1. Find the atomic component where you need to adopt the typescript
2. change the file extension to. tsx
3. if you have prototypes i.e. well good.
4. declare a type/interface using those prop types 
5. assign the interface/ type in the component

```javascript
type ControlPanelProps = {
  name: 'string';
  onChange: (e: React.ChangeEvent<HTMLInputElement>, param1: string) => void;
};

const ControlPanel = ({ name, onChange }: ControlPanelProps): JSX.Element => {}

```
How I got the onChange Type:- React.ChangeEvent<HTMLInputElement>

if you have vs code Hover on the onChange menthod it will point you to write type.


![This is how you will get hint from the Vs code](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gj8ia8ybeeyhsse8pjmy.png)


2. PropType for children:- React.ReactNode

**Typing useState**

``` javascript

type Quote = {
  id?: string;
  content: string;
  source: string;
};
  const [quote, setQuote] = useState<Quote | undefined>();
  const [quotes, setQuotes] = useState<Quote[] | undefined>([]);

```

**Below I tried to add possible scenarios in a component and how we can adopt typescript**

I hope this single example with quick time give you a glance of it. 

```React
import React, { useState, useContext, RefObject } from 'react';
import { useSelector, useDispatch, Dispatch } from 'react-redux';
import { MyContext } from './MyContext'; // import your context
import { MyAction } from './actions'; // import your action type

interface ChildComponentProps {
 children: React.ReactNode;
  ref: RefObject<HTMLDivElement>;
  dispatch: Dispatch<MyAction>;
}

const ChildComponent = React.forwardRef<HTMLDivElement, ChildComponentProps>((props, ref) => {
  const { dispatch } = props;

  // useState
  const [count, setCount] = useState<number>(0);

  // Context API
  const contextValue = useContext(MyContext);

  // useSelector and useDispatch
  const value = useSelector((state: RootState) => state.value); // replace RootState with your state type
  const reduxDispatch = useDispatch<Dispatch<MyAction>>();

  // Form event handler
  const handleChange = (event: React.FormEvent<HTMLInputElement>) => {
    // handle change
  };

  return (
    <div ref={ref}>
      {/* rest of your component */}
    </div>
  );
});

export default ChildComponent;

```
I hope this helps, Feel free to reach out to me if you have any concerns also feel free to add your valuable comment on enhancing other scenarios.
