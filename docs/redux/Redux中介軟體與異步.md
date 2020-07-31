# Redux 中介軟體與異步

Redux 提供了一套中介軟體 (Middleware) 機制，開發者可以在派發任何一個 action 和執行 reducer 這兩步之間，增加自訂擴展功能。

我們可以使用 Redux 中介軟體來完成日誌紀錄、呼叫異步介面或路由等。

Redux 本身提供了 applyMiddleware 方法來接入中介軟體，建立 store 實例的過程如下

```js
const store = createStore(reducer, preloadedState, enhancer);
```

可以在 enhancer 參數的位置接入中介軟體，createStore 可以接收 applyMiddleware(...middlewares) 作為參數，建立一個應用中介軟體的 store

```js
const store = createStore(
  reducer,
  preloadedState,
  applyMiddleware(middleware)
);

// or

const sotre = createStore(
  reducer,
  applyMiddleware(middleware)
)
```

## 應用 redux-logger 中介軟體

社區中的 redux-logger 中介軟體來進行日誌記錄。每一次派發前後的頁面資料狀態，以及當前所派發的 action，都能在瀏覽器 console 中印出來，方便開發除錯

```js
// 需先安裝再引入
import createLogger from 'redux-logger';
```

利入 applyMiddleware 和 createStore 接入中介軟體

```js
import { applyMiddleware, createStore } from 'redux'

const logger = createLogger();

const store = createStore(
  reducer,
  applyMiddleware(logger)
)
```

這裡在 createStore 中省略了 preloadedState 參數。如果需要在建立 store 時進行 store 狀態的初始化，那麼需要調整 createStore 函式，applyMiddleware(...arguments) 將會作為第三個參數出現

```js
const store = createStore(
  reducer,
  preloadedState,
  applyMiddleware(logger)
)
```

這樣就接上 redux-logger 中介軟體，可以前往官網或打開瀏覽器 console

## 應用 redux-thunk 中介軟體
