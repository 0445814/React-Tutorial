
### props是什麼 ？

簡單來講，props是一個object，是組件外部傳進來的屬性的集合。

props也可以是任意類型。

### 如何傳遞props ？

傳遞props非常簡單，只需要在組件調用時作為組件屬性添加給組件即可。
```js
// 調用組件時傳遞props
<App loading={ false } />
```

### 如何訪問props ？
函數組件和class組件訪問props的方式不同。函數組件的props通過函數傳參獲取，class組件通過訪問`this.props`來獲取。  

##### class組件:
```js
class App extends React.Component {  
    render(){   

        // 通過this.props即可訪問到外部傳進來的屬性 
        const { loading } = this.props; 
        return <div>
            { loading? <div> 載入中... </div> : null }
        </div>
    }
} 

// 調用組件
<App loading={ false } />
```

##### 函數組件:
```js
const App = (props) =>{  
    return <div>
        { props.loading? <div> 載入中... </div> : null }
    </div>
}

// 調用組件
<App loading={ false } />
```

### props.children  
`props.children`是組件的一個屬性，`children`就是組件的子元素。

如果組件在調用時嵌套了子元素，那麼我們需要在組件中獲取並渲染它，子元素才會顯示出來。

```js
// 渲染子元素
const App = (props) =>{
    return <div>
        { props.children }
    </div>
}

// 調用時嵌套子元素
<App>
  <div> hello，我是APP組件的子元素 </div>
</App>
```
