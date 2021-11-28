# [Next] SSR 、 SSG 和 CSR

Next 是一個基於 React 的框架，然而 React CSR (Client-Side-Rendering) 不利於 SEO ，因此為了解決這個問題，我們可以使用 SSR (Server Side Rendering) 來解決此問題。

而 Next.js 提供了 SSR 和 SSG (Static-Side-Generation) 兩種 render 方式，SSR 可用在內容很常改動，需要 API 時常支援變動的頁面，而 SSG 可以用在內容較不常變動的頁面。

## CSR

CSR 即在client 端 browser 使用 javascript 將畫面所需塞入 html 特定的某個 dom 裡面，就例如 React 會固定有一個 id 為 root 的 div 讓我們將其他元素利用 javascript 放入此 div。

所以打開 index.html 之類的檔案只會看到:

```html
<body>
  <div id = 'root' />
</body>
```

### CSR 優點

- 載入後的後續渲染畫面不用不斷與伺服器交互，體感比 SSR 快。
- 對伺服器負擔較少。

### CSR 缺點

- 第一次請求伺服器所得到的 HTML 檔基本上沒有內容，不利於 SEO。

## SSR

傳統的 SSR 為透過後端處理任何資料在編譯成 HTML 再讓使用者拿到完整的 HTML ，但是這樣做就可以看到畫面明顯的閃動，後來在 SPA 的流行下可以做到像是 SPA 的換頁不閃爍再加上第一次就從伺服器拿回完整的 HTML 利於 SEO。

### SSR 優點

- 可以拿回完整的 HTML 利於 SEO。

### SSR 缺點

- server 需要不斷處理來自使用者的請求，回傳 HTML。

## SSG

SSG 會將所有內容在 bundle 時打包進檔案中，所以使用者可以拿到完整的 HTML ，每次拿到的 HTML 內容也不會變，很適合使用在資料變動較少的頁面上。

### SSG 優點

- 解決 SEO 問題。
- server 不用一直處理來自使用者的請求。
- 可以將預先生成的 HTML 放在 CDN 上加快使用者端畫面呈現。

### SSG 缺點

- 使用者都會得到一樣的畫面，較難達成像是客戶資料頁面的客製化。

## Reference

[Day03 - 深入淺出 CSR、SSR 與 SSG](https://ithelp.ithome.com.tw/articles/10266781) @ it邦幫忙

[Client Side Rendering vs. Server Side Rendering vs. Static Site Generation](https://www.section.io/engineering-education/client-side-rendering-vs-server-side-rendering-vs-static-site-generation/)