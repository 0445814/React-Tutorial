# 對象拓展

### 一，對象屬性簡寫   

##### 基本使用
```js
let name = "ben";
let age = 23;
let gender = "男";   

// 賦值給user變數，使用簡寫的形式
const user = { name, age, gender  };
  

// 實際上等同於:
const user = { 
    name: name,
    age: age,
    gender: gender
}
```

##### 函數簡寫  
```js    
let name = "ben";
let age = 23;
const user = {
    name,
    age,  
    // 函數簡寫
    auth(name){
        return !name;
    }
}

```  
實際上等同於   

```js    
let name = "ben";
let age = 23;  
// 傳統寫法
const user = {
    name: name,
    age: age,  
    auth: function(name){
        return !name;
    }
}

```  

##### 使用拓展運算符`...`
```js

// 賦值給user變數，使用簡寫的形式
const base = { name:"ben", age:23 };   

// 使用`...`
const user = { ...base, gender:"男" }
console.log(user);  // { name:"ben", age:23, gender:"男" }

```


### 二，Object.keys()  

對象屬性是`key:value`結構，而Object.keys()方法主要用於把對象屬性的鍵`key`轉成一個數組。     

```js
const user = { name:"ben", age:23, gender:"男" };

const userkey = Object.keys(user);

console.log(userkey);  // [ "name", "age", "gender" ]

```  


##### 經典案例:
```js

class App extends Component {
    render(){
        const user = { name:"ben", age:23, gender:"男" };
        const options = { name:"使用者名稱", age:"年齡", gender:"性別" };
        return <div>
           {
               Object.keys(options).map(function(key){
                   return <p key={key} >  
                      { options[key] } : { user[key] }
                   </p>
               })
           }
        </div>
    }
}

// 上面渲染結果:  

使用者名稱: ben
年齡: 23
性別: 男

```

### 三，Object.values() 

和Object.keys()不同，Object.values方法主要用於把對象屬性的值`value`轉成一個數組。     

> Object.values是ES7中新增的方法

```js
const user = { name:"ben", age:23, gender:"男" };

const uservalue = Object.keys(user);

console.log(uservalue);  // [ "ben", 23, "男" ]

```


### 四，Object.assign() 

這是一個對象合併的方法。從右往左合併，當遇到相同屬性時會直接覆蓋。  

```js
const base = { name:"ben", age:23 }; // 基本訊息
const expand = { age: 20, gender:"男", birthday:"1月1日" }; // 額外訊息

// 對象合併
const user = object.assign(base,expand)
console.log(user);  // { name:"ben", age: 20, gender:"男", birthday:"1月1日" }
```
> base和expand都有age屬性，但expand在右邊，合併是從右往左的，所以expand的age覆蓋了base的age

### 五，Object.entries() 

這是一個對象屬性疊代的方法，最終產生一個二維數組。二維數組中的每個屬性對應對象屬性的`key`和`value`。

```js
const user = { name:"ben", age:23};

// 對象屬性疊代
console.log(Object.entries(user));  // [ ["name","ben"],["age",23] ]
```
相當於:
```js
const obj = { 
    key:value 
};

// 對象屬性疊代
console.log(Object.entries(obj));  // [ [key,value] ... ]
```

### 六，Object.is() 

Object.is()用於判斷兩個值是否相等，與運算符`===`等效。

```js
Object.is('foo', 'foo')
// true  

Object.is({}, {})
// false
```
  
> 如果要判斷兩個對象是否相等，建議使用lodash的isEqual方法  

```js  
import _ from 'lodash';  

let object = { 'a': 1 };
let other = { 'a': 1 };
 
_.isEqual(object, other);
// => true
 
object === other;
// => false
```