# 為什麼需要css處理方案？  
css樣式是前端開發中非常重要的一環，做開發時我們需要有一套完善的css處理方案來處理很多樣式問題。
主要是因為我們在使用原生css做開發時，經常會遇到一些難題，比如說：  
> 1，css代碼重用的問題  

> 2，class命名重複的問題   

> 3，不支持嵌套寫法，很不方便  

> 4，沒有壓縮合併，css文件比較大  

> 5，不能使用變數，不夠靈活  

> 6，一些未來的css語法不相容  

....  

原生css的問題很多，上面只是一些舉例。css社區為了解決這些難題，同時也為了提高我們寫樣式的效率和質量，推出了很多種css處理方案，比如前期的前處理器`sass/less`、再到模組化`css-module`、`postcss`，再到`css-in-js`。    

#### css處理方案有哪些？
css處理方案有很多種，可根據自己的需要來配置合適的css處理方案。  

下面我們來看看，具體有哪些css處理方案

##### 1，原生樣式
內聯樣式:
```js
const App = (props) =>{
    
    return <div className="wrap" >
       <div style={{ color:"red", fontSize:14 }} > hello word </div>
    </div>
}
```
外部樣式:
```js
const App = (props) =>{
    return <div className="wrap" >
       hello word
    </div>
}
```
```css
.wrap{
    width:100%;
    height:200px;
}
```

##### 2，前處理器sass/less
`sass/less`是一種前處理器，是處理css非常好的方式，它允許你使用變數、css嵌套、計算等強大功能，為寫css提供了非常多的便利。
```css
$color : #333; 
$height: 200px;   

.wrap{
    width:100%;
    height:$height;
    h2{                   
        font-szie: 18px;
        color:$color;
    }
}
```
編譯之後：
```css
.wrap{
    width:100%;
    height:200px;
}
.wrap h2{
    font-szie: 18px;
    color:#333;
}
```

##### 3，css-module
`css-module`是處理樣式的一種css模組化方案，它能讓你隨意地命名class，不用擔心它會重複或汙染全局。  

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

##### 4，postcss
[postcss](https://github.com/postcss/postcss)是一款使用插件去轉換CSS的工具集。例如[autoprefixer](https://github.com/postcss/autoprefixer)，[cssnext](https://github.com/MoOx/postcss-cssnext)以及[postcss-modules](https://github.com/css-modules/postcss-modules)。而上面列舉出的這些特性，都是由對應的postcss插件去實現的。  

##### 5，css-in-js (推薦)
`css-in-js`是使用js編寫css樣式的一種處理方案。它有很多非常棒的實現，比如組件化style`styled-components`、[emotion](https://github.com/emotion-js/emotion)等等。

以[styled-components](https://github.com/styled-components/styled-components)為例，`styled-components`可以說是集大成者，也是開拓者。它集成了`css-module`和`autoprefixer`的精髓，也實現了超前的`組件化style`，讓你如流水般寫css。
```js
import styled from 'styled-components'

const Button = styled.button`  
  background: transparent;
  color: white;
  ${props => props.primary && css`
    background: white;
    color: palevioletred;
  `}
`
// 上面styled.button`` 相當於 styled.button()  

const App = (props) =>{
    return <div className="wrap" >
       <Button> 提交  </Button>
       <Button primary > 提交  </Button>
    </div>
}
```

