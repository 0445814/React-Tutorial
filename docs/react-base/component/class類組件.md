# class 類組件

類組件顧名思義是透過class類來創建的組件。    

react提供了一個抽象的基類，也就是`React.Component`，它內建了很多生命週期方法，以及其他的一些特性，以幫助你創建react組件。 

你只需要創建一個class類並且透過`extends`來繼承`React.Component`這個基類即可創建一個類組件。  

##### 1，基本定義
```js 
import React from 'react'; 

// 類組件定義 
class App extends React.Component {  
    // ...做一些事情
    render(){
        return (<div>
            hello，這是一個類組件
        </div>)
    }
}
```
> 類組件內必須要有render方法，並返回jsx

##### 2，使用`PureComponent`    

與`Component`相比，`PureComponent`做了一些簡單最佳化，性能更好。 

```js 
import React from 'react';

// 類組件定義 
class App extends React.PureComponent {  
    // ...做一些事情
    render(){
        return (<div>
            hello，這是一個類組件
        </div>)
    }
}
```
>注意：使用`PureComponent`可能會導致一些問題，比如`react-router`的`Link`失效等問題。搭配`immutable.js`使用可避免這些問題。


### 三，類組件的使用
##### 閉合寫法
```js 
import React from 'react'; 

// 函數組件定義
<App />
```
##### 嵌套寫法  
嵌套使用的組件，可以通過`props`下的childdren屬性獲取到嵌套的子元素。
```js 
import React from 'react'; 

// 嵌套子元素
<App>
   <div> 我是App組件的子元素 </div>
</App>
   
   


```
App組件
```js
// App組件
class App extends React.Component {  
    // ...做一些事情
    render(){

        return (<div>
            { this.props.children }  
        </div>)
    }
}
```

##### 嵌套函數調用
組件調用時可嵌套函數時，可通過`props`下的childdren獲取這個函數，並調用這個函數來渲染子元素。

```js 
import React from 'react'; 

// 調用App組件，透過嵌套函數的方式
<App>
   {(args)=><div> 我是App嵌套的子元素，但我是一個函數 </div>}
</App>

```
App組件
```js
// App組件
class App extends React.PureComponent {  
    // ...做一些事情
    render(){

        return (<div>
            { this.props.children(args) }   // 調用時可傳入一些參數
        </div>)
    }
}
```
> 注意：嵌套的函數必須返回jsx，因此嵌套的函數本質上是一個函數組件  