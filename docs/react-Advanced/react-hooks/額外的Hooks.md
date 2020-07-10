# 額外的Hooks

* useMemo  
* useCallback  
* useRef  
* useImperativeMethods  
* useLayoutEffect   

## useMemo    

useMemo是一個用於性能最佳化的API，它透過`記憶值`手段讓你避免在每個渲染上執行高開銷的計算，可減少渲染的耗時。

尤其適合用在需要複雜計算的場景，比如`複雜的列表渲染`，對象深拷貝等等。

##### 基本用法  
```js
const memoizedValue = useMemo(callback,array);
```
> 1，callback： 一個函數，用於處理你的計算邏輯。      

> 2，array： 一個數組，當數組發生改變時useMemo才會重新執行。     

useMemo的返回值是一個記憶值，它是callback的返回值。  

useMemo只會在數組發生變化時才會重新計算memoized(記憶)值。這樣的最佳化有助於避免在每個渲染上進行昂貴的計算。

下面是一個用例：  
```js
// useMemo只會在obj1或obj2發生改變時才會重新執行。 

const obj1 = { id:"12", name:"jack" };
const obj2 = { id:"14", name:"ben", age:23 };

const memoizedValue = useMemo(()=>Object.assign(obj1,obj2),[obj1,obj2]);

// 使用
<div> { memoizedValue.name } </div>
```

> 注意：不要在useMemo裡面處理副作用的邏輯，副作用應該放在useEffect內處理。   

<br/>      
## useCallback  
useCallback和useMemo一樣，都是用於性能最佳化的API。
##### 基本用法  
```js
const memoizedCallback = useCallback(callback,array);
```  
> 1，callback： 一個函數，用於處理你的計算邏輯。      

> 2，array： 一個數組，當數組發生改變時useCallback才會重新執行。      

useCallback 和 useMemo 類似，它們的返回值都是記憶化的。但是會有一些不同，useMemo的返回值就是callback的返回值，而useCallback的返回值則callback函數本身。    

`useCallback(fn, inputs)` 等價於 `useMemo(() => fn, inputs)`。
   
<br/>    

下面是useCallback一個案例：
```js
const obj1 = { id:"12", name:"jack" };
const obj2 = { id:"14", name:"ben", age:23 };

const memoizedFn = useCallback(()=>Object.assign(obj1,obj2),[obj1,obj2]);  

// 使用
<div>{ memoizedFn().name }</div>
```
它相當於useMemo的這種寫法：  
```js
const obj1 = { id:"12", name:"jack" };
const obj2 = { id:"14", name:"ben", age:23 };

const memoizedFn = useMemo(()=>{
    return ()=>{
        return Object.assign(obj1,obj2)
    }
},[obj1,obj2]);  
// 或
const memoizedFn = useMemo(()=>()=>Object.assign(obj1,obj2),[obj1,obj2]);

// 使用
<div>{ memoizedFn().name }</div>
```
<br/> 

## useRef  

useRef 返回一個可變的 ref 對象，其 .current 屬性被初始化為傳遞的參數（initialValue)。

基本用法:  
```js
const MyComponent = () =>{
    // 1，創建ref
    const inputEl = useRef(null);
    const onInput = () =>{
        // 3，訪問ref
        console.log(inputEl.current.value)
    }
    // 2，掛載ref
    return (
        <div>
            <input ref={ inputEl } type="text" />
            <p>
                <button onClick={ onInput } > 獲取input的值 </button>
            </p>
        </div>
    )
}
```

<br/> 

## useImperativeMethods

useImperativeMethods是一個用於拓展ref實例的API，它能夠讓你自訂`使用 ref 時公開給父組件的實例值`。

下面是它的一個用例：  
```js
function FancyInput(props, ref) {
  const inputRef = useRef();
  useImperativeMethods(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    }
  }));
  return <input ref={inputRef} ... />;
}
FancyInput = forwardRef(FancyInput);
```

<br/> 

## useLayoutEffect 
useLayoutEffect 與 useEffect 基本相同，但它在所有 DOM 變化後同步觸發。 它能夠從 DOM 讀取布局並同步重新渲染。 在瀏覽器有機會繪製之前，將在 useLayoutEffect 內部計劃的更新將同步刷新。

在多數情況下首選標準的 useEffect ，以避免阻止視覺更新。  

下面是useLayoutEffect 的一個案例：
```js
useLayoutEffect(() => {
    const rootEl = document.getElementById("root");
    console.log(rootEl.);
  },[])
```
