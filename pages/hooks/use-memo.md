---
layout: section
---

## useMemo


---
layout: default
---

# useMemo

```jsx
function TodoList({ todos, query }) {
  const filteredTodos = useMemo(
    () => todos.filter(todo => todo.includes(query)),
    [todos, query]
  );

  return (
    <div>
      {filteredTodos.map(todo => <h1 key={todo}>{todo}</h1>)}
    </div>
  )
}
```


---
layout: default
---

# useMemo - memoize jsx

<div grid="~ cols-2 gap-4">
<div>

```jsx
function TodoList({ todos, query }) {
  const [darkmode, setDarkmode] = useDarkmode(false);

  const filteredTodos = React.useMemo(
    () => todos.filter((todo) => todo.includes(query)),
    [todos, query]
  );
  
  return (
    <div>
      <label>
        <input
          type="checkbox"
          onChange={(e) => setDarkmode(e.target.checked)}
        />
        Dark mode
      </label>
      {todoJsxs}
    </div>
  );
}
```
</div>
<div>

```jsx
function TodoList({ todos, query }) {
  const [darkmode, setDarkmode] = useDarkmode(false);

  const todoJsxs = React.useMemo(
    () => todos
      .filter(todo => todo.includes(query))
      .map((todo) => <Todo key={todo} text={todo} />),
    [todos, query]
  );
  
  return (
    <div>
      <label>
        <input
          type="checkbox"
          onChange={(e) => setDarkmode(e.target.checked)}
        />
        Dark mode
      </label>
      {todoJsxs}
    </div>
  );
}
```

</div>
</div>


---
layout: default
---

# useMemo - simplify dependencies

<div grid="~ cols-2 gap-4">
<div>

```jsx
function TodoList({ todos, query }) {
  const options = useMemo(
    () => ({ mode: 'includes', query }),
    [query]
  );

  const filteredTodos = React.useMemo(
		() =>
			todos.filter((todo) => {
				switch (options.mode) {
					case "includes": return todo.includes(query);
					default: return true;
				}
			}),
		[todos, query, options]
	);
  
  /** UI below */
}
```
</div>
<div>

```jsx
function TodoList({ todos, query }) {
  const filteredTodos = React.useMemo(
		() =>
			todos.filter((todo) => {
				const options = { mode: "includes", query };

				switch (options.mode) {
					case "includes": return todo.includes(query);
					default: return true;
				}
			}),
		[todos, query]
	);
  
  /** UI below */
}
```

</div>
</div>

---
layout: fact
---

## You might not need useMemo
