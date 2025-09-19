**1. controlled vs uncontrolled component**

- In React, there are two types of form inputs: Controlled Components and Uncontrolled Components.

**Controlled Components:**
   In a controlled component, the form data is handled by the state within the component. The state within the component serves as the "single source of truth" for the input elements. 

**Uncontrolled Components:**
   In an uncontrolled component, the form data is handled by the DOM itself. This means that instead of writing an event handler for every state update, you can use a ref to get form values from the DOM.

   Here's an example of an uncontrolled component in React:

   ```javascript
   const UncontrolledForm {
       const input = React.createRef();

     handleSubmit(event) {
       alert('A name was submitted: ' + input.current.value);
       event.preventDefault();
     }

 
       return (
         <form onSubmit={handleSubmit}>
           <label>
             Name:
             <input type="text" ref={input} />
           </label>
           <input type="submit" value="Submit" />
         </form>
       );
   }
   ```

**2. useReducer, Why we need it?**
Ans:- 

- lets say we have lots of state we need to manage,in this scenario rather than polluting our code base we can use the useReducer.
- Alternatively we can use custom hooks to have the logics in separate file.
- context API

**Example :-**

``` React
const [state, dispatch] = useReducer(reducer, initialState);

// How we can change something,

dispatch({type: 'ADD', payload: 100});

```

``` React
// reducer file

export const reducer = (state = initialState, action) => {
switch(action.type) {
  case 'ADD':
   // ... Do your Operation
   break;
 case 'MUL':
   // ... Do your Operation
   break;
default:
return state;
}
}
```
**3. In Which scenarios Error Boundaries don't reach Error?**

Ans:- 
- Inside Event Handler
- Asyn code
- During server-side rendering
- When Error Yhrough in the error Boundary code it self.

**4. Drawback of Context**
Ans:- Added a separate article on the same
https://dev.to/ashutoshsarangi/performance-impact-using-context-api-2eka

**5. Redux toolkit**
Ans:- We can refer to the Official document, it is self-sufficient
https://redux-toolkit.js.org/tutorials/quick-start

**6. Why we need thunk / any middleware**

Ans:-

- Thunk allows action creators to handle asynchronous operations, and dispatch actions when those operations are completed.

``` Javascript
function fetchUser(id) {
    return (dispatch) => {
        dispatch(fetchUserRequest(id));

        return fetch(`/api/users/${id}`)
            .then(response => response.json())
            .then(
                user => dispatch(fetchUserSuccess(id, user)),
                error => dispatch(fetchUserFailure(id, error))
            );
    };
}
```
**7. Slice, in redux toolkit**

https://redux-toolkit.js.org/api/createAsyncThunk
https://redux-toolkit.js.org/api/combineSlices
https://redux-toolkit.js.org/api/createSlice

**8. How JSX Prevents Injection Attack?**
Ans:- 

- React dom escapes any value embedded in jsx, before rendering them.
- Thus it ensures that you can never inject anything that's not explicitly written in your application.
- Everything is converted to a string before being rendered.

**9. <></> vs React.Fragment**

Ans:- as we see above we can pass **key attribute in Fragment** not <>.

**10. Axios Request and response interceptor**

Ans:-
- In Axios, interceptors are functions that Axios calls for every request. You can use interceptors to modify the request before it is sent, or to handle the response data before it is returned to the caller.

Example

``` Javascript
import axios from 'axios';

// Create a custom axios instance and we need to export it to be used in the application.
export const instance = axios.create({
    baseURL: 'https://your-api-url.com'
});

// Add a request interceptor
instance.interceptors.request.use((config) => {
    // Do something before request is sent
    // For example, add your auth token to the request
    config.headers.Authorization = `Bearer ${localStorage.getItem('token')}`;
    return config;
}, (error) => {
    // Do something with request error
    return Promise.reject(error);
});

// Add a response interceptor
instance.interceptors.response.use((response) => {
    // Do something with response data
    // For example, you can extract and return only the needed data
    return response.data;
}, (error) => {
    // Do something with response error
    // For example, you can handle specific HTTP error codes
    if (error.response.status === 401) {
        console.log('Unauthorized, logging out ...');
        // Logout or redirect to login page
    }
    return Promise.reject(error);
});
```
``` Javascript
import {instance} from 'path-to-the-instance'

instance.get(END_POINT) // Uses baseURL + endpoint
```

