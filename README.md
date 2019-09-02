# Understated
Super simple, hooks-based state management for React

## Usage

### StateProvider
Wrap your main component with the included `StateProvider`

```javascript
import { StateProvider } from '@stenners/understated';
// import { testReducer } from './reducers'; // See below

const App = () => {
  const initialState = {
    thing: { ... }
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

const [, dispatch] = getState();

const onEvent = () => {
  dispatch({
    type: "someAction", // action 
    data: {
      ...
    }
  })
}

```

