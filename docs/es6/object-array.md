# 解構賦值    
ES6 允許按照一定模式，從數組和對象中提取值，對變數進行賦值，這被稱為解構賦值（Destructuring）。
### 一，對象的解構賦值

#### 基本使用  
對象屬性的結構是`key:value`，解構賦值時，變數名需要和屬性名`key`一致，否則會是`undefined`。
```js
let user = { name: "ben", age: 20, gender:"男" };  

// 解構賦值
const { name, age } = user;  // 變數名對應的是對象屬性的key
console.log(name); // ben
console.log(age); // 20
```
等同於
```js  
// 傳統寫法
let user = { name: "ben", age: 20, gender:"男" };
const name = user.name;
const age = user.age;

```
案例: 在react組件中應用
```js
class App extends Components {
    render(){
        const { location } = this.props; // 解構賦值
        return <div>
           <p>當前路由是:<span>{ location.pathname }</span></p>
        </div>
    }
}

```

#### 解構時重命名
對象屬性是`key:value`結構，因此在解構時，解構出來的變數名預設是該鍵名key，但我們可以重新命名它。
```js

let user = { name: "ben", age: 20, gender:"男" };

// 解構賦值
const { name: username , age: userage } = user;

console.log(name); // 報錯  
console.log(age); // 報錯 

console.log(username); // ben   解構時已將變數名改為username
console.log(userage); // 20    解構時已將變數名改為userage
```

#### 解構時設置預設值  

> 設置預設值後，當獲取的值不存在時則使用預設值   

```js
// 沒有name的user
let user = { age: 20, gender:"男" }; 

// 正常解構賦值
const { name } = user;
console.log(name); // undefined

// 設置預設值
const { name="ben" } = user;
console.log(name); // ben   值不存在時使用預設值
```

### 二，數組的解構賦值  

##### 基本使用  

數組的解構賦值和對象不同，對象解構賦值對應的是鍵(key)，而數組對應的是索引(Index)
```js
let [first, ,last] = [1, 2, 3];
console.log(first);  // 1
console.log(last);  // 3
```
##### 設置預設值

數組的解構賦值和對象不同，對象解構賦值對應的是鍵(key)，而數組對應的是索引(Index)
```js
let [ first, , ,last=10 ] = [1, 2, 3];
console.log(first);  // 1
console.log(last);  // 10  // 該數組第四位不存在，因此使用預設值10
```

##### 經典案例：設置多個變數  

當要設置多個變數時，可使用變數解構賦值來簡化程式碼

```js
// 傳統寫法
let name = "ben";
let age = 23;
let gender = "男";

// 解構賦值寫法
let [ name, age, gender ] = [ "ben", 23, "男" ];
```


### 三，字串的解構賦值    

和數組一樣，字串的解構賦值也是基於下標索引(Index)的。  

```js
const [a, b, c, d, e] = 'hello';

console.log(a); // h
console.log(b); // e
console.log(e); // o
```

### 四，函數的解構賦值    

函數的參數也可以使用解構賦值。    

##### 當參數是`數組`時:
```js
// 原來
function add(args){
  return args[0] + args[1];
}  

// 解構賦值
function add([x, y]){
  return x + y;
}

add([1, 2]); // 3
```

##### 當參數是`對象(object)`時:
```js
// 原來
function add(args){
  return args.x + args.y;
}  

// 解構賦值
function add({ x, y }){
  return x + y;
}

add({ x:1, y:2 }); // 3
```



##### 使用預設值
```js
// 解構賦值
function add({ x=0, y=1 }){
  return x + y;
}

add({ x:1, y:2 }); // 3
add({ y:2 }); // 2
add(); // 1
```