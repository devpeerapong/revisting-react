---
layout: section
---

## useState

---
layout: default
---

# useState - object and array
Surprisingly, state can contain Object, Array, and others non-primitive type.

<div grid="~ cols-2 gap-4">

<div>

```jsx
const [name, setName] = useState("");
const [age, setAge] = useState(18);
const [isConsent, setIsConsent] = useState(false);

setName("Name");
setAge(20);
setIsConsent(true);
```

</div>

<div>

```jsx
const [form, setForm] = useState({
  name: "",
  age: 18,
  isConsent: false
});

setForm({
  name: "Name",
  age: 20,
  isConsent: true
});

```

</div>

</div>

---
layout: default
---

# useState - lazy initialization

use lazy initialization to avoid re-calculate expensive operation

<div grid="~ cols-2 gap-4">
<div>

```jsx
const [count, setCount] = useState(0);
const [cache] = useState(createExpensiveCache());
```

</div>

<div>

```jsx
const [count, setCount] = useState(0);
const [cache] = useState(createExpensiveCache);
```

</div>

</div>

---
layout: default
---

# useState - updater

use updater function to avoid unneccessary dependency

<div grid="~ cols-2 gap-4">
<div>

```jsx {all|3,8,12}
const [count, setCount] = useState(0);
function increment() {
  setCount(count + 1);
}

useEffect(() => {
  const intervalId = setInterval(() => {
    setCount(count + 1); 
  }, 1000);

  return () => clearInterval(intervalId);
}, [count])
```

</div>

<div>

```jsx {all|3,8,12}{at:2}
const [count, setCount] = useState(0);
function increment() {
  setCount(c => c + 1);
}

useEffect(() => {
  const intervalId = setInterval(() => {
    setCount(c => c + 1); 
  }, 1000);

  return () => clearInterval(intervalId);
}, [])
```

</div>

</div>

---
layout: default
---

# useState - update in render

It's okay to update state while rendering as long as you have the bailout condition. React will batch the changes and commit it in one go.

<div grid="~ cols-2 gap-4">
<div>

```jsx {all|5-7}
function Form() {
  const [name, setName] = useState("");
  const [cache, setCache] = useState("");

  useEffect(() => {
    setCache(name);
  }, [name]);
}
```

</div>

<div>

```jsx {all|5-7}{at:1}
function Form() {
  const [name, setName] = useState("");
  const [cache, setCache] = useState();

  if (cache !== name) {
    setCache(name);
  }
}
```
</div>
</div>


---
layout: default
---

# useState - group state together

Combine related pieces of data for better readability. It makes your code easier to understand at a glance.


<div grid="~ cols-2 gap-4">
<div>

```jsx
function Form() {
  const [name, setName] = useState("");
  const [age, setAge] = useState(0);

  return (
    <form>
      <input
        value={name}
        onChange={e => setName(e.target.value)} />
      <input
        value={age}
        onChange={e => setAge(e.target.value)} />
    </form>
  );
}
```

</div>

<div>

```jsx
function Form() {
  const [form, setForm] = useState({ name: "", age: 0 });
  const onChange = (e) => setForm({
    ...form,
    [e.target.name]: e.target.value
  })

  return (
    <form>
      <input value={name} name="name" onChange={handleChange} />
      <input value={age} name="age" onChange={handleChange} />
    </form>
  )
}
```
</div>
</div>


---
layout: default
---

# useState - Not everything is a state

- Don't store calculable values in state. 
- Derive values from existing state.

<div grid="~ cols-2 gap-4">
<div>

```jsx
const [search, setSearch] = useState("");
const [countryList, setCountryList] = useState([]);
const [filteredCountryList, setFilteredCountryList] = useState([]);

useEffect(() => {
  setFilteredCountryList(
    countryList
      .filter(country => country.name.includes(search))
  );
}, [countryList, search]);
```

</div>

<div>

```jsx
const [search, setSearch] = useState("");
const [countryList, setCountryList] = useState([]);
const filteredCountryList = countryList
  .filter(country => country.name.includes(search))
```
</div>
</div>

