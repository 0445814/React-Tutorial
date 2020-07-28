# Redux 基本使用與實踐

store 是 Redux 的核心，並且是一個 JS 物件，裡面包含了 dispatch 及獲取頁面狀態資料樹的方法等。

```js
store = {
  dispatch,
  getState,
  subscribe,
  replaceReducer,
};
```

## store 提供的方法

- dispatch(action): 派發 action。
- subscribe(listener): 訂閱頁面資料狀態，即 store 中 state 的變化。
- getState: 獲取當前頁面狀態資料樹，即 store 中 state。
- replaceReducer(nextReducer): 一般開發用不到，社區一些熱更新或程式碼分離技術中可能會使用到。

## 建立 state

使用 Redux.createStore 建立頁面應用的 store，即產生一個物件實例

```js
import { createStore } from "redux";
const store = createStore(reducer, preloadedState, enhancer);
```

createStore 方法接收三個參數

- reducer: 為開發者撰寫的 reducer 函式，必須。
- preloadedState: 頁面狀態資料樹的初始狀態，可選。
- enhancer: 增強器，函式類型，可選。

其中 reducer 參數必須存在。意即當開發者建立一個 store 時，必須同時定義好 reducer 函式，用來告知 store 資料狀態如何根據 action 進行變更。

在正常開發中，我們只需要關心前兩個參數來建立 store 就夠了。在 Redux 應用架構中，store 必須是唯一的。這也是 Redux 區別於 Flux 等架構的一個顯著特點

## 建構 action

action 描述了狀態變更的資訊，也就是需要頁面做出的變化，由開發者定義的 store.dispatch 派發。action 本身也是 JS 物件。

Redux 規定 action 物件需有一個 type 屬性，作為描述這個 action 的名稱來唯一確定這個 action，通常是 JS String 類型。另外，action 通常攜帶一些資料資訊，這些資訊包含了 action 的基本內容。

以下是一個標準 action，可理解為 "閱讀 Redux 書籍"，具體閱讀哪本 ? 就是 data 的 "深入淺出 1"

```js
const action1 = {
  type: "READ_REDUX_BOOK",
  data: {
    book: "深入淺出 1",
  },
};
```

## action creator (建構器)

想像一下這種情況，需要一個 type 為 READ_REDUX_BOOK 的 action，用來描述閱讀 Redux 書籍這樣的變化，但每次閱讀書籍都不同，即

```js
const action2 = {
  type: 'READ_REDUX_BOOK',
  data: {
    book: '深入淺出 2'
  }
}

const action3 = {
  type: 'READ_REDUX_BOOK',
  data: {
    book: '深入淺出 3'
  }
}

...
```

所以我們可以寫成這樣

```js
const learnReduxActionFactory = (book) => {
  type: "READ_REDUX_BOOK", book;
};
```

函式回傳一個物件，即一個 action，但是 action.type 固定為 READ_REDUX_BOOK，而攜帶資訊由參數決定，類似於一個工廠模式的生產工具，也算一種常見的最佳實踐

## 使用 dispatch 派發 action

dispatch 來自 store 物件暴露的方法，負責派發 action，這個 action 將作為 dispatch 方法的參數。

```js
store.dispatch(action1);
```

若使用 action creator

```js
store.dispatch(learnReduxActionFactory("深入淺出1"));
```

## 撰寫 reducer 函式更新資料

action 描述一種變化，並攜帶變化的資料資訊。真正執行這種變化並生成正確資料狀態的是 reducer 方法。我們了解到 reducer 必須為純函式，以保證資料的可預測性，以下是一個 reducer 函式。

```js
const updateStateTree = function (previousState = {}, action) {
  // ...
  return newState;
};
```

一個完整的 reducer 函式可能需要對多個 action 作處理，所以在開發時往往使用 switch-case 或 if-else 來撰寫:

```js
const updateStateTree = function (previousState = {}, action) {
  switch (action.type) {
    case "case1":
      return newState1;
    case "case2":
      return newState2;
    default:
      return previousState;
  }
};
```

!> 當無法匹配 action 時，預設回傳 previousState 參數，以保證其回傳值的穩定性

!> updateStateTree 函式第一個參數是 previousState = {} 表示設定了預設值代表初始狀態，預設值是一個空物件，也可根據需要合理進行設定

### 總結

