# [React] useRef

## 特性

useRef 每一次都匯回傳相同的值，並且當被改變的時候並不會觸發 re-render。

### 功用

- 操作 DOM 元素
- 取得先前 state
- 條件避免 re-render

### 操作 DOM 元素

```jsx
export default function App() {
  const inputRef = useRef(null);
  const handleClick = () => {
    inputRef.current.value = 123;
  };
  return (
    <div className="App">
      <input ref={inputRef} />
      <button onClick={handleClick}>Click</button>
    </div>
  );
}
```

![basic-useRef](/img/react/useRef/useRef-basic.gif)

另外也可以透過 children 獲得子元素。

```jsx
export default function App() {
  const inputRef = useRef(null);
  const handleClick = () => {
    console.log(inputRef.current.children[0]);
  };
  return (
    <div className="App">
      <div ref={inputRef}>
        <span>123</span>
        <h1>hello</h1>
      </div>
      <button onClick={handleClick}>Click</button>
    </div>
  );
}
```

![basic-children](/img/react/useRef/useRef-children.gif)

### 取得先前 state

[如何取得先前的 prop 或 state？](https://zh-hant.reactjs.org/docs/hooks-faq.html#how-to-get-the-previous-props-or-state)

### 條件避免 re-render

```jsx
export default function App() {
  const [count, setCount] = useState(0);

  const isFirstRun = useRef(true);
  useEffect(() => {
    // 第一次執行 useEffect 就直接 return 掉，不執行後面的程式碼
    if (isFirstRun.current) {
      isFirstRun.current = false;
      return;
    }

    console.log("Effect was run");
  });

  return (
    <div>
      <p>Clicked {count} times</p>
      <button
        onClick={() => {
          setCount(count + 1);
        }}
      >
        Click Me
      </button>
    </div>
  );
}
```

## Reference

[Day4-React Hook 篇-認識 useRef & useImperativeHandle](https://ithelp.ithome.com.tw/articles/10266635) @ iT邦幫忙

[useRef](https://zh-hant.reactjs.org/docs/hooks-reference.html#useref) @ [React Hooks API 參考](https://zh-hant.reactjs.org/docs/hooks-reference.html#useref)
