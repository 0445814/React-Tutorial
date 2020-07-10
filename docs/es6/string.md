# 模板字串

### 基本使用
  模板字串是對字串的一種拓展，它使用``符號定義字串，並且在字串內可通過`${ ... }`來使用js表達式。
```js
 const user = { name:"ben", age:23, gender:"男" };   

 let usermsg = `我叫${ user.name }，今年${ user.age }歲，性別${ user.gender }。`;

 console.log(usermsg); // "我叫ben，今年23歲，性別男"  

```  

相當於：  

```js
const user = { name:"ben", age:23, gender:"男" };  
  
// 傳統寫法
let usermsg = '我叫'+user.name+'，今年'+user.age+'歲，性別'+user.gender+'。';
``` 

### 應用案例:

```js

class App extends Components {
    render(){
        const user = { name:"ben", age:23, gender:"男" };
        let usermsg = `${user.name}，${user.age}歲，${user.gender}`;
        return <div>
           當前用戶：{ usermsg }
        </div>
    }
}

// 上面渲染結果:    

 當前用戶: ben，23歲，男
```