當通過 Redux 的 createStore 方法建立一個 store 實例之後，便可使用 store.dispatch 派發一個描述變化的 action，這個 action 需要開發者根據業務自行撰寫。同時，執行 store.dispatch 後，Redux 會"自動"幫我們執行處理變化並更新資料的 reducer 函式。從 store.dispatch 到 reduce 的過程可以認為是 Redux 內部處理的，但具體 action 和 reducer 需要開發者撰寫，以完成應用開發。那麼當頁面狀態資料更新後，如何促使頁面發生 UI 更新呢 ? 這時就需要使用 store.subscribe(callback function) 方法訂閱資料的更新，並由 callback function 完成 UI 更新。

## 合理分割 reducer 函式

當業務變得複雜，action 會越來越多，reducer 也將變得龐大，這對於開發體驗與維護都是難以接受的

````js
const fatReducer = function (previousState = {}, action) {
  switch (action.type) {
    case: 'case1'
    // do something ...
    return newState1;
    case: 'case2'
    // do something ...
    return newState2;
    ......
    ......
    default:
      return previousState;
  }
}

為了解決這個問題，Redux 提供一個工具函式: combineReducers，可以對 reducer 函式進行分割，最後在合併一個完整的 reducer。

它接收一個 JS 物件類型參數，這個物件的鍵值分別為頁面資料狀態分片和子 reducer 函式，最後回傳一個合併歸一的 finalReducer。

```js
let finalReducer = combineReducers({reducers});
````

例如，頁面資料狀態存在三種資料狀態: data1、data2、data3，相互獨立而不關聯

```js
state = {
  data1: {
    ...
  },
 data2: {
    ...
  },
  data3: {
    ...
  },
}
```

接著把三個狀態分割成三個小的 reducer 函式: reducer1、reducer2、reducer3

```js
const reducer1 = function (previousState = {}, action) {
  // 根據 action 和 state.data1 計算產生新的 state.data1
  return state.data1;
};

const reducer2 = function (previousState = {}, action) {
  // 根據 action 和 state.data2 計算產生新的 state.data2
  return state.data2;
};

const reducer3 = function (previousState = {}, action) {
  // 根據 action 和 state.data3 計算產生新的 state.data3
  return state.data3;
};
```

最後，利用 combineReducer 將三個子 reducer 函式合併並回傳完整的 finalReducer

```js
const { combineReducers } = Redux;
const finalReducer = combineReducers({
  data1: reducer1,
  data2: reducer2,
  data3: reducer3,
});
```

在 ES6 開發環境下，常用作法是令子 reducer 函式名稱與資料狀態命名一致，即將 reducer1、reducer2 和 reducer3 分別命名為 data1、data2 和 data3。

```js
const { combineReducers } = Redux;
const finalReducer = combineReducers({
  data1: data1,
  data2: data2,
  data3: data3,
});
```

於是，可簡寫成:

```js
const finalReducer = combineReducers({ data1, data2, data3 });
```

總之，合併為一個 finalReducer，就可單獨維護這三個子 reducer，進而提升維護效率。

回頭看一下 combineReducers 方法，它接收一個 Object 類型參數，這個參數定義了頁面資料狀態中不同的資料部分與更新這些資料的 reducer 含式之間的映射關係，並最終回傳一個合併完整的 reducer 函式。

實際開發中，我們往往遵循這樣一個"最佳實踐"，將 reducer 命名為其處理的頁面狀態資料樹中的鍵值

```js
const state = {
  data1: {},
  data2: {},
  data3: {},
};
```

同時，reducer1、reducer2、reducer3 分別處理 data1、data2、data3，那我們就將 reducer 與其處理的 state 相同命名

```js
const data1 = function (state.data1, action) {
  ...
};

const data2 = function (state.data2, action) {
  ...
};

const data3 = function (state.data3, action) {
  ...
};
```

這樣做的好處是 reducer 命名更加規格和清晰，能夠準確表達其處理對應資料的意義，同時有利多人開發時的維護

在 ES6 下，可簡寫為

```js
const finalReducer = combineReducers({
  data1,
  data2,
  data3,
});
```

記得建立 store 實例的方式嗎 ? 這時可簡寫成

```js
const store = createStore(combineReducers(...), preloadedState, enhancer);

// or

const store = createStore(finalReducers, preloadedState, enhancer)
```

