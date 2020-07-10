# 箭頭函數
ES6 允許使用“箭頭”（=>）定義函數，給開發者帶來大大的便利。
### 一，基本使用  

```js  
 // 匿名箭頭函數
 (arg) =>{
     // Todo
 }    
 
 // 有名箭頭函數
 const fn = (arg) =>{
     // Todo
 }
```  
等同於:  
```js  
 // 傳統寫法
 function fn(arg){
     // Todo
 }
```   
> 注意：匿名箭頭函數不能直接定義，它需要依附，比如作為回調函數  arr.forEach((item)=>{ ... })
  
### 二，多種寫法  
  
##### 不同參數  
```js  
 // 單個參數時，可省略括號()
 const fn = arg =>{
     // Todo
 }  

 // 沒有參數或有多個參數時，需要加括號() 
 const fn =()=>{
     // Todo
 }  
 const fn =(arg1,arg2...)=>{
     // Todo
 }    
```     

##### 不同返回值    
1，單條語句返回值時，可省略大括號{} 
```js  
 // 單個參數
 const fn = v =>v;  
 
 // 多個參數
 const fn = (x,y) =>x+y;  
```    
2，多條語句返回值時，需要加大括號{} 
```js  
 const fn = v =>{
    if(v){
        return v++;
    }
 };  
``` 
3，單條語句且返回值為對象時，可省略大括號{}，但返回值需要用()包裹。
```js  
 const fn = user =>({ id: user.id, name: user.name });  
 //等同於  
 function fn(user){
    return {
        id: user.id, 
        name: user.name
    }
 }  
``` 

##### 使用解構賦值  
1, 參數為object時
```js
// 原來
const fn = user =>({ id: user.id, name: user.name });   

// 使用解構賦值  
const fn = ({ id, name, age, gender }) =>({ id, name });

```  
2, 參數為數組時
```js
// 原來
const fn =arr=>arr[0]+arr[0];   

// 使用解構賦值  
const fn = ([x,y]) =>x+y;

```

### 三，箭頭函數嵌套    

1，沒有函數嵌套時
```js    
const fn= a =>a;    

//等同於
function fn(a){
   return a;
}
```
2，一層函數嵌套時
```js    
const fn= a =>b=>a+b;    

//等同於
function fn(a){
   return function(b){
       return a+b;
   }
}
```
3，兩層函數嵌套時
```js    
const fn= a => b => c =>a+b+c;    

//等同於
function fn(a){
   return function(b){
       return function(c){
           return a+b+c;
       };
   }
}
```
4，三層函數嵌套時
```js    
const fn= a => b => c => d =>a+b+c+d;    

//等同於
function fn(a){
   return function(b){
       return function(c){
           return function(d){
               return a+b+c+d;
           }
       };
   }
}
```

> 以此類推...