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

reducer 命名由來，與 JS 的 reduce 方法有關(巧合?)。reduce 方法是一種運算合成，它經過遍歷、變形、累積，將陣列所有成員"累積"成為一個值。

MDN 描述更為直接: 對累加器和陣列中每個值(左到右)應用一個函式，將其減少為單個值

在 Redux 資料流中，reducer 在具備初始狀態下，每一次運算其實都是根據之前的狀態 (previous state) 和現有的 action (current action) 來更新 state 的，這個 state 可以理解為上文中累加器的結果。每次 reducer 被執行時，state 和 action 都被傳入，這個 state 根據 action 進行累加，進而回傳新的 state。符合一個 典型 reducer 函式用法和思想，也是函數式開發的一個重要概念和體現。

