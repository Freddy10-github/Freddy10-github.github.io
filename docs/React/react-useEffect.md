# [React] useEffect

## 特性

處理各式各樣的 side effect，在 React 當中 fetch API data 、事件監聽、setInterval 甚至是手動更改 Dom 這種得對於 React 都算是 side effect。

>如果您熟悉 React 生命周期方法，則可以將 useEffect Hook 視為componentDidMount，componentDidUpdate 和 componentWillUnmount 的組合。 --[使用 Effect Hook](https://zh-hant.reactjs.org/docs/hooks-effect.html)

## 語法

```javascript
useEffect(() => {
  // do something...
}, []);
```

useEffect 可以傳入兩個參數，第一個為要執行的 callback function，第二個則是 dependency array。

### dependency array

dependency array 有三種狀況，分別會在不同的時機點觸發。

#### 不放值

若是不填入任何值，會在 render 和每次 component re-render 時呼叫。

```javascript
useEffect(() => {
  // do something...
});
```

#### 空陣列

只有第一次 render 會呼叫 callback 函式。

```javascript
useEffect(() => {
  // do something...
}, []);
```

#### 陣列內有值

在第一次 render 和陣列內的元素值變更時呼叫。

```javascript
useEffect(() => {
  // do something...
}, [data]);
```

## 對應的 life cycle

- componentDidMount

  將 dependency array 設為空陣列，表示只會在第一次 render 後觸發。

- componentDidUpdate

  將 dependency array 設值，會在第一次 render 以及內容值變化時觸發。

- componentWillUnmount

  當component要unmount的時候，會執行return內的程式。

### componentWillUnmount

當我們在 useEffect 裡執行事件監聽或是 setTimeout 、 setInterval，會需要加上 return 清除 effect (removeEventListener 、 clearInterval)，避免多次觸發 effect 不斷疊造成 memory leak

```jsx
useEffect(() => {
    // ...
    return () => {...};
}, [data])
```

## 甚麼是 effect?

在 React 當中，尤其是 hook 發布的之後， React 應該更希望開發者使用 functional programming 開發，而 useEffect 就是為了處理各種 side effect 的 hook，我認為因此 functional component 作為 pure function ，主要的工作因該是負責`渲染畫面`，因此 fetch data 這件事在很多範例中都會被寫到 useEffect 執行。

## Reference

[[Day 17 - 即時天氣] 頁面載入時就去請求資料 - useEffect 的基本使用](https://ithelp.ithome.com.tw/articles/10224270) @ iT邦幫忙

[Day3-React Hook 篇-認識 useEffect](https://ithelp.ithome.com.tw/articles/10265945) @ iT邦幫忙

[探討React的side effects](https://blog.yyisyou.tw/a96774ca/)

[React memory leak — 記憶體洩漏](https://medium.com/coding-hot-pot/react-memory-leak-%E8%A8%98%E6%86%B6%E9%AB%94%E6%B4%A9%E6%BC%8F-55390c460730)

[What the React? Sagas and side effects](https://smartcar.com/blog/what-the-react-sagas/)
