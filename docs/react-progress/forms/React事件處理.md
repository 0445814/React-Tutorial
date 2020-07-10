# 事件處理

react有自己的事件系統，和原生的事件處理程序有些許不同。

### 一，react中使用事件

react事件和原生事件的幾點區別：
> 1，事件名不同，react事件名必須使用駝峰命名   
  
> 2，原生事件處理程序為字串調用，而react則是一個函數

原生的方式：  
```js
// 原生事件處理，事件名小寫，事件處理程序使用字串
<button onclick="submit()">
  提交
</button>
```
react的方式：
```js
// react事件處理，事件名必須使用駝峰命名，事件處理程序使用變數或函數
<button onClick={ submit }>
  提交
</button>
```

### 二，事件綁定(bind)

react規定，在class組件內使用事件時需要使用`bind`來綁定`this`，否則的話`this`會是`undefined`。

```js
class App extends React.Component {
    
    onSubmit(){
        // 通過bind綁定this之後，才可以訪問this，否則會是undefined
        console.log(this); 
    }

    render(){
        // 使用bind綁定this
        return (
            <button onClick = { this.onSubmit.bind(this) } ></button>
        )
    }
}
```

上面的效果等同於下面：  

```js
class App extends React.Component {
    
    onSubmit(){
        // 可以訪問this
        console.log(this); 
    }

    render(){
        // 不使用bind綁定this
        return (
            <button onClick = {e=>this.onSubmit(e)} > 提交 </button>
        )
    }
}
```


### 三，事件傳參

react事件傳參需要先使用`bind`綁定`this`，然後再傳遞參數。

##### 1，函數組件事件傳參：
```js  

const App = () =>{
    const onSubmit = (arg1,arg1,e) =>{
        console.log(arg1);  // 1
        console.log(arg2);  // 2
        console.log(e);     // event對象
    } 
    return (
      <div>
         <button onClick={ onSubmit.bind(this,1,2) } > 提交 </button>
      </div>
    )
}
```

##### 2，class組件事件傳參：  
```js  
class App extends React.Component {
    
    onSubmit(arg1,arg2,e){
        console.log(arg1);  // 1
        console.log(arg2);  // 2
        console.log(e);     // event對象
    }

    render(){
        return (
            <button onClick = { this.onSubmit.bind(this,1,2) } > 提交 </button>
        )
    }
}
```


### 四，阻止事件默認行為  

react不支持通過`return false`阻止事件默認行為，要阻止事件默認行為必須使用`調用 preventDefault`。

原生阻止事件默認行為：
```js
<a href="https://www.baidu.com" onclick="console.log('阻止跳轉.'); return false">
  跳轉
</a>
```

react阻止事件默認行為： 
```js
const App = () =>{
    const onSubmit = (e) =>{
      console.log(e);
      e.preventDefault();
    }
    return (
      <div>
         <a href="https://www.baidu.com" onClick={ onSubmit } >跳轉</a>
      </div>
    )
}
```