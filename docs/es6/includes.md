# includes 是否包含

> includes是ES7中新增的一個方法，用於在數組或字串中判斷是否包含某個元素，如果包含就返回`true`，否則就返回`false`。

### 在數組中應用
```js
  const arr = [ 1, 2, 3 ];

  console.log(arr.includes(2));  // true
  console.log(arr.includes(9));  // false
```
等同於  
```js
  const arr = [ 1, 2, 3 ];
  // 傳統寫法
  console.log(arr.indexOf(2)!==-1);  // true
  console.log(arr.indexOf(9)!==-1);  // false
```  

### 在字串中的應用  

```js
  const str = "Hello world!";

  console.log(str.includes("e"));  // true
  console.log(str.includes("z"));  // false
```
等同於  
```js
  const str = "Hello world!";
  // 傳統寫法
  console.log(str.indexOf("e")!==-1);  // true
  console.log(str.indexOf("z")!==-1);  // false
```  