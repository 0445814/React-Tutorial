# Suspense和lazy

React官方提供了`React.lazy`和`React.Suspense`來實現代碼分割。  

### React.lazy 

React.lazy允許你將`動態import()`渲染為常規組件。

下面是一個案例：
```js
const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <div>
      <OtherComponent />
    </div>
  );
}
```

> 需要注意的是，目前通過 React.lazy 載入的組件，需要在Suspense裡面使用，否則報錯

目前`React.lazy`和`React.Suspense`還不支持服務端渲染，如果你使用的是服務端渲染，可以使用[loadable-components](https://github.com/smooth-code/loadable-components)方案。

### React.Suspense

Suspense主要有三個功能：
> 1，配合`React.lazy`實現代碼分割

> 2，載入指示符(類似`loading`載入狀態)   

> 3，數據獲取 (預計在v16.9版本中實現) 

##### 1，結合React.lazy實現代碼分割
```js
const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <div>
      <React.Suspense fallback={<div> Loading... </div>}>
        <div>
            <OtherComponent />
        </div>
        </React.Suspense>
    </div>
  );
}
```

##### 2，載入指示符(loading狀態)  

調用`Suspense`組件時我們需要給它添加一個`fallback`屬性，它的值是一個指示符組件。  

下面是一個案例：
```js
const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    // 顯示<Spinner> 直到載入其他組件
    <React.Suspense fallback={<Spinner />}>
      <div>
        <OtherComponent />
      </div>
    </React.Suspense>
  );
}
```
> 注意：目前React.Suspense是React.lazy的唯一用例。  






