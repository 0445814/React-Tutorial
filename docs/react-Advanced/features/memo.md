# React.memo  

React.memo 是一個高階組件。它的主要作用在於性能最佳化，和React.PureComponent 類似，不同的是React.memo包裹函數式組件，而不是類組件。

如果傳入的props沒有變化，則會跳過渲染，使用上一次渲染結果。

下面是一個案例： 
```js
const MyComponent = React.memo((props)=>{
    return (
        <div>
            被最佳化的函數組件
        </div>
    )
});
```

#### 自訂比較函數
```js
const MyComponent = (props) =>{
    return (
        <div>
            { props.name }
        </div>
    )
}  

// 比較函數
const areEqual = (prevProps, nextProps) =>{

   if(prevProps.name !== nextProps.name){
       // 和類組件的shouldComponentUpdate() 方法不同，如果不相等則返回false
       return false;
   }
}
export default React.memo(MyComponent, areEqual);

```

