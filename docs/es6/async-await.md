# async/await 非同步終結者
ES2017(ES8) 標準引入了 `async 函數`，使得非同步操作變得更加方便。  

`async / await`對應的是generator的`function* / yield`,它是generator的語法糖，但比generator更友好，async內建執行器，靈活簡單。

### 一，基本定義      
async函數的定義很簡單，只需要在函數聲明前加`async`關鍵字即可。async函數內可使用await關鍵字來處理非同步。
```js 
async function fn() {  
   const result = await promise ; // await後面通常需要接promise，比如fetch、axios請求等
}    

// 調用  
fn();
```    
> 當函數執行的時候，一旦遇到await就會先返回，等到非同步操作完成，再接著執行函數體內後面的語句。  

### 二，async函數多種寫法  

```js  

// 1，函數聲明
async function fn(){
   // Todo
}


// 2，函數表達式
const foo = async function (){
    // Todo
};


// 3，對象的方法
let obj = { 
    name:"ben",
    age: 23,
    async fn() {
        // Todo
    } 
};  
obj.fn();


// 4，Class類的方法
class Post {

  async getPost(id) {
    const post = await fetch("/api/post",{ postId: id }).then(res=>res.json());
    // ...
  }
}
const Posts = new Post();
Posts.getPost('id');  


// 5，箭頭函數
const fn = async () => {
    // ...
};
```

##### 基本用法
```js
async function getPost() {  
  try {

    const post = await fetch('./post.json').then(res=>res.json()); 
   // 或
    const postres = await fetch('./post.json')
    const post = await postres.json();

    console.log(post);  

    // 其他工作
    ...
  }
  catch(err){
    // 捕獲異常
    console.log(err);  
  }
}    

// 調用  
getPost();
```    
### 三，返回promise  
async函數返回一個 Promise 對象。

> async函數內部return語句返回的值，會成為then方法回調函數的參數。    

如果await後面的非同步操作出錯，那麼async函數返回的 Promise 對象就和被reject。

```js
async function getPost() {  
  try {

    return await fetch('./post.json'); // 返回await結果

    // 其他工作 
  }
  catch(err){
    // 異常捕獲
    console.log(err);  
  }
}    

// 調用  
getPost()
 .then(res=>{
    return res.json();
 })
 .then(data=>{
    console.log(data);
 })
 .catch(err=>{
    console.log(err);
 })
```    


### 四，匿名自執行async  
```js
(async () => {
    const response = await fetch('./post.json').then(res=>res.json());
    console.log(response);
})();
```