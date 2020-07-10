# async/await 异步终结者
ES2017(ES8) 标准引入了 `async 函数`，使得异步操作变得更加方便。  

`async / await`对应的是generator的`function* / yield`,它是generator的语法糖，但比generator更友好，async内置执行器，灵活简单。

### 一，基本定义      
async函数的定义很简单，只需要在函数声明前加`async`关键词即可。async函数内可使用await关键词来处理异步。
```js 
async function fn() {  
   const result = await promise ; // await后面通常需要接promise，比如fetch、axios请求等
}    

// 调用  
fn();
```    
> 当函数执行的时候，一旦遇到await就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。  

### 二，async函数多种写法  

```js  

// 1，函数声明
async function fn(){
   // Todo
}


// 2，函数表达式
const foo = async function (){
    // Todo
};


// 3，对象的方法
let obj = { 
    name:"ben",
    age: 23,
    async fn() {
        // Todo
    } 
};  
obj.fn();


// 4，Class类的方法
class Post {

  async getPost(id) {
    const post = await fetch("/api/post",{ postId: id }).then(res=>res.json());
    // ...
  }
}
const Posts = new Post();
Posts.getPost('id');  


// 5，箭头函数
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
    // 捕获异常
    console.log(err);  
  }
}    

// 调用  
getPost();
```    
### 三，返回promise  
async函数返回一个 Promise 对象。

> async函数内部return语句返回的值，会成为then方法回调函数的参数。    

如果await后面的异步操作出错，那么async函数返回的 Promise 对象就和被reject。

```js
async function getPost() {  
  try {

    return await fetch('./post.json'); // 返回await结果

    // 其他工作 
  }
  catch(err){
    // 异常捕获
    console.log(err);  
  }
}    

// 调用  
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


### 四，匿名自执行async  
```js
(async () => {
    const response = await fetch('./post.json').then(res=>res.json());
    console.log(response);
})();
```