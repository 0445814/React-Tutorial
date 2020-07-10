### 一，什麼是jsx ？

jsx是一種獨立的js標籤語法，它既不是字串也不是HTML。  

但jsx是在html基礎上使用js開發出來的，因此它具有幾乎所有的html特性。你完全可以把它當html來使用。
```js
// jsx
const element = <h1>Hello, world!</h1>;
```

從本質上講，jsx 只是為 `React.createElement(component, props, ...children)` 函數提供的語法糖。

> React.createElement方法主要用於生成 `React elements`，這是一種`虛擬DOM`。

### 二，jsx和html的區別  

> 1，jsx和html是兩種不同的標籤語法，但jsx擁有和html幾乎相同的寫法和特性(標籤、標籤屬性、事件名等等)    

> 2，jsx是js語法拓展，而html則是原生的標籤語法    

> 3，jsx可以使用js表達式，html不能   

> 4，jsx天然預防xss漏洞，html不能   

> 5，jsx事件和標籤屬性使用駝峰命名，html不需要   

> 6，jsx會被轉換成`React Dom`，然後再轉換為`原生DOM`，而html則直接生成`原生dom`  

> 7，jsx和html的部分屬性有差異，比如html的`class`對應jsx的`className`  

##### 總的來說，jsx可以說是JavaScript版的html。  

### 三，jsx和html的屬性差異

#### 1，命名方式  
在jsx中，所有的html屬性和事件名都需要使用駝峰命名，有兩種例外，那就是`aria-*`和`data-*`。

###### 屬性名  

```js
// `minLength`使用的是駝峰命名，而html中則是`minlength`
 <App>
    <input type="text" minLength="10"  />
 </App>
```

###### 事件名  

```js
//  react中onChange、onClick使用的是駝峰命名，而在html中則是onchange、onclick
<App>
    <input type="text" onChange={ (e)=>console.log(e.target.value) }  />
    <button onClick={ ()=>alert("點擊提交") }>提交</button>
 </App>
```

###### 樣式名 (內聯樣式) 
jsx中使用內聯樣式時，也需要駝峰命名，且樣式需要寫在一個object中，並賦給style屬性。  

jsx內聯樣式:
```js  
// jsx駝峰內聯樣式
<App>
    <input type="text" style={{ backgroundColor:"#f66", fontSize: 15 }}  />
</App> 
```
原生html內聯樣式:
```js  
// 原生內聯樣式
<input type="text" style="background-color:red;font-size:15px;"  />
```

#### 2，屬性差異

##### 1，className 
html中的css類名為`class`，而jsx中css類名則是`className`
```js  
<App>
    <input type="text" className="myclass" />
</App> 
```

##### 2，value 和 defaultValue 
在jsx中除了可以用`value`屬性設置`<input>` 和 `<textarea>`的值以外，還可以使用`defaultValue`屬性設置首次裝載時的值。
```js  
<App>
    <input type="text" value="我是固定值" />
    <input type="text" defaultValue="我是初始預設值" />
</App> 
```

##### 3，checked 和 defaultChecked

`checked`可用於設置`checkbox` 和 `radio`是否選中，defaultChecked可用於設置默認選中的項(首次載入組件時是否選中)。
```js  
<App>
    <input type="radio" checked="checked" />白色
    <input type="radio" defaultChecked={true} />紅色
</App> 
```

##### 4，innerHTML 和 dangerouslySetInnerHTML
`dangerouslySetInnerHTML`相當於html的`innerHTML`。它接受一個對象作為值，並且對象中使用`__html`來指定html字串。

```js  
// html字串
const htmlstr = `<p>hello word</p>`;

// jsx
<App>
    <div dangerouslySetInnerHTML={{ __html: htmlstr }} >
    </div>
</App> 
```