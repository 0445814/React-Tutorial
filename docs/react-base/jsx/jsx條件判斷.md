# jsx條件判斷   
jsx不能直接使用if等判斷語句，但可以使用三元運算符進行判斷。  

雖然不能直接使用if等判斷語句，但我們可以變通來使用它。  

### 三元運算符
jsx中可以直接使用三元運算符進行判斷。

##### 1，普通使用
```js
const App = ({ loading }) =>{

    return <div className="wrap" >
       { loading ? <div> 載入中... </div> : null }
    </div>
}
```

##### 2，嵌套使用
```js
const UserPage = ({ user }) =>{

    return <div className="wrap" >
       { 
            user ? 
               user.email? <span> { user.email } </span> : { user.phoneNumber }
            : null 
        }
    </div>
}
```
### 使用`&&`邏輯操作符

```js
const App = ({ loading=false }) =>{
    
    return <div className="wrap" >
       { loading && <div> 載入中... </div> }
    </div>
}
```

### if判斷   
jsx不能直接使用if語句，但我們可以在jsx之前使用它，把判斷的結果賦給變數，然後再輸出到jsx中。

```js
const App = ({ user }) =>{
    let isLogin = false;
    if(user && user.id) isLogin = true;
    return <div className="wrap" >
       { isLogin ? <div> 您已登錄! </div> : <div> 請未登錄 </div> }
    </div>
}
```
