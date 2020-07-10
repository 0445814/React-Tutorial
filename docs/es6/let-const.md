# let 和 const 的用法
## 一，基本使用
```js
// 定義count 

// ES5寫法  
var count = 100;

// ES6寫法
let count = 100;

// 使用const定義常量count 
const count = 100;
```
> 注意：常量是不可變的，也就是常量定義之後不能更改它，否則會報錯  

! > 建議：儘量使用const，除非值可變(值可變時使用let)

## 二，注意事項

##### 塊級作用域
```js
// ES5 - var作用於全局作用域和函數作用域
function f1() {
  var n = 5;
  if (true) {
    var n = 10;
  }
  console.log(n); // 10
}

// ES6 - let只作用於它所在的塊級作用域
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}
```

##### 不允許重複聲明
let不允許在同級作用域內，重複聲明同一個變數。
```js
// ES5 
function f1() {
  let count = 100;
  let count = 10; // 會報錯
}
```


##### 不存在變數提升

```js
// var 的情況
console.log(count); // 輸出undefined
var count = 2;

// let 的情況
console.log(count); // 報錯ReferenceError
let count = 2;

```
