# Portals(插槽)

Portals 提供了一種很好的方法，能夠將子節點渲染到父組件以外的 DOM 節點。   

Portals主要依賴`ReactDOM.createPortal(child, container)`方法來實現。

<br />

#### ReactDOM.createPortal(child, container)

參數說明：  
> child: 你要插入的`React DOM`，可以是jsx、字串或者片段 。    

> container: 你要插入的位置，必須是真實存在的`DOM`，比如`body`。

下面是一個案例：  

```js
import React from 'react';
import { createPortal } from 'react-dom';

const Portals = () =>{
    return createPortal(
        <div> 
            給<body></body>插入一段文字
        </div>,
        document.body
    )
}

export default Portals;
```

