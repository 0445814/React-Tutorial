# 使用sass

sass是一種css前處理器，是處理css非常好的方式，它允許你使用變數、css嵌套、計算等強大功能，為寫css提供了非常多的便利。

[cra(create-react-app)](https://facebook.github.io/create-react-app/)是支持sass的，但需要你安裝它。

### 安裝sass  

安裝sass非常簡單，只需要安裝`node-sass`即可在`cra`中使用它。
```js
yarn add node-sass
```
安裝好之後你就可以創建scss文件編寫樣式了。比如:

```js
import './style.scss';

const App = () =>{
    return <div className="wrap" >
        sass我來啦
    </div>
}
```
```css  
/* style.scss */ 

 .wrap{
    width:100%;
    height:200px;
 }
```  

### 一，樣式嵌套
scss允許你嵌套寫樣式。
```css
/* sass嵌套寫法 */
 .wrap{
    width:100%;
     h2{
         color:#333;
         font-size:18px;
     }
 }

/* 編譯後 */  
.wrap{
    width:100%;
}
.wrap h2{
    color:#333;
    font-size:18px;
}
```

### 二，群組嵌套
```css
/* Sass代碼 */
.wrap {
    h1, h2, h3 {
      margin-bottom: 0.8em
    }
}  

/*編譯後*/
.wrap h1, .wrap h2, .wrap h3 { 
    margin-bottom: 0.8em; 
}
```

### 三，css屬性嵌套
```css
/* Sass代碼 */
.wrap {
  width:100%;
  border: {
    style: solid;
    width: 1px;
    color: #ccc;
  }
}  

/* 編譯後 */
.wrap {
  width:100%;
  border-style: solid;
  border-width: 1px;
  border-color: #ccc;
}
```

### 四，使用變數
```css  
 $defaultColor: #333;
 $defaultFontSize: 16px;  

 .wrap{
    width:100%;
     h2{
         color: $defaultColor;
     }
     .content{
         font-size:$defaultFontSize;
         .box{
            padding: 1em 2em;
         }
     }
 }
```

......  

更多用法請參考[sass官方文件](http://sass-lang.com/)