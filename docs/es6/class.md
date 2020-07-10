# class 類
> ES6中的class(類)是ES5原型寫法的一個語法糖，擁有很好的開發體驗

### 一，基本使用  

```js
// 定義一個空的類
class Point {
}

// 如果class內沒有定義constructor，則默認class的constructor為空函數。
class Point {
  constructor() {}
}
```
生成類實例，傳遞參數
```js
// ES6寫法
class Point {
  // 構造函數
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}  
// 訪問
const a = new Point(1, 2);  
```  
等同於:
```js
// 傳統ES5寫法
function Point(x, y) {
  this.x = x;
  this.y = y;
}
Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};  
// 訪問
var p = new Point(1, 2);

```
> constructor是class的構造函數，當使用new生成實例時，constructor方法會自動調用  

### 二，定義class類屬性    

##### 1，在constructor內定義
```js  
// ES6寫法
class Point {  
    constructor() {
        this.state={
            name: null
        }
        this.getname = this.getname.bind(this);
    }
    getname(){
        // do
    }
}    

```    
##### 2，使用[class properties proposal](https://github.com/tc39/proposal-class-fields)定義類屬性  
class properties proposal 支持省略constructor，在類內直接定義類的屬性，大大簡化了類的操作。    
> [class properties proposal](https://github.com/tc39/proposal-class-fields)是ES7新提案，
需要[@babel/plugin-proposal-class-properties](https://babeljs.io/docs/en/babel-plugin-proposal-class-properties)插件的支持。  
  
```js
class Point {      

    // 直接定義類屬性
    state = {
        name: null
    }    

    // 不再需要在constructor內綁定
    getname(){
        // do
    }
}    
```   
[class properties proposal](https://github.com/tc39/proposal-class-fields)在react中的應用:  
```js
class App extends Component {      

    // 直接定義類屬性state
    state = {  
        name: "ben",
        age: 23,
        gender: "男"
    }  

    render(){
        const { name, age, gender } = this.state;
        return <div>
           <p> 當前登錄用戶: { name }，{ age }歲，{ gender } </p>
        </div>
    }
}
```

### 三，使用`static`定義靜態方法和靜態屬性      
使用static定義類的靜態方法，不需要實例化就能訪問。
```js
class Point {      

    // static定義靜態方法
    static getname(name){
        return name;
    }    

    // static定義靜態屬性
    static gender = "man";  

    checkphone(){
       // do something
    }
}  

// 訪問
const P = Point.getname("ben"); // ben 
const gender = Point.gender; // => man 

```


### 四，在class類內定義函數  
```js
class Point {  
    getname(){
        return 1;
    }
    // 或使用箭頭函數
    getname = () =>{
        return 1;
    }
}  
```

### 五，class類的繼承  
   
#### 基本使用  
class的繼承需要使用`extends`關鍵字 ，這比 ES5 的通過修改原型鏈實現繼承，要清晰和方便很多。
```js
class A {}

class B extends A {
  constructor() {  
    super(); 
    // do
  }
}
```  

#### super的使用 
子類要繼承父類，還需要在子類的構造函數內調用super方法，否則會報錯。   
super實際上是調用父類的構造函數，但它的this指向的是子類。  
> 注意：super只能用在子類的構造函數之中，並且需要執行`super()`之後才能訪問`this`  

```js  
class A {}

class B extends A {
  constructor() {  
    console.log(this); // 報錯
    super(); // 繼承父類A的屬性和方法    
    console.log(this); // 正確
  }
}
```  

#### 使用 [class properties proposal](https://github.com/tc39/proposal-class-fields) 直接繼承  
使用class properties proposal的好處是可以省略constructor的繁瑣綁定，可以直接定義且自動繼承。
```js  
class A {
    state={
        age:23
    }
}

class B extends A {
  state = {
      userage: this.state.age  // age已被繼承，因此可直接訪問。this指向的是B。
  }
}    

// 訪問  
const P = new B();  
console.log(P.state.userage); // 23
``` 