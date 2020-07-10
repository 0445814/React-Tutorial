# API統一管理
一個成熟的應用程式，通常需要統一管理API，這樣有利於我們協作開發和維護。  

### 封裝請求方法   

首先，我們需要封裝一個統一的請求方法。  

不管是`fetch`還是`axios`，它們請求的配置方式都是差不多的，因此我們可以對它們進行一些封裝以達到代碼復用。

##### 1，封裝`fetch`請求方法  
```js
// request.js
export default ({ url, method, headers, data },options={})=>{
    return fetch(url,{
        // *GET, POST, PUT, DELETE。
        method: method||'GET', 
        // 發送給後台的數據
        body: data ? JSON.stringify(data) : null, 
        // 請求頭
        headers: headers || {
            'content-type': 'application/json'
        },
        mode: 'cors', // 跨域處理
        ...options    // 其他配置項
    }).then(res=>res.json());
}
```
使用案例：  
```js
import request from './utils/request';  

const result = request({ url: "/api/user", data: { id: "userId" } });
```

##### 2，封裝`axios`請求方法  
```js
// request.js
export default ({ url, method, headers, data },options={})=>{
    return axios(url,{
        // *GET, POST, PUT, DELETE。
        method: method||'GET', 
        // 發送給後台的數據
        data, 
        // 請求頭
        headers: headers || {
            'content-type': 'application/json'
        },
        ...options    // 其他配置項
    })
}
```
使用案例：  
```js
import request from './utils/request';  

const result = request({ url: "/api/user", data: { id: "userId" } });
```


### 集中管理請求API  

如果我們將各個請求分散在每個組件中定義，這樣是非常麻煩和難以維護的。因此比較好的做法是將它們集中起來管理，方便開發和維護。  

通常我們可以按功能模組來管理。比如用戶模組的請求函數，單獨寫在一個`user.js`模組裡面。

下面是一個案例：  

```js
// 用戶請求模組
// services/user.js
import request from '../utils/request';  

export default class user {   

    // 獲取所有用戶
    static gets(){
        return request({
            url: "/api/user"
        })
    }  

    // 獲取指定用戶
    static get(id){
        return request({
            url: `/api/user/${ id }`
        })
    }   

    // 新增用戶
    static create(data){
        return request({
            url: "/api/user",
            method: 'POST',
            data
        })
    }   

    // 更新用戶訊息
    static put(id,data){
        return request({
            url: `/api/user/${ id }`,
            method: 'PUT',
            data
        })
    }   

    // 刪除用戶
    static delete(id){
        return request({
            url: `/api/user/${ id }`,
            method: 'DELETE'
        })
    }
}
```

基本使用：  
```js  
import userapi from '../services/user';  

class UserPage extends React.Component {

    state = {
        user: null
    }

    async componentDidMount(){
        // 調用請求函數
        const user  = await userapi.get("userid");
        if(user){
            this.setState({ user });
        }
    }   

    render(){
        const { user } = this.state;
        return (
            <div>
                當前用戶是：<div> { user && user.name } </div>
            </div>
        )
    }
}
```
