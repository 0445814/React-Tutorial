# react組件通信方式  
react組件之間往往需要進行通信，比如傳遞參數，傳遞數據等等。組件會發生以下三種通信:  
* 向子組件通信
* 向父組件通信
* 向其他組件通信

### 一，向子組件通信  
react是單向數據流，也就是自上而下傳遞數據。因此父組件可以通過props傳遞參數給子組件，下面是一個例子：
```js
// App是父組件，Header是子組件，App傳遞了user給子組件Header
const App = () =>{
    const { user } = props;
    return <div>
        <Header user={ user } />
    </div>
}

// 子組件Header，透過props獲取到父組件傳遞過來的user
const Header = (props) =>{
    const { user } = props;
    return <div>
        { user && user.name }
    </div>
}
```

### 二，向父組件通信 
react子組件無法向父組件傳遞props，但我們可以透過一些特別的手段，來實現自下而上的反向數據流。

如何實現？ 我們可以從父組件傳遞一個callback(回調函數)給子組件，子組件調用這個callback並傳遞參數，從而實現子組件向父組件傳遞數據，也就是react的反向數據流。  

```js
// 父組件Form
class Form extends React.Component { 

    state = {
        inputValue: null
    }

    onEditor(inputValue){
        this.setState({ inputValue })
    }

    render(){
        return <div>
           <FormFiled onEditor = { this.onEditor.bind(this) }  />
        </div>
    }
}

// 子組件FormFiled
class FormFiled extends React.Component {

    render(){
        const { onEditor } = this.props;
        return <div>
           <input 
             type="text" 
             onChange = {e=>{
                 // 調用父組件的callback，並傳遞數據給父組件
                 onEditor(e.target.value);
             }}
           />
        </div>
    }
}
```

### 三，向其他組件通信

非從屬關係組件通信不能直接傳遞數據，因此通常需要其他手段來實現通信。

##### 1，Context 數據共享
Context是react提供的一個API，用於幫助不同組件之間實現數據共享。  

Context 旨在共享全局數據，例如當前經過身份驗證的用戶，主題或首選語言等。 

> 注意： 請謹慎使用它，因為它使組件重用更加困難。


##### 2，第三方狀態管理器 (redux、dva、mobx)
react允許使用第三方狀態管理器來管理react組件的狀態。他們是如何工作的呢 ？

以dva為例：    

![dva數據流](../../images/dva.png)

> 上圖中，`view`層是指react組件(視圖層)，`state`層是指外部組件，通常存放在store狀態庫中，`Action`則是更新state的一些行為。  

> `connect`是一個方法，用於組件(view)連接store(狀態庫)，從而實現view和state同步更新。

> `dispatch`是用於更新state的一個方法。