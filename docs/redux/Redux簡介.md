# Redux

Redux 是一個可預測狀態的"容器"

## 設計理念

> Single source of truth，單一真相，表達資料來源的單一，使用一個 JS 物件來表述全部狀態。

```js
// 獲取當前應用狀態
let state = store.getState();
```

> State is read-only，表示狀態結果是唯讀的，我們不能直接改變它。唯讀並非無法改變，而是當頁面需要新的資料狀態時，再生成一棵全新的狀態樹

使用 dispatch (派發) 一個 action (動作/事件)，action 其實也是 JS 物件，就像頁面狀態資料樹這個 JS 物件描述整個頁面狀態，action 則描述這個動作單元的變化。

> Changes are made with pure function called reducer。

使用 reducer 函式來接收 action，並執行頁面狀態資料樹變更，經 reducer 處理後，`store.getState()` 方法會回傳薪頁面資料狀態。當然，當前頁面是唯讀的，經過 reducer 處理後，回傳一個新的 JS 物件，而不會對原回傳值進行更改。所以 reducer 並不直接更改頁面狀態資料樹

```js
function reducer() {
  let state = getState();
  state.foo = 'bar'
}
```

根據當前頁面狀態資料樹，結合描述改變資訊的 action，產生一棵新的頁面狀態資料樹，並把它應用在 store.getState() 當中。

reducer 與 action 都需要開發者撰寫，reducer 接收以下兩個參數

- 當前頁面資料狀態
- 被派發的 action

所以這個函式處理可以被抽象表達:

```js
(previousState, action) => newState
```

d