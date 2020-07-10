# flex彈性布局  

flex彈性布局是目前主流的頁面布局方案，因此在react開發中也是必備的。

目前主流瀏覽器都已經支持flex，並且[cra(create-react-app)](https://facebook.github.io/create-react-app/docs/getting-started)內建了`Autoprefixer`插件，它會自動添加相容性前綴，因此你必擔心flex的相容性問題。

#### flex基本使用
在react中使用flex彈性布局很簡單，直接在樣式中寫flex語法即可。

比如，下面用flex來實現一個常見的`縱向三欄布局`： 

先看參考效果:   

![布局效果](../../images/shengbei.png)
  
下面是實現的代碼：

組件頁面布局
```js
import React from 'react';
import './App.css'; 

const App = () =>{
    return <div className="App">
        <header className="header" >這裡是頭部</header>
        <section className="content" >
            這裡是內容區
        </section>
        <footer className="footer" >這裡是固定尾部</footer>
    </div>
}
```
App.css
```css
.App{
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}  

.App .content{
   flex: 1;
}
```



