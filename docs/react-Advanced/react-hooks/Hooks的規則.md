# hooks的規則

Hooks 是 JavaScript 函數，但在使用它們時需要遵循一些規則。

### 只在頂層調用Hooks

儘量在頂層作用域中調用Hooks。

不要在循環，條件或嵌套函數中調用Hook，否則可能會無法確保每次組件渲染時都以相同的順序調用Hook。

### 只在函數組件中調用Hooks

React Hooks目前只支持函數組件，因此你不能在class組件中調用它API，但你可以在class組件內調用react hooks組件。  

下面是React Hooks的應用場景：

> 1，函數組件    

> 2，自訂hooks (在自訂的hooks中調用hooks)

在未來，react官方計劃將`React Hooks` 拓展到class組件，到時候class組件也能使用`React Hooks`。
