# css-module
`css-module`是處理樣式的一種css模組化方案，它支持哈希class，組合class、class繼承等特性，非常有利於我們編寫樣式。  
### 如何在cra中使用css-module ？  
[cra(create-react-app)](https://facebook.github.io/create-react-app/docs/getting-started)默認支持`css-module`，開箱即用。   

> 1，樣式文件以 `[name].module.css`或`[name].module.scss`的形式命名 

> 2，以變數的形式導入樣式文件，比如 `import styles from './style.module.css'; `  
  
> 3，className以變數引用的方式添加，比如 `className={ styles.title }`  

### 一，哈希class (默認) 
你可以隨意命名class，最終css-module會在局部作用域內給class添加哈希值，確保class唯一而不重複。  
```js
import styles from './style.module.css';  

const App = (props) =>{
    return <div className="wrap" >
       <h2 className={ styles.title } > hello word </h2>
    </div>
}
```
style.module.css:
```css
.title{
    font-size: 17px;
    color: #f66;
}
```
編譯之後：
```html
<h2 class="style_title__s0dsl" > hello word </h2>
```

### 二，非哈希class ( global(.className) ) 
css-modules 允許使用`:global(.className)`的語法，聲明一個全局規則。凡是這樣聲明的class，都不會被編譯成哈希字串。  

style.module.css：
```css  
/* 默認哈希用法 */  
.title{
   color:#f66;
}  
/* global用法 */
:global(.wrap){
  color: green;
  background: red;
}
    

/* 編譯後 */
.style_title__s0dsl{
  color:#f66;
}
.wrap{
   color: green;
   background: red;
}
```
> 注意：使用global的方式添加樣式時，className需要以字串的形式來命名，而不是變數引用  

```js  
import styles from './style.module.css';  

const App = () =>(
   <div className="wrap">
      hello，word
      <h2 className={ styles.title } ></h2>
   </div>
)
```

### 三，class組合 `composition`   

在`css-module`中，一個選擇器可以繼承另一個選擇器的規則，這稱為"組合"（"[composition](https://github.com/css-modules/css-modules#composition)"）。

```css
.className {
  color: green;
  background: red;
}

.otherClassName {
  composes: className;
  color: yellow;
}
```

### 四，class模組繼承  
選擇器也可以繼承其他CSS文件裡面的規則。
```css
/* another.css */  

.className {
  background-color: blue;
}
```  
通過`composes` 和 `from`組合，繼承其他css模組中的css規則。
```css 
/* style.css */
.title {
  composes: className from './another.css';
  color: red;
}

```

### 五，使用變數  
`css-module`支持使用變數，不過需要安裝 PostCSS 和 [postcss-modules-values](https://github.com/css-modules/postcss-modules-values)。
```css
/* 定義變數 */
@value white: #fff;
@value blue: #0c77f8;

/* 使用變數 */
.title {
  color: white;
  background-color: blue;
}
```  

### 六，css-module和sass結合使用  

css-module和sass都非常好用，但他們都有不足的地方，比如css-module不支持css嵌套寫法，sass不支持哈希class等等。  

因此，如果將`css-module`和`sass`結合來使用，將會互相彌補，非常強大。幸運的是，[cra(create-react-app)](https://facebook.github.io/create-react-app/docs/getting-started)支持這樣做。    

下面是一個例子：
```js
import styles from './style.module.scss';  

const App = (props) =>{
    return <div className={ styles.wrap } >
       <h2> hello word </h2>
    </div>
}
```
style.module.scss:
```css
.wrap{
    font-size: 17px;
    color: #f66;
    h2{
       font-size: 28px;
    }
}
```
