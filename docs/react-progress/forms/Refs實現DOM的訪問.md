## Refs是什麼 ？

`Refs(轉發)`是react提供的一種訪問DOM節點的方法。

> 官方提醒：不要過度使用`Refs`，並且儘量少地操作DOM

## 如何創建和使用Refs ?

創建refs有兩種方式，分別是:

> 1，`React.createRef()`   

> 2，`回調式refs`  

#### 1，React.createRef()
使用`React.createRef()`方法就可以創建refs。
```js
class MyComponent extends React.Component {    

  // 1，創建ref
  myRef = React.createRef();  

  componentDidMount(){  

    // 3，通過ref訪問DOM節點
    console.log(this.myRef); // 訪問ref對象 { current: node }
    console.log(this.myRef.current); // 訪問實際DOM節點
    console.log(this.myRef.current.innerHTML); // 訪問DOM的html內容
  }

  render() { 
    // 2，掛載ref
    return <div ref={ this.myRef } > 內容 </div> ;  
  }
}
```

#### 2，回調refs  

除了使用`React.createRef()`方法來創建refs以外，你還可以透過回調函數來使用ref。
```js
class MyComponent extends React.Component {     

  // 1，創建類屬性
  myRef = null;  

  componentDidMount(){  

    // 3，通過ref訪問DOM節點
    console.log(this.myRef); // 直接獲取到DOM節點
    console.log(this.myRef.innerHTML); // 訪問DOM的html內容
  }
  
  render() { 
    // 2，透過ref回調函數來獲取DOM節點
    return <div ref={ node=> this.myRef = node } > 內容 </div> ;  
  }
}
```
<!-- 
### 如何使用Refs ?     

#### 一，React.createRef()
使用`React.createRef()`方法就可以創建refs。
```js
class MyComponent extends React.Component {    
  // 1，創建ref
  myRef = React.createRef();  

  render() { 
    // 2，掛載ref
    return <div ref={ this.myRef } > 內容 </div> ;  
  }
}
```


##### 1，在class組件內部使用    
```js
class MyComponent extends React.Component {    
  // 1，創建ref
  myRef = React.createRef();  

  componentDidMount(){
    // 3，通過ref訪問DOM節點
    console.log(this.myRef); // 訪問ref對象 { current: node }
    console.log(this.myRef.current); // 訪問實際DOM節點
    console.log(this.myRef.current.innerHTML); // 訪問DOM的html內容
    console.log(this.myRef.current.innerText); // 訪問DOM的文本內容
  }

  render() { 
    // 2，掛載ref
    return <div ref={ this.myRef } > 內容 </div> ;  
  }
}
```

##### 2，在class組件上使用      
refs不僅能在DOM上面用，也能在組件上使用(僅限class組件)，通常用於父子組件的DOM交互(儘量少地使用)。
   
下面是一個例子：  
```js
// 父組件
class Parent extends React.Component {  

  childElement = null;  // 1，父組件內定義類屬性

  render() {
    // 2，給子組件傳遞 ref回調函數 ，可獲取到子組件的DOM，並賦給 childElement 類屬性
    return (
      <Child inputRef={el => this.inputElement = el} />
    );
  }
}     

// 3，子組件內獲取父組件ref回調函數，並掛載給DOM節點
function Child(props) {
  return (
    <div>
      <input ref={props.inputRef} />
    </div>
  );
}
```  

##### 3，在函數組件內部使用    
```js
const App = () =>{

    let textInput = React.createRef(); // 1，創建ref

    const getInputValue=()=>{
        console.log(textInput.current);  // 3，訪問DOM
        console.log(textInput.current.value);
    }
    
    // 2，掛載ref
    return (
        <div>
            <input
              type="text"
              ref={textInput}
            />
            <button onClick={ this.getInputValue } > 獲取input值 </button>
        </div>
    )
}
```

##### 2，在函數組件中使用    

#### 二，回調refs
除了使用`React.createRef()`方法來創建refs以外，還可以使用回調函數來創建ref。
```js
class MyComponent extends React.Component {      
  // 創建類屬性
  myRef = null;  

  componentDidMount(){
    // 
  }
  
  render() { 
    return <div ref={ refs=> this.myRef = refs } > 內容 </div> ;  
  }
}
```

### 如何使用Refs ?

Refs的使用分為幾種不同的情況:  

- `class組件的DOM添加Refs`   

- `給class組件添加Refs`   

- `給函數組件的DOM添加Refs`

> 注意：不能給函數組件添加refs，因為它沒有實例

### 一，回調式Refs     
通過回調函數獲取DOM的ref，並賦給類屬性，從而實現對DOM的訪問。
```js
class MyComponent extends React.Component {   

  divRef = null;  // 1，先聲明一個類屬性

  componentDidMount(){ 

      // 3，訪問DOM  

      console.log(this.divRef); // DOM節點
      console.log(this.divRef.innerHTML); // DOM節點的內容
  }

  render() { 

    // 2，通過回調函數獲取ref，並賦給 divRef   

    return <div ref={ element=> this.divRef = element } > 內容 </div> ;  
  }
}
```

### 二，class組件的DOM添加Refs  
在class組件內使用Refs非常簡單，只需要通過`React.createRef()`方法創建一個`ref`，然後掛載到DOM節點就可以通過ref訪問DOM了。   

```js
class MyComponent extends React.Component { 

  myRef = React.createRef();  // 1，創建ref

  componentDidMount(){  

      // 3，訪問ref對象
      console.log(this.myRef); 
      console.log(this.myRef.current); // 訪問實際DOM節點
      console.log(this.myRef.current.innerHTML); // 訪問DOM的html內容
      console.log(this.myRef.current.innerText); // 訪問DOM的文本內容
  }

  render() {
    return <div ref={ this.myRef } > 內容 </div> ;  // 2，掛載ref
  }
}
```

### 三，給class組件添加Refs  
refs不僅能在DOM上面用，也能在組件上使用(僅限class組件)，通常用於父子組件的DOM交互(儘量少地使用)。
   
下面是一個例子：  
```js
// 父組件
class Parent extends React.Component {  

  childElement = null;  // 1，父組件內定義類屬性

  render() {
    // 2，給子組件傳遞 ref回調函數 ，可獲取到子組件的DOM，並賦給 childElement 類屬性
    return (
      <Child inputRef={el => this.inputElement = el} />
    );
  }
}     

// 3，子組件內獲取父組件ref回調函數，並掛載給DOM節點
function Child(props) {
  return (
    <div>
      <input ref={props.inputRef} />
    </div>
  );
}
```


### 四，給函數組件的DOM添加Refs
```js
const App = () =>{

    let textInput = React.createRef(); // 1，創建ref

    const getInputValue=()=>{
        console.log(textInput.current);  // 3，訪問DOM
        console.log(textInput.current.value);
    }
    
    // 2，掛載ref
    return (
        <div>
            <input
              type="text"
              ref={textInput}
            />
            <button onClick={ this.getInputValue } > 獲取input值 </button>
        </div>
    )
}
```

> 注意：不能給函數組件添加refs，因為它沒有實例    

```js  

const MyFunctionalComponent =()=>{
  return <input />;
}

class Parent extends React.Component {  

  textInput = React.createRef();  

  render() {
    // 錯誤的做法 ❌
    return (
      <MyFunctionalComponent ref={this.textInput} />
    );
  }
}
``` -->