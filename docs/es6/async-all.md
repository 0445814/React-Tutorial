##### 1，回调式异步处理
```js  
// 回调式异步处理
ajax('http://url-1', data1, function (err, result) {
    if (err) {
        return handle(err);
    }
    // 做一些事情
    ajax('http://url-2', data2, function (err, result) {
        if (err) {
            return handle(err);
        }
        // 做一些事情
        ajax('http://url-3', data3, function (err, result) {
            if (err) {
                return handle(err);
            }
            // 做一些事情
            ....
        });
    });
});
```  
##### 2，promise异步处理
```js
// promise异步处理
fetch('http://url-1',args) 
 .then(data1=>{
    // data1
    return fetch('http://url-2',data1);
 })
 .then(data2=>{
   // data2
   return fetch('http://url-2',data2);
 })
 .then(data3=>{
   // data3
 })
 ...

```
##### 3，generator异步处理
```js
// generator异步处理。
// 以同步的效果处理异步(实际上还是异步的)
function* (){
  try {
    r1 = yield ajax('http://url-1', data1);
    r2 = yield ajax('http://url-2', data2);
    r3 = yield ajax('http://url-3', data3);
    console.log(r3);
  }
  catch (err) {
    console.log(err);
  }
}
```
##### 4，async/await异步处理
```js
// 终极解决方案。
// 以同步的效果处理异步(实际上还是异步的)
async function (){
  try {
    r1 = await ajax('http://url-1', data1);
    r2 = await ajax('http://url-2', data2);
    r3 = await ajax('http://url-3', data3);
    console.log(r3);
  }
  catch (err) {
    console.log(err);
  }
}
```