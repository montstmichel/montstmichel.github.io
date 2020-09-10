---
title: 微信小程序项目结构
date: 2019-11-10 12:10:08
tags: 
- 小程序 
- 笔记
---
![wxstructure.png](http://ww1.sinaimg.cn/large/006reQWdgy1gilfm6r8y0j30ra0min17.jpg)
## 1. 逻辑 app.js
**调用一个App的方法（全局方法）**
```
// app.js
var obj = {}

// 调用一个App的方法（全局方法）
App(obj)

// 调用App方法的作用就是用来创建应用程序实例对象
// 定义应用程序的生命周期事件
```
## 2. 样式 app.wxss
```
/**app.wxss**/
/* 样式文件 */
/* CS3 flex布局 */
/* 定义全局共享样式，公用样式 */
.container {
}
```