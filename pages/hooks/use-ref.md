---
layout: section
---

## useRef

---
layout: default
---

# useRef - DOM manipulation

use ref to gain access to the DOM.

```jsx
const ref = useRef(null);

<button
  onClick={() => {
    ref.current.scrollTo({
      top: ref.current.scrollHeight,
      behavior: 'smooth',
    });
  }}
>
  Scroll to bottom
</button>
<div ref={ref} style={{ height: 30, overflow: 'auto' }}>
  <div style={{ height: 30, background: 'blue' }}>Blue</div>
  <div style={{ height: 30, background: 'red' }}>Red</div>
</div>
```

---
layout: default
---

# useRef - Manage non-rendering data

Optimize render cycle by storing value not used for rendering.


<div grid="~ cols-2 gap-4">

<div>

```jsx 
const [keypressCount, setKeypressCount] = useState(0);
const [value, setValue] = useState("")

<input
  onChange={(e) => setValue(e.target.value)}
  onKeyPress={() => setKeypressCount(keypressCount + 1)
/>
<button
  onClick={() =>
    alert(`You press ${keypressCount} times`)
  }>
  Submit
</button>
```

</div>

<div>

```jsx 
const keypressCountRef = useRef(0);
const [value, setValue] = useState("")

<input
  onChange={(e) => setValue(e.target.value)}
  onKeyPress={() => keypressCountRef.current++}
/>
<button
  onClick={() =>
    alert(`You press ${keypressCountRef.current} times`)
  }>
  Submit
</button>
```

</div>

</div>

