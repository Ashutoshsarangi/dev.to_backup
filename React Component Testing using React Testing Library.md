Recently I adopted component testing in one of my react application using **react-testing library**.

``` Javascript
import { render, cleanup, screen, fireEvent } from "@testing-library/react";
import QuizForm from "./QuizForm";

 describe("It should render", () => {
    const props = {
      formValue: { category: "", difficulty: "" },
      setFormValue: vi.fn(),
      clickHandle: vi.fn(),
      submit: false,
      clearForm: vi.fn(),
    };

    afterEach(() => {
      cleanup(); // It is Clearing the rendered element every test cases
    });

    it("QuizForm Component Rendered Successfully", () => {
      render(<QuizForm {...props} />);
    });

    it("QuizForm Component When change the category drop down", () => {
      render(<QuizForm {...props} />);
      const categoryDropDown = screen.getByTestId("categorySelect");
      fireEvent.change(categoryDropDown); // Fireing the user event
      expect(props.setFormValue).toHaveBeenCalledOnce();
    });

    it("QuizForm Component When change the category drop down", () => {
      render(<QuizForm {...props} />);
      const difficultyDropDown = screen.getByTestId("difficultySelect");
      fireEvent.change(difficultyDropDown);
      expect(props.setFormValue).toHaveBeenCalled();
    });

    it("QuizForm Component When change the category drop down", () => {
      render(<QuizForm {...props} />);
      const createBtn = screen.getByTestId("createBtn");
      fireEvent.click(createBtn);
      expect(createBtn.textContent).toBe("Create");
      expect(props.clickHandle).toHaveBeenCalled();
    });
  });
```

**How to test react hooks, like useEffect and useState()**

``` Javascript
import { render, fireEvent, waitFor, screen } from '@testing-library/react';
import MyComponent from './MyComponent'; // replace with your component

describe('MyComponent', () => {
  it('renders and updates state based on useEffect', async () => {
    render(<MyComponent />);

    // Wait for useEffect to run and update state
    await waitFor(() => expect(screen.getByTestId('my-element')).toHaveTextContent('expected text'));

    // Interact with the component to trigger a state update
    fireEvent.click(getByTestId('my-button'));

    // Wait for state to update and re-render
    await waitFor(() => expect(screen.getByTestId('my-element')).toHaveTextContent('updated text'));
  });
});
```

**How to test our Context API**

```javascript
import { render } from '@testing-library/react';
import { MyContext } from './MyContext'; // replace with your context
import MyComponent from './MyComponent'; // replace with your component

describe('MyComponent', () => {
  it('renders with the value from the context', () => {
    const mockContextValue = { /* your mock context value */ };

    const { getByTestId } = render(
      <MyContext.Provider value={mockContextValue}>
        <MyComponent />
      </MyContext.Provider>
    );
// We can have screen Object from the library to get the testId,a s used above.

    expect(getByTestId('my-element')).toHaveTextContent('expected text'); // replace with your assertions
  });
});
```


Feel Free to reach out to me, if you have any concerns or questions.
