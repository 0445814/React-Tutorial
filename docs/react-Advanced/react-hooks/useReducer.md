# useReducer - 複雜的狀態管理    

useReducer 是 useState 的變體，用於處理複雜的狀態管理。

useReducer 可以作為 useState 的一種替代方案，它的靈感來自於redux的reducer。  

### 基本使用
useReducer主要接受三個參數，下面是useReducer的基本用法：  
```js
// useState基本用法
const [state, setState] = useState(initialState);  

// useReducer 基本用法
const [state, dispatch] = useReducer(reducer, initialState,initialAction);
```      
參數：    

> 1，reducer是一個函數，用於處理action並更新state   

> 2，initialState為初始的state    

> 3，initialAction為useReducer初次執行時被處理的action

返回值：    

> 1，state為狀態    

> 2，dispatch為更新state的方法，它接受action作為參數    
    
<br/>

#### 如何用useReducer更新state ？   
只需要調用`dispatch(action)`方法即可更新state。 
```js
dispatch({ type: "reset" })
```
> dispatch用於更新state，當`dispatch(action)`被調用時，reducer方法也會被調用，並會根據action的描述去更新state。

<br/>

### reducer 參數詳解 

在了解參數reducer之前，我們先來了解action是什麼。

##### 1，action   

action是一種動作的描述，描述你發出的這個動作它應該做的事情。

action本質是一個對象(object)，它通常有一個`type`屬性，用於描述該如何更新state，此外你還可以攜帶其他的參數。  

下面是action的一個例子：   

```js
const action = { 
    type: 'increment',  // 增量，表示該state的值要增加
    payload:{ 
        other: "value"  // 攜帶的其他參數
    } 
} 
```

我們該如何把描述性的action轉換為最新的state ？這就是reducer函數所做的事情了。

##### 2，reducer   

reducer是redux的產物，它本質上是一個函數，主要用於處理action，並它返回最新的state。   

總的來說，reducer是action和state的轉換器，它根據action的描述，去更新state。

它的結構如下：  
```js
(state, action) => newState
```

下面是reducer的一個應用案例：   
```js
const initialState = { count: 0 };  // 初始state

const reducer = (state,action) =>{  

    // 變數action，更加action的描述去更新state
    switch (action.type) {   

        // 當type為reset時，重設state的值，讓state等於初始state
        case 'reset':    
            return initialState;  

        // 當type為increment時，讓count加一
        case 'increment':
            return {count: state.count + 1};  

        // 當type為decrement時，讓count減一
        case 'decrement':
            return {count: state.count - 1};    

        // 當type不屬於上面任何一個時，不做任何更改，返回當前的state
        default:
            return state;
    }
}

const MyCompoent = () =>{

    const [state, dispatch] = useReducer(reducer, initialState);  

    return (
        <div>
            <p>當前count的值為：{ state.count }</p>
            <p><button onClick = {()=>dispatch({ type: 'reset' }) } >重設</button></p>
            <p><button onClick = {()=>dispatch({ type: 'increment' }) } >加一</button></p>
            <p><button onClick = {()=>dispatch({ type: 'decrement' }) } >減一</button></p>
        </div>
    )
}
```

### 結合useContext  

useContext可以解決組件間的數據共享的問題，而useReducer則解決了複雜狀態管理的問題，因此把他們結合起來之後，我們就可以實現redux的功能了。那也意味著我們可以不再依賴第三方狀態管理器。


