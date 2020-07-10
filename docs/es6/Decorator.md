# 類修飾器Decorator
修飾器是ES7新增的一個特性，主要用於修改class類的行為。[proposal-decorators](https://github.com/tc39/proposal-decorators)

> 修飾器只能用於類和類的方法，不能用於函數。

#### 基本使用  
```js 
// 修飾器函數，它接受class類為參數(target)，並修改類的行為。 
function annotation(target) {  
   target.annotated = true;  // 給MyClass類添加annotated屬性
   target.state = {   // 給MyClass類添加state對象
       name:"ben"
   };  
}   

// 使用修飾器時，需要放在類的頂部，或者類方法的頂部，後面不能接符號
@annotation    
class MyClass {   

    // 修飾器也可以用於類的方法
    @annotation 
    getname(name){
        return name;
    }
}
   

console.log(MyClass.annotated); // true
console.log(MyClass.state); // { name:"ben" }
```
> 修飾器函數將類作為參數，並修改類的行為。   

> 修飾器的使用需要[@babel/plugin-proposal-decorators](https://babeljs.io/docs/en/babel-plugin-proposal-decorators)插件的支持。

#### 經典案例——mobx(狀態管理器)  
mobx是react生態中主流的狀態管理器之一，它應用了修飾器作為store(狀態庫)和組件之間的黏合劑，使store和組件之間可以很好地交互。
```js
import React, { Component } from 'react';
import { inject, observer } from 'mobx-react';  

// inject表示調用快取,observer表示當快取數據生效時，刷新當前頁面
@inject("store")
@observer
class SchoolComponent extends Component{  

    state={
        schoolname:this.props.store.school.name // store是透過修飾器注入進來的
    }  

    render(){
        return(
            <div>學校：{ this.state.schoolname }</div>
        )
    }
}
export default SchoolComponent;
```

#### 一些建議  

隨著react hook的推出，開發者將更偏向於函數組件，而類組件將會被更少地使用，而修飾器主要應用於類，因此往後修飾器的使用也會減少。

因此不建議大量地使用修飾器，或者可以不使用它。