# generator非同步編程  
### 一，基本簡介
和promise一樣，generator也是一種非同步處理方案。  

但generator做得更徹底，它能實現以同步的方式來處理非同步，過去處理非同步可能需要十幾行程式碼，而它只需要一行程式碼。  
```js
 // 傳統回調式非同步處理  -  回調地獄
 ajax('http://url-3', options, function (err, result) {
      if (err) {
          return alert(err);
      }
      // 做一些事情
      ...
  });
  

 // generator處理非同步
 function* (){
    ...
    const result1 = yield fetch('http://url-1');
    const result2 = yield fetch('http://url-2'); 

    console.log(result1);
    console.log(result2);
    ...
 }
```

### 二，generator基本使用    

##### 1，Generator函數和普通的函數區別
> a，function和函數名之間有一個*號  

> b，函數體內使用了yield表達式    

##### 2，定義generator函數      
 定義generator函數需要使用`fuction*`關鍵字，函數內可使用`yield`等待處理非同步操作。
 > 注意： yield後面通常要接promise   

```js
  function* fn(){
      const result = yield fetch('./post.json'); // 執行完後才會執行下一行程式碼，感官上相當於同步
      console.log(result);
  }
```  
在對象或class中定義可簡寫：  
```js
  // 在對象中定義  
  const obj = {
    username: "ben",
    * fn(){
        const result = yield fetch('./post.json'); 
        console.log(result);
    }
    // 或
    *
  }  

  // 在class中定義  
  class App {  

    * fn(){
        const result = yield fetch('./post.json'); 
        console.log(result);
    }
  }
```

##### 3，generator原生用法  
調用generator對象有兩個方法:    

一是不斷地調用generator對象的next()方法  

二是直接用for ... of循環疊代generator對象
```js
 function* fn(){
    const res = yield fetch('./post.json');  // 同步執行
 }  
  
// 1，使用next調用generator函數
const g = fn();
const result = g.next();  

result.value.then(function(data){
  return data.json();
}).then(function(data){
  g.next(data);
});    
  

// 2，使用`for of`調用generator函數，遍歷出來的是promise實例
for (let p of fn()) {  
  console.log(p);
}

```  

### 三，使用co模組簡化generator操作    
co是一個js模組，它對generator做了很多封裝處理，它能自動執行generator函數，大大簡化了generator的操作流程。
> 使用co時，yield後面必須是promise   

```js
// co方法接收generator作為參數
co(function *(){
  try {
    const result = yield fetch('./post.json');  // 同步執行
    console.log(result);
  } 
  catch (err) {
    console.error(err);
 }
})
.catch(err=>{
    console.log(err);
});

```

