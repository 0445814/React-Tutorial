# useEffect - 副作用

數據獲取、訂閱、或手動修改React DOM這些行為都可以稱之為`副作用(side effect)`。`useEffect`正是用來處理這些副作用的。

同時`useEffect`也是`componentDidMount`，`componentDidUpdate`，和 `componentWillUnmount`這幾個生命週期方法的統一。

### 基本使用  
用法：
```js
useEffect(callback,array)
``` 
> 1，callback：回調函數，用於處理副作用邏輯。   

> 2，array(可選)：一個數組，用於控制執行。

```js
import { useState, useEffect } from 'react';

const Example = (props) =>{  

  const [count, setCount] = useState(0);

  useEffect(()=>{
      // 更新頁面標題
      document.title = `你點擊了${count}次`;
  },[])
  
  return (
    <div>
      <p>你點擊了{count}次</p>
      <button onClick={() => setCount(count + 1)}>
        點擊
      </button>
    </div>
  );
}
```  
<br/>   

### callback 副作用邏輯    
```js
useEffect(callback,array)
```
callback(回調函數)是`useEffect`的第一個參數，你所有的副作用邏輯都應該在這裡處理。

另外你可以在callback中返回一個函數，用於清理工作。
```js
useEffect(()=>{
    // 副作用邏輯
    return ()=>{
        // 清理工作，類似於 componentWillUnmount
    }
})
```
<br/>

### array 控制執行   
```js
useEffect(callback,array)
```
array(數組)是`useEffect`的第二個參數，它可以用於控制`useEffect`是否執行。  

主要分以下兩種情況： 

> 1，如果是空數組，則只會執行一次(初次render之後)，相當於`componentDidMount`。  

> 2，如果數組內存在值，那麼`useEffect`會在該數組發生改變後執行。    

下面是基本案例：   

```js
useEffect(()=>{
    // 該effect僅在初次渲染之後執行一次，相當於`componentDidMount`
},[])   
```

```js
useEffect(()=>{
    // 該effect會在初次渲染之後執行一次，同時當數組內的count發生改變時也會執行
    // 相當於componentDidUpdate
},[count])
```
數組內的值可以是組件的state，或者是外部傳遞的props屬性，亦或者是其他的值。   
<br/>

### useEffect 在什麼時候執行？  

**useEffect** 會在每一次`render`之後執行。包括初始`render`和更新`render`。
<br/> <br/>  

### 可以執行多個 `useEffect`嗎 ？ 

我們可以同時使用多個`useEffect`，如下：   
```js  
const App = () =>{    

    const [ user, setUser ] = useState(null);

    useEffect(()=>{
        // 初始化，獲取數據，僅執行一次
        setUser(userData);
    },[])  

    useEffect(()=>{
        // 更新數據
    })  

    return (
        <div> 
            <p> { user && user.name } </p>
            <button onClick={()=> setUser() } >點擊</button>
        </div>
    )
}
```

### useEffect 處理數據請求       
```js  
const App = () =>{    
    const [ user, setUser ] = useState(null);  

    const fetchUser = async () =>{
        const result = await fetch("./user.json").then(res=>res.json());
        setUser(result.user);
    }
    useEffect(()=>{
        fetchUser(); 
    },[])  
    return (
        <div> 
            <p> { user && user.name } </p>
            <button onClick={()=> setUser() } >點擊</button>
        </div>
    )
}
```

### useEffect清理機制       

react中有兩種常見的副作用，一種是需要清理的，一種是不需要清理的。  

> 1，網路請求、DOM修改和日誌記錄等，這些是不需要清理的。`useEffect`會自動處理。    

> 2，訂閱和取消訂閱，事件監聽和取消事件監聽，這種是需要清理的。  

下面是useEffect清理機制:

> 1，useEffect在每次執行之前都會自動清理之前的effect。   

> 2，effect中可以返回一個函數用於清理工作

