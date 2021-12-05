# [Typescript] 介紹

## 甚麼是 Typescript ?

Typescript 是由 Microsoft 主打，擁有型別系統 (Type System) 和 介面 (Interface) 設計的語言，可以想像為 Typescript 是在原生的 JS 上包裝一層新語法，因此原生的 JS 在 Typescript 也是可以被編譯的，但是會幫你找出原生 JS 潛藏的 bug 或是沒有補清的邏輯。

## 優點

### 增加程式碼可讀性跟可維護性

1. 可透過型別定義就知道函式如何使用。

2. 在編譯時期就能找出大部分錯誤。

### 包容性

1. 可以良好的包容 JS ，原 .js 檔案換成 .ts 即可。

2. 可自動做出行別推論。

3. 許多第三方也都支援或是使用 ts 編寫。

4. 即便 Typescript 編譯時報錯依然可以產生 js 檔案。
  
## 缺點

### 學習成本

1. 介面 (Interface)

2. 泛型 (generics)

3. 類別 (classes)

4. 列舉型別 (Enums)

### 開發成本

因為在開發的時候需要多編寫型別定義，勢必會造成開發時的時間成本，但是對於一個長期維護的專案來講反而能減少其維護成本。

## 安裝

```bash
npm install -g typescript
```

## 環境配置

在想要使用 typescript 的專案資料夾內

```bash
tsc --init
```

這樣就會建立 typescript 設定檔 `tsconfig.json`

並且輸入 `tsc` 指令就會將所有 ts 檔案編譯為 js 檔。

## Reference 

[什麼是 TypeScript](https://willh.gitbook.io/typescript-tutorial/introduction/what-is-typescript)

[Day 02. 前線維護・型別推論 X 註記 - Type Inference & Annotation](https://ithelp.ithome.com.tw/articles/10214719)