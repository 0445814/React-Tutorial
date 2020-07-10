# state的基本使用

### state是什麼 ？

簡單來講，state就是react組件的狀態。在組件內，state是一個object。

state分為本地狀態和外部狀態，本地狀態也就是組件內部狀態，它必須添加在組件`state對象`上。  

外部狀態也就是從組件外部傳進來的狀態，外部狀態通常是由第三方狀態管理器進行管理。

> 注意：函數組件本身沒有生命週期，也不能使用state，但借助`react hook`可以使用state和生命週期。

### state如何定義 ?  
定義state非常簡單，只需要在class組件內添加`state`對象屬性即可。state對象內的屬性就是組件本地狀態。 

通過`this.state`即可訪問到組件本地狀態。

比如下面的`loading`就是react組件的一個本地狀態。
```js
class App extends React.Component {  

    state = {
        loading: false  // 設置預設值為false
    } 

    render(){
        return <div>
            { this.state.loading? <div> 載入中... </div> : null }
        </div>
    }
}
```    

### 數據也是一種state  

我們從後台請求的數據也是一種state，如果是本地狀態，我們通常把它添加在組件`state對象`上，然後再輸出到jsx。
```js
class App extends React.Component {  

    state = {
        user: null
    } 

    // 這個生命週期方法在組件渲染完成時執行
    async componentDidMount(){
        // 向後台請求用戶數據
        const user = await fetch("/api/user").then(res=>res.json());
        this.setState({  // 更新用戶數據到state對象
            user
        })
    }

    render(){ 

        // 外部狀態loading
        const { loading } = this.props; 

        // 通過this.state訪問狀態user
        const { user } = this.state;
        return <div>
            { user && user.name }
        </div>
    }
}
```
