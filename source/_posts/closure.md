---
title: 闭包
date: 2019-09-13 22:58:49
image: http://ww1.sinaimg.cn/large/006reQWdgy1gipf5dc68ij31210p90u0.jpg
tags:
- JavaScript
- 笔记
---
##### 1 变量作用域
1. 函数内部可以使用全局变量
2. 函数外部不可以使用局部变量
3. 当函数执行完毕，本作用域内的局部变量会销毁
##### 2 什么是闭包
**闭包（closure）指有权访问另一个函数作用域中变量的函数。-----	JavaScript高级程序设计**
简单理解就是，一个作用域可以访问另外一个函数内部的局部变量。
```
<script>
        // 闭包（closure）指有权访问另一个函数作用域中变量的函数。
        // 闭包: 我们fun 这个函数作用域 访问了另外一个函数 fn 里面的局部变量 num
        // 闭包是函数fn
        function fn() {
            var num = 10;

            function fun() {
                console.log(num);

            }
            fun();
        }
        fn();
</script>
 ```
 ##### 3 闭包的作用
 **我们fn 外面的作用域可以访问fn 内部的局部变量
 闭包的主要作用: 延伸了变量的作用范围**
 ```
 <script>
        function fn() {
            var num = 10;

            // function fun() {
            //     console.log(num);

            // }
            // return fun;
            return function() {
                console.log(num);
            }
        }
        var f = fn();
        f();
        // 类似于
        // var f = function() {
        //         console.log(num);
        //     }
        // var f =  function fun() {
        //         console.log(num);

        //     }
</script>
```
##### 4. 闭包案例
###### 1. 循环注册点击事件
###### 2. 循环中的 setTimeout()
###### 3. 计算打车价格（封装函数）
