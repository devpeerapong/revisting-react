---
layout: section
---

## useReducer

---
layout: default
---

# useReducer - lazy initialize

Same as `useState`, `useReducer` also supports lazy initialization 


<div grid="~ cols-2 gap-4">
<div>

```jsx
function createInitialState({ dateOfBirth }) {}

function Form({ dateOfBirth }) {
  const [state, dispatch] = useReducer(
    reducer,
    createInitialState({ dateOfBirth })
  );

  ...
}
```

</div>

<div>

```jsx
function createInitialState({ dateOfBirth }) {}

function Form({ dateOfBirth }) {
  const [state, dispatch] = useReducer(
    reducer,
    { dateOfBirth },
    createInitialState
  );

  ...
}
```
</div>
</div>


---
layout: default
---

# useReducer - Descriptive actions

Use a descriptive name and action to make state updates clear and self-documenting.


<div grid="~ cols-2 gap-4">
<div>

```jsx 
function reducer(state, action) {
  switch (action.type) {
    case "changed_count": {
      return { ...state, count: action.count };
    }
    default: return state;
  }
}

dispatch({ type: "changed_count ", count: state.count + 1 });
dispatch({ type: "changed_count ", count: state.count - 1 });
```

</div>

<div>

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "increment": {
      return { ...state, count: action.count + 1 } 
    }
    case "decrement": {
      return { ...state, count: action.count - 1 } 
    }
    default: return state;
  }
}

dispatch({ type: "increment" });
dispatch({ type: "decrement" });
```
</div>
</div>


---
layout: default
---

# useReducer - Always use RTK

Redux Toolkit can simplify reducer creation and common patterns.

<div grid="~ cols-2 gap-4">
<div>

```jsx 
const initialState = { count: 0 };

const incrementCount = () => ({ type: 'INCREMENT' });
const decrementCount = () => ({ type: 'DECREMENT' });

function reducer(state, action) {
  switch (action.type) {
    case "increment": {
      return { ...state, count: action.count + 1 } 
    }
    case "decrement": {
      return { ...state, count: action.count - 1 } 
    }
    default: return state;
  }
}

const [state, dispatch] = useReducer(reducer, initialState);
dispatch(increment())
dispatch(decrement())
```

</div>

<div>

```jsx
const initialState = { count: 0 };

const { reducer, actions } = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      state.count += 1; // immer built-in
    },
    decrement: (state) => {
      state.count -= 1;
    },
  },
});

const [state, dispatch] = useReducer(reducer, initialState);
dispatch(actions.increment())
dispatch(actions.decrement())
```
</div>
</div>