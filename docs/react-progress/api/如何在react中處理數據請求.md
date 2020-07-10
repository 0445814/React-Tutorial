# 如何在react中處理數據請求 ？
數據層是必不可少的，在react中你可以很靈活地處理你的數據。  

### 在組件內部處理
在組件內處理數據請求，通常適用於那些簡單而不複雜的應用。   
##### 1，class組件  
在class組件內處理數據請求的話，通常需要在`componentDidMount`生命週期方法內處理。

下面是一個例子：
```js
class App extends React.Component {  
    
    // 1，聲明初始state
    state = {
        data: null
    }
    
    // 2，請求並更新數據
    componentDidMount(){
        // ...ajax請求...
        // 更新數據
        if(data){
            this.setState({ data });
        }
    }

    render(){
        // 3，渲染數據
        const { data } = this.state;
        return (
            <div>
                { data }
            </div>
        )
    }
}  
```

##### 2，函數組件    

函數組件本身沒有生命週期，但是我們可以借助`react hook`中的`useEffect`來處理數據請求。

函數組件的`useEffect`相當於class組件的`componentDidMount`。
```js
import React,{ useState, useEffect } from 'react';  

export default () =>{     

    // 1，聲明初始state
    const [ data, setData ] = useState(null);
    
    // 2，請求並更新數據
    useEffect(async ()=>{
        // ...ajax請求...
        // 更新數據
        if(result){
            setData(result.data);
        }
    })
   
    // 3，渲染數據
    return (
        <div>
            { data }
        </div>
    )
}
```

### 在組件外部處理

在react中，數據也是一種`state(狀態)`。

使用react做開發，通常中大型複雜應用都需要用到第三方狀態管理器，比如redux、mobx、dva等等。

而這些狀態管理器相應地擁有非常強大的數據管理能力，於是通常組件的數據層交由這些狀態管理器來管理。

以`dva`為例，`dva`提供了一個`model`模組專門用於處理組件外部狀態的(含數據層)。  

下面是一個案例，使用`dva`來管理`用戶訊息`數據，我們來看`dva`是如何管理這些數據的：  

1，添加數據請求函數：
```js
// 請求函數 - 請求用戶訊息
const fetchUser => () =>{
   return fetch("/api/user").then(res=>res.json());
}
```
2，dva 的 `model層`中處理數據請求和更新：
```js
app.model({
  namespace: 'usermodel',
  state: {
    user: null
  },
  // effects為副作用，專注於數據處理
  effects: {
    *getUser(action, { call, put }) {
      //1， 調用fetchUser請求函數，向後台請求用戶數據
      const user = yield call(fetchUser, 1000);
      //2， 更新user
      yield put({ type: 'updateUser',payload: { user }})
    },
  },
  reducers: {
    updateUser(state,action) {
      //3， state為舊的state，這裡被新的state覆蓋
      return { ...state, ...action.payload };
    },
  },
  subscriptions: {
    // 訂閱
  },
});
```
3，dva的state同步更新到react組件
```js
// dva 的 connect 方法可以將組件和數據關聯在一起
import { connect } from 'dva';  

// MyComponent為react組件，透過connect方法從dva裡面獲取最新的state。
connect((state)=>{
   return { user: state.user }
})(MyComponent);
```

4，react組件：  
```js
class MyComponent extends React.Component {

    componentDidMount(){
        // 觸發action - "getUser"(model - effects - getUser)
        this.props.dispatch({ type:"getUser" });
    }

    render(){
        // 從dva中獲取的最新state - user
        const { user } = this.props;
        return (
            <div>
                當前登錄的用戶是：<b>{ user && user.name }</b>
            </div>
        )
    }
}
```
