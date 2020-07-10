# useContext - 上下文   

[useContext](https://reactjs.org/docs/hooks-reference.html#usecontext)是為了方便我們使用[context](https://reactjs.org/docs/context.html)而提出的一個API。

### context 

通常我們可以使用第三方狀態管理器來實現全局數據共享，管理狀態，比如redux、dva、mobx。

而context(上下文)是react提供的一個用於實現數據共享的API。它可以解決需要通過多層嵌套傳遞props的問題。  

主要通過以下三步：  
> 1，通過React.createContext()創建Context對象    

> 2，使用Context.Provider包裹組件，給它的後代組件提供數據   

> 3，Context.Provider所有的後代組件，都可以通過Context.Consumer獲取Context數據

下面是context的一個使用案例：   

1，創建Context
```js
const Context = React.createContext();
```    

2，使用Context.Provider包裹組件  

```js
<Context.Provider value = { store } >
    <MyComponent />
</Context.Provider>
```  

3，使用Context.Consumer獲取共享的數據

```js
// MyComponent組件  
<Context.Consumer>
   {value =>{
       // value就是通過context共享的數據，這裡是store
       // ...
   }}
</Context.Consumer>
```  

### useContext(context)  

`useContext(context)`是針對`context`(上下文)提出的一個API，它接受`React.createContext()`的返回值作為參數，也就是context對象，並返回最近的context。

使用useContext將不再需要Provider和Consumer。

當最近的`context`更新時，那麼使用該context的hook將會重新渲染。

### 基本使用  
```js
const Context = React.createContext({ loading: false , name: "jack" });

// 組件1
const OnePage = () =>{

    const ctx = useContext(Context);

    return (
        <div>
            { ctx.loading && "Loading..." }
        </div>
    )
}


// 組件2
const TwoPage = () =>{

    const ctx = useContext(Context);

    return (
        <div>
            { ctx.name && ctx.name }
        </div>
    )
}
```
