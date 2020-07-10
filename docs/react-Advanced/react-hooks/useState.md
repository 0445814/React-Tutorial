# useState - 組件狀態管理  

`useState`使函數組件能夠使用state。

下面是它的一個基本結構：  

```js
const [state, setState] = useState(initState);
```
> 1，state為你要設置的狀態

> 2，setState為更新state的方法，命名隨意  

> 3，initState為初始的state，可以是任意數據類型，也可以是回調函數，但必須有返回值

下面是一個具體的例子：
```js
import { useState } from 'react';

const Example = () =>{  
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>你點擊了{count}次</p>
      <button onClick={() => setCount(count + 1)}>
        點擊
      </button>
    </div>
  );
}
```

