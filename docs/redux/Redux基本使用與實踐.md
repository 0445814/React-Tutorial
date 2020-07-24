# Redux基本使用與實踐

store 是 Redux 的核心，並且是一個 JS 物件，裡面包含了 dispatch 及獲取頁面狀態資料樹的方法等。

```js
store = {
  dispatch,
  getState,
  subscribe,
  replaceReducer
}
```

## store 提供的方法

- dispatch(action): 派發 action。
- subscribe(listener): 訂閱頁面資料狀態，即 store 中 state 的變化。
- getState: 獲取當前頁面狀態資料樹，即 store 中 state。
- replaceReducer(nextReducer): 一般開發用不到，社區一些熱更新或程式碼分離技術中可能會使用到。

## 建立 state

使用 Redux.createStore 建立頁面應用的 store，即產生一個物件實例

```js
import { createStore } from 'redux';
const store = createStore(reducer, preloadedState, enhancer);
```

createStore 方法接收三個參數

- reducer: 為開發者撰寫的 reducer 函式，必須。
- preloadedState: 頁面狀態資料樹的初始狀態，可選。
- enhancer: 增強器，函式類型，可選。

其中 reducer 參數必須存在。意即當開發者建立一個 store 時，必須同時定義好 reducer 函式，用來告知 store 資料狀態如何根據 action 進行變更。

在正常開發中，我們只需要關心前兩個參數來建立 store 就夠了。在 Redux 應用架構中，store 必須是唯一的。這也是 Redux 區別於 Flux 等架構的一個顯著特點

