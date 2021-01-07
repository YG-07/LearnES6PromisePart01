# LearnES6PromisePart01
学习ES6 Promise
  
### 一.资料整理来源  
coderwhy老师  B站账号：ilovecoding  
bilibili URL：https://space.bilibili.com/36139192  
视频(126-129p) URL：https://www.bilibili.com/video/BV15741177Eh?p=126  
  
# 二、本部分知识大纲
(数字表示视频URL分p)
### 一、Promise的结构和基本使用
(本节使用使用setTimeout定时器模拟不同请求时间的网络请求！)
* Promise简书 博客 URL：https://www.jianshu.com/p/1b63a13c2701
* Promise MDN文档 URL：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise
  
#### 1.1 Promise介绍
**Promise** 对象用于表示一个**异步操作**的最终`完成 (或失败)及其结果值`。  
  
#### 1.2 Promise的状态
 一个 Promise 对象代表一个在这个 promise 被创建出来时不一定已知的值。  
它让您能够把异步操作最终的成功返回值或者失败原因和相应的处理程序关联起来。  
一个 Promise 必然处于以下几种状态之一：
* **待定（pending）**: 初始状态，既没有被兑现，也没有被拒绝。
* **已兑现（fulfilled）**: 意味着操作成功完成。
* **已拒绝（rejected）**: 意味着操作失败。
  
#### 1.3 Promise的链式调用
1. Promise的基本使用结构：
```javaScript
new Promise((resolve, reject)=>{...})
  .then((..)=>{...}).then((..)=>{...}).then((..)=>{...})
  .catch(err => {...})
```
  
#### 1.4 Promise的链式调用补充
需求：多层网络请求，而且每次请求先自己处理，再进行网络请求(这里是拼接字符串)  
1. 对于多层请求，可返回一个new Promise对象
```javaScript
return new Promise(resolve => {
  resolve(res + '111')
})
```
2. 可简化，返回其**静态方法**Promise.resolve()
```javaScript
return Promise.resolve(res+'222')
```
3. 再简化，直接返回成功结果，Promise能自动进行resolve()的封装
```javaScript
return res+'333'
```
  
#### 1.5 Promise处理失败请求
1. 同上成功请求，使用new Promise(reject => {...})时，不会中断请求
2. 使用静态方法或throw语句,会中断请求
* 如：`return Promise.reject('ERROR: 3th request')`
* 如：`throw 'ERROR: 4th request'`
  
#### 1.6 静态方法Promise.all(iterable)
1. iterator:迭代器,可遍历的，.all([...])使用一个数组或可迭代的参数
2. 可同时处理多个网络请求，对不同状态进行处理，`都成功才调用.then()`，否则调用.catch()抛出异常请求结果
3. .all()的.then()方法接收的是所有请求的成功数据
```javaScript
.then(results => {
    for(result of results){
      console.log(result);
    }
  })
```
