---
title: closure
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
```
<ul class="nav">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
</ul>
<script>
        // 闭包应用-点击li输出当前li的索引号
        // 1. 我们可以利用动态添加属性的方式
        var lis = document.querySelector('.nav').querySelectorAll('li');
        for (var i = 0; i < lis.length; i++) {
            lis[i].index = i;
            lis[i].onclick = function() {
                // console.log(i);
                console.log(this.index);

            }
        }
        // 2. 利用闭包的方式得到当前小li 的索引号
        for (var i = 0; i < lis.length; i++) {
            // 利用for循环创建了4个立即执行函数
            // 立即执行函数也成为小闭包因为立即执行函数里面的任何一个函数都可以使用它的i这变量
            (function(i) {
                // console.log(i);
                lis[i].onclick = function() {
                    console.log(i);

                }
            })(i);
        }
</script>
```
###### 2. 循环中的 setTimeout()
异步任务触发是执行：1. 回调函数	2.定时器、事件（鼠标点击，经过）中的回调函数	3.ajax中的回调函数
```
<script>
        // 闭包应用-3秒钟之后,打印所有li元素的内容
        var lis = document.querySelector('.nav').querySelectorAll('li');
        for (var i = 0; i < lis.length; i++) {
            (function(i) {
                setTimeout(function() {
                    console.log(lis[i].innerHTML);
                }, 3000)
            })(i);
        }
</script>
```
###### 3. 计算打车价格（封装函数）
```
<script>
        // 闭包应用-计算打车价格 
        // 打车起步价13(3公里内),  之后每多一公里增加 5块钱.  用户输入公里数就可以计算打车价格
        // 如果有拥堵情况,总价格多收取10块钱拥堵费
        // function fn() {};
        // fn();
        var car = (function() {
            var start = 13; // 起步价  局部变量
            var total = 0; // 总价  局部变量
            return {
                // 正常的总价
                price: function(n) {
                    if (n <= 3) {
                        total = start;
                    } else {
                        total = start + (n - 3) * 5
                    }
                    return total;
                },
                // 拥堵之后的费用
                yd: function(flag) {
                    return flag ? total + 10 : total;
                }
            }
        })();
        console.log(car.price(5)); // 23
        console.log(car.yd(true)); // 33

        console.log(car.price(1)); // 13
        console.log(car.yd(false)); // 13
</script>
```
