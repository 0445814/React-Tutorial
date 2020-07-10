# jsx的基本使用   
jsx是js的拓展語法，因此它能和js很好地結合使用。
### 如何編寫html標籤 ？ 
在jsx中直接編寫即可。
```js
// 使用html標籤
const App = () =>{
    return <div>
        這裡是jsx
    </div>
}
```
### 如何編寫樣式 ？ 
##### 1，內聯樣式
內聯樣式需要使用`style`屬性，它的值必須是一個object，樣式可寫在這個object中。可使用js計算。
```js
const App = () =>{
    return <div style={{ color:"red",fontSize:15, width: document.body.clientWidth }} >
        這裡是jsx
    </div>
}
```
##### 2，外部樣式
外部樣式需要載入css文件，然後使用`className`定義類名。
```js
import './style.css';  

const App = () =>{
    return <div className="wrap" >
        這裡是jsx
    </div>
}
```
style.css
```css
.wrap{
    width:100%;
    height:100%;
    font-size:16px;
}
 
```
### 如何使用JavaScript表達式 ？ 
jsx中可使用花括號`{}`來輸入js表達式。

##### 1，普通使用
```js
// UserPage組件
const UserPage = (props) =>{
    const { name } = props;
    return <div className="wrap" >
        <p> 我的名字是: { name } </p>
    </div>
}

```
##### 2，jsx用作表達式  
jsx也可以作為一種表達式使用，把它賦給變數。  

```js
// UserPage組件
const UserPage = (props) =>{

    const title = <h1> 這裡是個人首頁 </h1>;  

    return <div className="wrap" >
        { title }
        <p> 我的名字是: { name } </p>
    </div>
}
```

##### 3，傳遞屬性  
傳遞屬性時，如果是變數、數字或布爾值，也需要使用花括號`{}`來傳遞。
```js
// UserPage組件
const UserPage = (props) =>{

    const title = <h1> 這裡是個人首頁 </h1>;  

    return <div className="wrap" >

        { title }
        <p> 我的名字是: { name } </p>

        <UserProfile
            name = { name }
            age = { 23 }
            gender = "男"
            loading = { false }
        />
    </div>
}
```

##### 4，輸出html  
輸出html需要使用`dangerouslySetInnerHTML`屬性。這個屬性相當於`innerHTML`。
```js
const App = (props) =>{

    const content = "<p> 我是html字串 </p>";  

    return <div className="wrap" >
       <div dangerouslySetInnerHTML={{ __html: content }} ></div>
    </div>
}
```

##### 5，輸出事件 
```js
const App = (props) =>{

    const onSubmit = () =>{
        console.log("提交數據~");
    }

    return <div className="wrap" >
       <button onClick={ onSubmit } >提交</button>
    </div>
}
```

### 如何載入圖片 ？
###### 使用require載入
```js
const App = (props) =>{
    return <div className="wrap" >
       <img src={ require("./test.png") } />
    </div>
}
```
###### 使用import載入
```js
import Img from './test.png';  

const App = (props) =>{
    return <div className="wrap" >
       <img src={ Img } />
    </div>
}
```

### 如何使用注釋 ？
在jsx中使用注釋，要使用`{/* 注釋的內容 */}`
```js
const App = (props) =>{
    return <div className="wrap" >
       {/* <p>hello word</p> */}
    </div>
}
```