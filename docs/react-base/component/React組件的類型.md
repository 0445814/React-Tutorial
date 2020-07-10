# react組件的類型

按寫法分，react組件主要分為三種，分別是`傳統組件( createClass )`、`類組件(class component)`、`函數組件(function component)`。

如果按功能分，又可以分為很多種，比如`頂層組件`、`布局組件`、`容器組件( container component )`、`展示組件(show component)`等等。
  
## 按寫法劃分
### 一，傳統組件  createClass

傳統組件是react最初創建組件的方式，它主要透過調用`React.createClass`方法來創建組件。它需要你傳入組件的相關配置訊息，比如`render`方法等等。

但目前傳統組件已經被淘汰，`react v16`以後不再支持。
下面是一個傳統組件:
```js
// 傳統組件
var App = React.createClass({
    render:function(){
        return (
          <div>hello，這是一個類組件</div>
        );
    },
});
ReactDOM.render(
        <App />,
        document.getElementById('content')
);
```

### 二，class類組件  Class Component  
類組件顧名思義是透過class類來創建的組件。它依賴於class語法。下面是一個class組件:
```js 
// 類組件定義  
// React.Component是react提供的用於創建類組件的基類
class App extends React.Component {  
    // ...做一些事情
    render(){
        return (<div>
            hello，這是一個類組件
        </div>)
    }
}
```
> 類組件內必須要有render方法，並返回jsx


### 三，函數組件 - Fuction Component  
函數組件非常簡單，一個函數內返回jsx，這個函數就是一個函數組件。  
> 函數組件本身沒有生命週期，但react hook出來以後，函數組件也能使用生命週期。  

```js 
// 函數組件定義
const App =(props)=>{  

    // ...做一些事情
    return (<div>
        hello，這是一個類組件
    </div>)
}
```

## 按功能劃分  
##### 頂層組件 和 布局組件
```js
  // <App>為頂層組件，Header、Content、Footer為布局組件
  <App>
    <Header />
    <Content />
    <Footer />
  </App>
```  

##### 容器組件 和 容器子組件
容器組件就是一個模組級別的包裝組件，非容器組件就是容器組件的子組件
```js
  //  用戶首頁模組，UserPage是容器組件，UserProfile和UserWork則是容器組件的子組件
  <UserPage>
    <UserProfile />
    <UserWork />
  </UserPage>
```

##### 展示組件  
純展示組件，沒有交互性。
```js
  //  展示組件
  <UserProfile>
    <ProfileCard />
  </UserProfile>
```
