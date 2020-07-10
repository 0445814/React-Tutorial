# css-in-js  
### 什麼是css-in-js ？
`css-in-js`是一種使用js編寫css樣式的css處理方案。它的實現方案有很多，比如[styled-components](https://github.com/styled-components/styled-components)、[polished](https://polished.js.org/)、[glamorous](https://github.com/paypal/glamorous)(paypal開源的，不再維護)、[radium](https://github.com/FormidableLabs/radium)、[emotion](https://github.com/emotion-js/emotion)等等。

其中最成熟的便是[styled-components](https://github.com/styled-components/styled-components)和[emotion](https://github.com/emotion-js/emotion)。它們真正意義上實現了`組件化style`，可以說是專門為react打造的。

這裡以`styled-components`為例，其他的`css-in-js`方案可自行查看文件。

### styled-components簡介 
[styled-components](https://github.com/styled-components/styled-components)是css-in-js主流的實現方案，同時也是`組件化style`的主流實現方案。

下面是`styled-components`的一些特性：  
> 1，`唯一class類名`：和css-module異曲同工，生成唯一類名，避免重複和全局汙染，也不需要你費腦筋思考該如何命名。  

> 2，`無冗餘css代碼`：它的樣式和組件綁定，組件調用則樣式起作用。意味著你不需要關心如何檢測和刪除那些未使用的css代碼。

> 3，`動態樣式`： 它可以很簡單地調整和拓展組件的樣式，而不需要建立很多個class類來維護組件的樣式。  

> 4，`自動添加相容前綴`：和Autoprefixer類似，會自動添加瀏覽器相容前綴以支持舊版瀏覽器。  

> 5，`支持變數和繼承`：你可以使用變數來設置不同的樣式，使用這些不同樣式時只需要給樣式組件傳遞一個參數即可。


### 安裝styled-components

使用[styled-components](https://github.com/styled-components/styled-components)非常簡單，和其他多數js包一樣，把它安裝下來即可開箱即用。
```js
yarn add styled-components
```

### ES6標籤模板語法
比如下面有一個函數`tag()`
```js
// 標籤模板寫法
tag`123`;

// 等同於
tag(123);
```

### styled-components的基本使用

`styled-components`提供了一系列的html標籤函數，比如button、h1、h2、ul、div、p等等，標籤函數調用時會生成相應的標籤組件，比如Button、Div等等，可賦給變數隨意命名。

##### 1，普通用法

`styled-components`主要基於ES6的`標籤模板語法`調用標籤函數。比如下面：
```js
import styled from 'styled-components';  

// 標籤模板 - 函數名後接模板字串``
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;

// 使用
<App>
    <Title> 我是標題組件，自帶樣式 </Title> 
</App>
```

##### 2，css嵌套寫法

`styled-components`支持css嵌套寫法，包括標籤和class等。
```js
import styled from 'styled-components';  

// 標籤模板 - 函數名後接模板字串``
const Content = styled.div`
  padding: 12px;
  width:100%;
  height:200px;
  border: 2px solid green;
  > h2 {
     color: palevioletred;
  }
  > .content {
    text-align: center;
    color: #999;
  }
`;

// 使用
<App>
    <Content>
       <h2> 我是標題 </h2>
       <div className="content" > 我是內容 </div>
    </Content>
</App>
```

##### 3，傳遞props屬性
```js
import styled, { css } from 'styled-components';  

const Button = styled.button`
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border-radius: 5px;
  color: palevioletred;
  border: 2px solid palevioletred; 

  /* 傳參 */
  ${props => props.primary && css`
    border: 2px solid mediumseagreen;
    color: mediumseagreen;
  `}
`

const App = (props) =>{
    return <div className="wrap" >
       <Button> 提交  </Button>
       <Button primary > 提交  </Button>
    </div>
}
```

##### 4，拓展樣式組件
```js
import styled from 'styled-components';    

const Button = styled.button`
  background: palevioletred;
  color: white;
`

const ExtendingButton = styled(Button)`
  font-size:18px;
  padding: 5px 25px;
`;

const App = (props) =>{
    return <div className="wrap" >
       <Button> 提交 </Button>
       <ExtendingButton> 提交  </ExtendingButton>
    </div>
}
```

##### 5，拓展組件樣式
```js
import styled from 'styled-components';    

const Link = ({ className, children }) => (
  <a className={className}>
    {children}
  </a>
);

const StyledLink = styled(Link)`
  color: palevioletred;
  font-weight: bold;
`;

const App = (props) =>{
    return <div className="wrap" >
       <Link>跳轉</Link>
       <StyledLink>跳轉</StyledLink>
    </div>
}
```

.... 

更多用法請查看[styled-components文件](https://www.styled-components.com/docs)