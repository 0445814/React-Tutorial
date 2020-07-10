# react組件生命週期

### 基本概念
每個人都有一個生命週期，那就是從出生到死亡。

react組件也有生命週期，從組件初始化到組件渲染完成，再到組件卸載就是一個完整的react組件生命週期。  

> 需要注意的是，class組件自帶生命週期，但是函數組件因為是純函數，需要借助`react hook`才能實現生命週期部分功能。

react組件生命週期主要分為三個階段，分別是初始化階段、組件更新階段、組件卸載階段。每個階段都有不同的生命週期方法。

[cinwell website](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram ':include :type=iframe width=100% height=900px')

### Mounting(裝載) `初始化階段` 
一些初始化工作，包括dom渲染，獲取數據、填充數據等等。
> 1，constructor  `構造函數`

> 2，static getDerivedStateFromProps() 【新】 `初始化、props或state改變時執行`  

> 3，componentWillMount() / UNSAFE_componentWillMount() 【將廢棄】`組件渲染前執行`  

> 4，render() `渲染函數`

> 5，componentDidMount()  `渲染完成後執行`

### Updating(更新) `組件更新階段`
props或state的改變可能會引起組件的更新，組件重新渲染的過程中會調用以下方法：
> 1，componentWillReceiveProps() / UNSAFE_componentWillReceiveProps() 【將廢棄】 `props改變時執行`

> 2，static getDerivedStateFromProps() 【新】 `初始化、props或state改變時執行`  

> 3，shouldComponentUpdate()  `props或state更新時執行`

> 4，componentWillUpdate() / UNSAFE_componentWillUpdate() 【將廢棄】 `組件更新前執行` 

> 5，render()  `渲染函數`

> 6，getSnapshotBeforeUpdate() 【新】  `組件更新前執行` 

> 7，componentDidUpdate()  `組件更新完畢後執行` 

### Unmounting(卸載) `組件卸載階段`  
> componentWillUnmount()  `組件卸載前執行` 

### 錯誤處理 

> componentDidCatch()  `捕獲組件錯誤訊息` 
