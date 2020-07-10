# fetch和axios
[fetch](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API)和[axios](https://github.com/axios/axios)都是非常優秀的用於請求數據的API，不同在於，fetch是原生的API，[axios](https://github.com/axios/axios)則是基於ajax封裝的一個模組。

### 基本使用

##### 1，class組件    

在class組件內處理數據請求的話，通常需要在`componentDidMount`生命週期方法內處理。

下面是一個例子：
```js
import axios from 'axios';  

class UserPage extends React.Component {  
    
    // 1，聲明初始state
    state = {
        user: null
    }

    // 2，請求並更新數據
    async componentDidMount(){  

        // 使用fetch
        const user = await fetch("/api/user").then(res=>res.json());  
        if(user){
            this.setState({ user });
        }

        // 使用axios
        const result = await axios("/api/user");  
        if(result && result.data){
            this.setState({ user: result.data });
        }
        
    }

    render(){
        // 3，渲染數據
        const { user } = this.state;
        return (
            <div>
                當前登錄用戶是：<b> { user && user.name } </b>
            </div>
        )
    }
}  
```

##### 2，函數組件    

函數組件中我們可以借助`react hook`的`useEffect`來實現生命週期，然後我們就可以使用`async/await`請求數據。

```js
import React,{ useState, useEffect } from 'react';  

export default () =>{     

    // 1，聲明初始state
    const [ user, setUser ] = useState(null);
    
    // 2，請求並更新數據
    useEffect(async ()=>{

        // 使用fetch
        const result = await fetch("/api/user").then(res=>res.json());  
        if(result){
            setUser({ user: result });
        }

        // 使用axios
        const result = await axios("/api/user");  
        if(result && result.data){
            setUser({ user: result.data });
        }

    })
   
    // 3，渲染數據
    return (
        <div>
            當前登錄用戶是：<b> { user && user.name } </b>
        </div>
    )
}
```
