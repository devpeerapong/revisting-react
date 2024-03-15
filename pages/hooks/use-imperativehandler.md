---
layout: section
---

## useImperativeHandler


---
layout: default
---

# useImperativeHandler - Give control to parent

<div grid="~ cols-2 gap-4">

<div>

```jsx 
const [isOpenForm, setIsOpenForm] = useState(false);
const [isOpenInfo, setIsOpenInfo] = useState(false);

<button
  onClick={() => setIsOpenForm(true)}>
  Open Form
</button>
<Modal
  isOpen={isOpenForm}
  onClose={() => setIsOpenForm(false)}>
  <form onSubmit={() => setIsOpenForm(false)}>
    {/* Form Input */}
  </form>
</Modal>

<button onClick={() => setIsOpenInfo(true)}>More Info</button>
<Modal
  isOpen={isOpenInfo}
  onClose={() => setIsOpenInfo(false)}>
  {/* More info UI */}
</Modal>
```

</div>

<div>

```jsx 
const formModalRef = useRef();
const infoModalRef = useRef();

<button
  onClick={() => formModalRef.current.open()}>
  Open Form
</button>
<Modal>
  <form onSubmit={() => formModalRef.current.close()}>
    {/* Form Input */}
  </form>
</Modal>

<button onClick={() => infoModalRef.current.open()}>More Info</button>
<Modal>
  {/* More info UI */}
</Modal>
```

</div>

</div>

---
layout: default
---

# useImperativeHandler - Modal

```jsx 
const Modal = forwardRef(function Modal(props, ref) {
  const [isOpen, setIsOpen] = useState(false);

  useImperativeHandle(ref, () => {
    return {
      open() {
        setIsOpen(true)
      },
      close() {
        setIsOpen(false)
      }
    }
  }, []);

  if (!isOpen) {
    return null;
  }

  return (
    <div>
      {/* Modal UI */}
      {props.children}
    </div>
  )
})
```

