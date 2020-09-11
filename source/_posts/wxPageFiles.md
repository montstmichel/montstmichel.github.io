---
title: 微信页面文件组成
date: 2019-11-13 12:22:50
image: http://ww1.sinaimg.cn/large/006reQWdgy1gin5n7zvgyj30xz0pagrv.jpg
tags:
- 小程序 
- 笔记
---
## 1. [page-name].js
**页面逻辑文件，用于创建页面对象，以及处理页面生命周期控制和数据处理**
```
// index.js
// 获取应用实例
// 完成页面的逻辑，包括功能的实现
var app = getApp()
Page()
```
## 2. [page-name].wxml
**语法遵循XML语法，不是HTML语法**
```
<!--index.wxml-->
<!-- wxml: wei xin markup language -->
<!-- 基于XML语法，用来定义界面结构 -->
<view class="container">
</view>
```
## 3. [page-name].json （可选）
**设置当前页面工作时的window的配置，此处会覆盖app.json中的window设置，也就是说只可以设置window中设置的属性**
```
{
	"navigationBarTitileText": "查看启动日志"
}
```
## 4. [page-name].wxss	（可选）

**wxss指的是Wei Xin Style Sheet
用于定义页面样式的，语法遵循CSS语法，扩展了CSS基本用法和长度单位 （主要就是rpx响应式像素）**
```
/**index.wxss**/
/* 完全遵循CSS语法，单位这点比CSS高级 */
/* 用于定义页面样式 */
.userinfo {
}
```