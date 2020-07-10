### setState是什麼方法 ？  

`setState(stateObject,callback)`方法是class組件自帶的方法，它主要用於更新組件的狀態(state)。  

setState方法是非同步執行的，它接收兩個參數。  

> stateObject：第一個參數，是一個object或函數，裡面是你最新的state,如果是函數則必須返回一個object。  

> callback：state更新後執行的回調函數。

!> 注意：你不能在render方法中直接調用`setState`方法，否則會報錯。

### 如何訪問setState ？

很簡單，在class組件內透過`this`來訪問即可。`this.setState`

### setState基本使用    
setState用於更新組件狀態，使用它非常簡單。 
```js
class App extends React.Component {  

    state = {
        count: 0
    } 

    addCount(){
        const { count } = this.state;
        this.setState({
            count: count+1
        })
    }

    render(){ 
        const { count } = this.state;
        return <div>
           <div> { count } </div> 
           <button onClick={ this.addCount.bind(this) }  > 增加 </button>
        </div>
    }
}
```
### state雙向綁定  
react也可以實現雙向綁定，使用`setState`方法即可。下面是一個例子：
```js
class App extends React.Component {  

    state = {
        value: null
    }  

    render(){ 
        return <div>
            <input 
              type="text" 
              value={ this.state.value }
              onChange={e=>this.setState({ value: e.target.value })} 
            />  
            <p> 輸入的值是: { this.state.value } </p>
        </div>
    }
}
```

### state同步更新     

在react開發中經常會有這種需求，要先後更新多個state，後一個更新必須在前一個state更新完畢後執行。也就是串列執行setState。比如下面這個案例：  
```js
class App extends React.Component {  

    state = {
        user: null,
        posts: null
    }  

    componentDidMount(){
        // 由於是非同步，下面兩個setState是同時執行的
        setState({ user: {} });
        setState({ posts: [] });
    }

    render(){ 
        return <div>
            hello word
        </div>
    }
}
```

但是`setState`方法是非同步的，也就是當有多個`setState`時他們是同時執行的，並不能實現執行完一個setState後，再執行下一個setState。

當我們要實現這種需求的時候，我們只能借助setState方法的第二個參數來實現，也就是callback。下面是一個例子：
```js
class App extends React.Component {  

    state = {
        user: null,
        posts: null
    }  

    componentDidMount(){
        // 透過回調函數來實現串列更新state
        setState({ 
            value: { name:"ben" }
        },()=>{
            setState({ posts: [] });
        });
    }

    render(){ 
        return <div>
            hello word
        </div>
    }
}
```

但是我們還有更簡潔的方式，就是借助`async/await`語法。下面是一個例子：

```js
class App extends React.Component {  

    state = {
        user: null,
        posts: null
    }  

    async componentDidMount(){
        await setState({ user: { name:"ben" } });
        await setState({ posts: [] });
    }

    render(){ 
        return <div>
            hello word
        </div>
    }
}
```

### 封裝同步setState
我們還可以使用`promise`和`async/await`封裝一個同步setState方法，方便我們使用。下面是一個例子： 

```js
class App extends React.Component {  

    state = {
        user: null,
        posts: null
    }  

    setStateAsync(stateObject){
        return new Promise((resolve) => {
            this.setState(stateObject, resolve);
        });
    }

    async componentDidMount(){
        await this.setStateAsync({ value: 1 });
        await this.setStateAsync({ posts: [] });
    }

    render(){ 
        return <div>
            hello word
        </div>
    }
}
```