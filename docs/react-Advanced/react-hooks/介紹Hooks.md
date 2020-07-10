# 介紹Hooks

[React Hooks](https://reactjs.org/docs/hooks-intro.html)是React 16.8中新增的功能。它允許你在函數組件裡使用state和其他React功能。

### React Hooks 解決了什麼問題 ？  

#### 1，函數組件不能使用state   

在[React Hooks](https://reactjs.org/docs/hooks-intro.html)推出之前，函數組件通常只能用於一些簡單而無交互的場景，比如訊息展示。當需要交互的時候我們就得用臃腫的class組件來實現。  

在[React Hooks](https://reactjs.org/docs/hooks-intro.html)推出之後，函數組件能夠使用state功能，並且比class組件更加簡潔，更加好用。

可以預見的是，未來函數組件將會被大幅度地採用，這不僅能給我們帶來非常爽的開發體驗，同時也提高了我們的開發效率和質量。

<br/>   

#### 2，副作用的問題
通常數據獲取、訂閱、或手動修改`React DOM`這些行為，我們可以稱之為`副作用(side effect)`。

[React Hooks](https://reactjs.org/docs/hooks-intro.html)提供了`useEffect`這個API來處理組件的副作用問題。

那也就意味著你可以在函數組件內進行數據獲取、訂閱等操作。

而在class組件裡我們需要依賴`componentDidMount`，`componentDidUpdate`，和 `componentWillUnmount`這幾個生命週期方法來實現。

`useEffect`可以說是對這幾個生命週期方法的統一。  
<br/>   

#### 3，有狀態的邏輯重用的問題

在開發中我們經常會遇到一些組件復用的問題，比如公共`<Button>`、跳出視窗、布局、卡片等等，又或者說一些可復用的業務邏輯，比如數據請求、關注和取消關注等等。

[React Hooks](https://reactjs.org/docs/hooks-intro.html)可以很輕鬆地實現這些邏輯的封裝，從而達到組件復用的效果。你完全可以根據你的需要創建自訂的hooks。

簡單點說就是，React Hooks解決了代碼復用的問題。

這裡有一個[Hooks指南網站](https://www.hooks.guide)，它裡面封裝了幾十個非常好用的`hooks`，並且還在不斷地新增。

<br/>   

#### 4，複雜狀態管理的問題  

對於複雜的狀態管理，過去我們使用`redux`、`dva`、`mobx`等第三方狀態管理器來管理。  

[React Hooks](https://reactjs.org/docs/hooks-intro.html)推出之後，我們可以不再依賴這些第三方狀態管理器了，我們只需要依據React Hooks提供的API就可以實現複雜的狀態管理。  

主要就是`useReducer`、`useContext`這些API。

<br/>   

#### 5，效率和質量的問題  

[React Hooks](https://reactjs.org/docs/hooks-intro.html)是純函數式開發，相比於臃腫的class組件，函數組件開發體驗更好，開發效率更高，應用性能更好。  

[React Hooks](https://reactjs.org/docs/hooks-intro.html)擴大了函數組件的應用範圍，意味著我們可以在絕大都數應用場景使用函數組件進行快速開發。

