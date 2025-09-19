## Introduction

- To test the Redux Toolkit store, you can use the configureStore function from the Redux Toolkit to create a mock store.
- Then, you can dispatch actions to this store and check if the state changes as expected.

We need to have a separate **store.mock.js**

``` Javascript
import { configureStore } from '@reduxjs/toolkit';
import rootReducer from './path_to_your_reducer'; // replace with the path to your reducer

export const mockStore = configureStore({
  reducer: rootReducer,
  middleware: getDefaultMiddleware => getDefaultMiddleware(),
});
```
Then, in your test file, you can import this mock store and use it to dispatch actions and check the state:

``` Javascript
import { mockStore } from './store.mock';
import { yourAction } from './path_to_your_actions'; // replace with the path to your actions

describe('Redux Toolkit Store', () => {
  it('should handle yourAction', () => {
    const expectedState = { /* your expected state after dispatching the action */ };

    mockStore.dispatch(yourAction(/* your action payload */));
    expect(mockStore.getState()).toEqual(expectedState);
  });
});
```

**To Avoid Confusion**

- when you dispatch an action to the mock store created by configureStore in your tests, it will indeed "hit" the reducer.

- The reducer will run with the current state and the dispatched action, and return a new state.

- This is the same behavior as in your actual application.  However, this does **not have any consequences** for your** actual application state**.

- The mock store you create in your tests is completely separate from the actual Redux store in your application. 

-Any actions you dispatch in your tests will not affect the actual application state.

-  As for clearing the store, it's not necessary to clear the mock store after each test. Each test runs in isolation, and if you create a new mock store in a beforeEach block (as is common practice), each test will get its own fresh instance of the store. 

- Therefore, the state from one test will not leak into another.

Feel free to reach out to me if you have any queriers.
