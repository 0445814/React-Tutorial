# es-module 模組化   

以前JavaScript是沒有模組體系的，後來js社區提出了三種模組化方案，主要是`CommonJS`，`AMD`，`CMD`三大規範。比如nodejs的模組系統`require`、webpack等都是以`CommonJS`規範來實現的；requirejs是基於`AMD`規範來實現的，seajs是基於`CMD`規範實現的。

但這些都不是最好的方式，於是ES6提出了官方的`es-module`模組化方案，成為瀏覽器和伺服器通用的模組解決方案。  

es-module主要由兩個命令構成：export和import，即導出和導入。   

使用es-module時，可以說一個js文件就是一個模組，文件內的變數、函數、類需要export，然後才能在另一個模組中使用import來引用。
## 一，基本使用

##### 普通導入導出
```js
// test1.js 
// 導出 - export一個count變數
export const count = 100;

// test2.js 
// 導入 - import text1.js 的count
import { count } from './test1';
```


##### 默認導入導出
```js
// test1.js 
// 默認導出一個count變數
const count = 100;
export default count;  // 使用默認導出時，不能使用變數聲明表達式
  
  
// 導入時是預設的變數名`default`，你可以定義一個新的名字，或使用`default as`重命名  

// test2.js 
import count from './test1';
或
import anyname from './test1'; // anyname可以是任意變數名  

// 等同於  
import { default as count }  from './test1';
或
import { default as anyname }  from './test1';
```
> 使用默認導出，在其導入時其變數名可自訂


##### 多種導入導出
```js
// test1.js 
export const Component = {};
export default = {};


// test2.js 
import React,{ Component } from './test1';  // React是默認導出的{}，默認導出的變數是可以自訂的

```


##### 複合寫法
```js
export { foo, bar } from 'my_module';

// 等同於
import { foo, bar } from 'my_module';
export { foo, bar };

```

#### 使用`* as` 整體導入
首先，在`validate.js`定義兩個驗證函數
```js
// validate.js

// 驗證手機號碼
export function checkphone(phone) {
  ...
  return phone;
}
// 驗證email
export function checkemail(email) {
  ...
  return email;
}

```

正常導入
```js
// test.js
import { checkphone,checkemail } from './validate';
console.log(checkphone);
console.log(checkemail);
```

使用`* as` 整體導入
```js
// test.js
import * as validates from './validate';
console.log(validates.checkphone);
console.log(validates.checkemail);
```
> `* as`實際上是將導入模組的所有值存放在一個object中，然後可以通過這個object去訪問它們



##### 導入時重命名
```js
// test1.js
export let count = 100;  

// test2.js  導入時將count重命名為num
import { count as num } from './test1';

```

##### 導入普通樣式
```js
import './style.css';

import styles from './style.css';  // css-module
```

## 二，注意事項

1，普通導出(`export`)時，可以導出object、聲明表達式，但不能導出已聲明的變數，或者無變數聲明的表達式
> 無變數聲明，比如匿名函數 function(){...}、class{...} 等等  

!> 總之：export命令規定的是對外的介面，必須與模組內部的變數建立一一對應關係。因為使用import命令的時候，用戶需要知道所要載入的變數名或函數名  

```js
const count = 100;  

export count; // 錯誤❌
export 100; // 錯誤❌
export function(){}; // 錯誤❌
export class {}; // 錯誤❌


export const count = 100; // 正確✔️
export function check(){}; // 正確✔️
export class Component {}; // 正確✔️
export { count }; // 正確✔️
```
  

2，默認導出(`export default`)時，不能導出聲明表達式，class除外。  

這是因為export default命令其實只是輸出一個叫做default的變數，所以它後面不能跟變數聲明語句。  
```js
export default const count = 100; // 錯誤❌


const count = 100;
export default count; // 正確✔️
export default { count }; // 正確✔️
export default [ count ] // 正確✔️
export default function check(){}; // 正確✔️
export default class Component {}; // 正確✔️
```

3，import導入的變數是只讀的
```js
import { a } from './xxx.js'

a = {}; // 錯誤 Syntax Error : 'a' is read-only;

a.foo = 'hello'; // 合法操作
```