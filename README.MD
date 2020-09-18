# Understanding Redux 🚀🚀

## Steps 
1. Install  the packages required.
 * redux
 * react-redux -connect react and redux
 * redux-devtools-extension -This makes redux state available in the browser
 * redux-thunk -makes the ajax call,redux can't make ajax calls

2. Set up redux in index.js
```
import { createStore, applyMiddleware } from 'redux';
import { Provider } from 'react-redux';
import thunk from 'redux-thunk';
import { composeWithDevTools } from 'redux-devtools-extension';

```

3. create  store

Redux store takes two arguments:-
- Reducer.
- Redux devtools to see redux state in the browser dev tools in the devtools you pass thunk to handle ajax calls.

``` const store = createStore(Reducer, composeWithDevTools()); ```

4. create action types
- create a file called actionTypes and create an action type.

``` export const GET_TODOS = 'GET_TODOS';```

5. create actions.

* Create a folder actions and create a file  for the  the actions, like todoAction.js.
* import the actionType from the action type file.

```
import { GET_TODOS} from '../actionTypes';
 ```
* Action is function, so create a function based on the  type of action you  want to perform.

```export function getTodos() {
    return dispatch => {
        database.on('value', snapshot => {
            dispatch({
                
                type: GET_TODOS,
                payload: snapshot.val()
            });
        });
    };
}

```

6. create reducers.

 * Reducers are functions which  work based on  actions, after actions have been dispatched  they provide the results.

* create the folder called reducers and create a file to write all your reducers.

* Takes two arguments:- 

    * state and  action.

* It uses switch case for all the actions returns the payload

 ``` 
export default function(state = {}, action) {
    switch (action.type) {
        case GET_TODOS:
            return action.payload;
        default:
            return state;
    }
} 
```

7. combine reducers

* In the reducers folder create a file called index.js and in that file we will combine all the reducers we created.

* import the package ``` combineReducers```   and the todoReducer
```
import { combineReducers } from 'redux';
import todoReducer from './todoReducer';
  ```

  ``` const mainReducer = combineReducers({
    todos: todoReducer,
    another:anotherReducer
});
```
export the mainReducer.

8. Pass the combined reducers  and  Thunk middleware  in the createstore.

* Now that we have the reducers we can pass that as(reducers) argument in the redux store and also the thunk middleware.

``` const store = createStore(mainReducer, composeWithDevTools(applyMiddleware(thunk)));```

9. make the store available to the app using provide.
```
     <Provider store={store}>
        <App />
    </Provider>,
```
10. connect react to redux using connect. 

   ```import { connect } from 'react-redux';
      import { getTodo } from '../actions/todosAction';

 ```

11. Invoke the connect function and pass the redux state as props and the actions as arguments.

*  You wanna inform the store to map data from the state to props.
 - state is immutable in react 
``` 
this function maps the redux state to props

function mapStateToProps(state, ownProps) {
    return {
        notes: state.notes
    };
} 
```
``` 
export default connect(mapStateToProps, { getTodos })(App); 
```
12. use the actions in your app.

 ```
    componentDidMount() {
        this.props.getNotes();
    } 

    ```

🎉🎉🎉🎉 Not as Hard ...  you can do it too😉😉






