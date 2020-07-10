# Spread operator 拓展運算符
 拓展運算符`...`是在對象或數組中展開屬性的一種語法。遵循從右往左，相同則覆蓋的原則。
### 在對象中使用

```js
 const base = { name:"ben", age:23 };  
  
 // 通過拓展運算符'...'將base屬性在user中展開，從而合併對象。
 const user = {  age:20, gender: "男", ...base };  

 console.log(user); // { age:23, gender: "男", name:"ben"};  
```  

##### 在react中的應用  
```js

class UserComponent extends Component {
    render(){
        const user = { name:"ben", age:23, gender: "男" };  
        return <div>
           <Header />  

           <UserPage {...user} />  

           {/* 等同於 */}
           <UserPage name="ben" age="23" gender="男" />  

           <Footer />
        </div>
    }
}  

```  

### 在數組中使用

##### 普通應用 
```js
 const base = [ 1, 2, 3 ];  

 const arr = [ 0, ...base ];  // 數組合併，和concat有相同的功效

 console.log(arr); // [ 0, 1, 2, 3 ]
```
##### `set`和`...`實現數組去重    
ES6 提供了新的數據結構 Set。它類似於數組，但是成員的值都是唯一的，沒有重複的值。
```js
const arr = [ 1,1,2,2,3,4,5,5,5 ]; 
const noRepeatArr = [ ...new Set(arr) ];
```

### 在字串中使用

```js
 const str = "hello";  

 const arr = [ 0, ...str ];

 console.log(arr); // [ 0, "h","e","l","l","o" ]

```