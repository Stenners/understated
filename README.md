# Understated
Super simple, hooks-based state management for React

You don't really need this library; it just's wrapper around React's Context API and useReducer. See the bottom for an example of handling it yourself.   

## Usage

### StateProvider
Wrap your main component with the included `StateProvider`

```javascript
import { StateProvider } from '@stenners/understated';
// import { testReducer } from './reducers'; // See reducer example below

const App = () => {
  const initialState = {

  };

  return (
    <StateProvider initialState={initialState} reducer={reducer}>
      ...
    </StateProvider>
  );
};

export default App;
```

### Reducers

Define a reducer (or seven) and import into the main app:

```javascript
export const testReducer = (state, action) => {
    switch (action.type) {
      case "someAction":
        return {
          ...state,
          thing: action.data
        };

      default:
        return state;
    }
  };
```

### Actions

Import `getState`, Define some actions and import where they need to be called.

```javascript
import { getState } from "@stenners/understated";
// use state if you need state where your action is called. 
// dispatch is used to fire the action. 
const [state, dispatch] = getState(); 

const onEvent = () => {
  dispatch({
    type: "someAction", // action 
    data: {
      ...
    }
  })
}

```

## Roll your own:

Instead of importing '@stenners/understated' and using the provider, do your own: 

```javascript
import React, { createContext, useContext, useReducer } from 'react';
import { testReducer } from './reducers';

const App = () => {

  const initialState = {};

  const StateContext = createContext(initialState);

  const [state, dispatch] = useReducer(testReducer, initialState);

  return (
    <StateContext.Provider value={{ state, dispatch }}>
      // Main component here
    </StateContext.Provider>
  );
};

```