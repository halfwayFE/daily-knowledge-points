# Promise

> Promise是一种异步处理方案，起源于社区，ES6后ECMAScript原生支持Promise对象

Promise解决的问题
1. 回调地狱
2. 解决回调函数执行多次的问题（Promise只能改变一次状态）

Promise的局限性
1. Promise的内部错误不会被外部捕获
2. Promise一旦新建无法中途取消
3. 无法得知pending时进展到哪个阶段，是刚开始还是即将完成


## 题目
将callback语法的方法改成Promise语法
```javascript
// 获取用户的方法，callback语法，使用时需要传入回调函数拿到用户信息
function fetchUser(cb) {
  setTimeout(() => {
    cb(null, [{ name: '张三' }])
  }, 1500);
};

// promisify方法
function promisify(origin) {
  return function(...args) {
    return new Promise((resolve, reject) => {
      args.push(function callback(err, result) {
        if(err) {
          return reject(err)
        }
        return resolve(result)
      })
      origin.call(this, ...args);
    })
  }
}

const promisifyFetchUser = promisify(fetchUser);

promisifyFetchUser().then(res => { console.log('用户数据：', res) })

```