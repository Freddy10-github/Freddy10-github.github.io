# [CSS] CSS 階層效能建議

## 瀏覽器執行步驟

1. HTML 解析成 DOM 樹狀結構
2. CSS 解析成 CSSOM  樹狀結購
3. DOM 樹狀結構和 CSSOM 樹狀結構合併為轉譯的樹狀結購
4. 對轉譯樹進行 Layout 配置， 計算每個節點的幾何形狀、位置
5. 繪製節點

### DOM & CSSOM

瀏覽器在執行的時候會將 HTML 跟 CSS 各自轉譯成 DOM 和 CSSＯＭ，

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/186ea662-e405-494a-a0df-f56c1ef955c3/Untitled.png)

## 生成轉譯樹(render tree)

生成轉譯樹首先會從 DOM 的樹狀結購開始，會選出每一個 **可見** 的節點，像是 head 裡面的 meta 或是 link 就會被忽略，而在 CSS 中被寫成 `display: none;`這種也會被忽略。

> **Note:** 順帶一提，請注意「visibility: hidden」和「display: none」不同。 前者會隱藏元素，但這個元素仍會佔據版面配置中的相應空間 (其實就是一個空白方塊)；而後者 (display: none) 會直接從轉譯樹狀結構中徹底移除元素，該元素不僅會消失，而且也不再屬於版面配置的一部分。
>

接下來會為每一個節點配對上 CSSOM 的樣式，而需要注意的地方就在這邊

```css
body header a li .item{   
 padding:4px;
}

a .item{   
 padding:4px;
}
```

以上面這個例子來看，就 Google 的解釋而言，其實第二種的指定 CSS 方法會比第一種好，原因就是 render tree 在配對 CSSOM 的時候寫越多的 CSS selector 其實就代表瀏覽器要訪問的節點越多。

看下圖可以看到，在不同 CSS selector 的匹配下所花費的時間。

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e3ca57b9-d347-4e31-8df8-e56ac9317cd6/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a39e0bb9-bbee-43b6-9e4c-f007a326b5fa/Untitled.png)

最後就是將所有東西 render 上瀏覽器。

## 計算版面配置

render tree 有所有的樣式資訊後，就會進行版面配置的階段，瀏覽器會從 render tree 的 root 開始瀏覽，計算所有元素在瀏覽器上的樣式跟位置

## 如何改善

其實最好的方式就是一個 component 就有一個專屬的 class 去渲染樣式，而 Google 建議的最基本的做法就是使用 BEM 做 class 的 naming rule。
