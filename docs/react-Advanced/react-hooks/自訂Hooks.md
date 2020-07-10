# 自訂hooks  

自訂的hooks是一個 JavaScript 函數，其名稱以 `use` 開頭，函數內可以調用其他 Hook。

主要就是利用react hooks封裝成一個具有特定邏輯的，或可重用的函數。

下面是官方的一個案例，查詢指定用戶是否在線上：
```js
import { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null); 

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    // 訂閱
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      // 組件卸載時取消訂閱
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

案例應用：
```js
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```