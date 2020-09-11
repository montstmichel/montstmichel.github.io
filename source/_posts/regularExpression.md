---
title: 正则表达式（JavaScript）
date: 2019-09-20 23:02:50
tags:
- JavaScript
- 笔记
---
### 正则表达式
**正则表达式**（ regular Expression）是用来匹配字符串中字符组合的模式。
在 **JavaScript** 中，正则表达式也是**对象**

#### 1. 用处：
1. 正则表达式通常被用来检索、替换那些符合某个模式（规则）的文本，例如验证表单：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文(匹配)。
2. 正则表达式还常用于过滤掉页面内容中的一些敏感词(替换)
3. 从字符串中获取我们想要的特定部分(提取)
#### 2. 正则表达式在js中的使用
##### 2.1 正则表达式的创建
1. 通过调用 RegExp 对象的构造函数创建    
```
var regexp = new RegExp(/123/)
```
2. 利用字面量创建 正则表达式
```
var re = /123/
```
##### 2.2 测试正则表达式
RegExpObj.test(str) 正则对象方法，用于检测字符串是否符合该规则，该对象会返回 true 或 false，其参数是测试字符串。
#### 3. 正则表达式中的特殊字符
##### 3.1 正则表达式的组成（边界符）
边界符     | 说明
-------- | -----
^  | 表示匹配行首的文本（以谁开始）
$  | 表示匹配行尾的文本（以谁结束）
如果 ^和 $ 在一起，表示必须是精确匹配。
```
<script>
        // 边界符 ^ $ 
        var rg = /abc/; // 正则表达式里面不需要加引号 不管是数字型还是字符串型
        // /abc/ 只要包含有abc这个字符串返回的都是true
        console.log(rg.test('abc'));
        console.log(rg.test('abcd'));
        console.log(rg.test('aabcd'));
        console.log('---------------------------');
        var reg = /^abc/;
        console.log(reg.test('abc')); // true
        console.log(reg.test('abcd')); // true
        console.log(reg.test('aabcd')); // false
        console.log('---------------------------');
        var reg1 = /^abc$/; // 精确匹配 要求必须是 abc字符串才符合规范
        console.log(reg1.test('abc')); // true
        console.log(reg1.test('abcd')); // false
        console.log(reg1.test('aabcd')); // false
        console.log(reg1.test('abcabc')); // false
</script>
```
##### 3.2 字符类

###### 1. [ ] 方括号
-  方括号 [ ] 表示有一系列字符可供选择，只要匹配其中一个就可以了
- ^ 在 [^] 方括号内部表示取反符
```
<script>
        //var rg = /abc/;  只要包含abc就可以 
        // 字符类: [] 表示有一系列字符可供选择，只要匹配其中一个就可以了
        var rg = /[abc]/; // 只要包含有a 或者 包含有b 或者包含有c 都返回为true
        console.log(rg.test('andy')); // true
        console.log(rg.test('baby')); // true
        console.log(rg.test('color')); // true
        console.log(rg.test('red')); // false
        var rg1 = /^[abc]$/; // 三选一 只有是a 或者是 b  或者是c 这三个字母才返回 true
        console.log(rg1.test('aa')); // false
        console.log(rg1.test('a')); // true
        console.log(rg1.test('b')); // true
        console.log(rg1.test('c')); // true
        console.log(rg1.test('abc')); // false
        console.log('------------------');

        var reg = /^[a-z]$/; // 26个英文字母任何一个字母返回 true  - 表示的是a 到z 的范围  
        console.log(reg.test('a')); // true
        console.log(reg.test('z')); // true
        console.log(reg.test(1)); // false
        console.log(reg.test('A')); // false
        // 字符组合
        var reg1 = /^[a-zA-Z0-9_-]$/; // 26个英文字母(大写和小写都可以)任何一个字母返回 true  
        console.log(reg1.test('a')); // true
        console.log(reg1.test('B')); // true
        console.log(reg1.test(8)); // true
        console.log(reg1.test('-')); // true
        console.log(reg1.test('_')); // true
        console.log(reg1.test('!')); // false
        console.log('----------------');
        // 如果中括号里面有^ 表示取反的意思 千万和 我们边界符 ^ 别混淆
        var reg2 = /^[^a-zA-Z0-9_-]$/;
        console.log(reg2.test('a'));; // false
        console.log(reg2.test('B'));; // false
        console.log(reg2.test(8));; // false
        console.log(reg2.test('-'));; // false
        console.log(reg2.test('_'));; // false
        console.log(reg2.test('!')); // true
</script>
```
###### 2. 量词符
量词符用来设定某个模式出现的次数。
量词符| 说明
-------- | -----
*  | 重复0次或更多次
+  | 重复1次或更多次
？  | 重复0次或1次
{n}  | 重复n次
{n,}  | 重复n次或更多次
{n,m}  | 重复n到m次(中间不要有空格)
```
<script>	
        // 量词符: 用来设定某个模式出现的次数
        var reg = /^a$/;
        console.log(reg.test('a')); // true
        console.log(reg.test('aa')); // false


        // 1. * 相当于 >= 0 可以出现0次或者很多次 
        var reg = /^a*$/;
        console.log(reg.test('')); // true
        console.log(reg.test('a')); // true
        console.log(reg.test('aa')); // true
        console.log(reg.test('aaaaaa')); // true

        // 2. + 相当于 >= 1 可以出现1次或者很多次
        var reg = /^a+$/;
        console.log(reg.test('')); // false
        console.log(reg.test('a')); // true
        console.log(reg.test('aa')); // true
        console.log(reg.test('aaaaaa')); // true

        // 3. ?  相当于 1 || 0
        var reg = /^a?$/;
        console.log(reg.test('')); // true
        console.log(reg.test('a')); // true
        console.log(reg.test('aa')); // false
        console.log(reg.test('aaaaaa')); // false

        // 4. {3 } 就是重复3次
        var reg = /^a{3}$/;
        console.log(reg.test('')); // false
        console.log(reg.test('a')); // false
        console.log(reg.test('aa')); // false
        console.log(reg.test('aaaaaa')); // false
        console.log(reg.test('aaa')); // true

        // 5. {3, }  大于等于3
        var reg = /^a{3,}$/;
        console.log(reg.test('')); // false
        console.log(reg.test('a')); // false
        console.log(reg.test('aa')); // false
        console.log(reg.test('aaaaaa')); // true
        console.log(reg.test('aaa')); // true
        
        // 6. {3, 16}  大于等于3 并且 小于等于16

        var reg = /^a{3,16}$/;
        console.log(reg.test('')); // false
        console.log(reg.test('a')); // false
        console.log(reg.test('aa')); // false
        console.log(reg.test('aaaaaa')); // true
        console.log(reg.test('aaa')); // true
        console.log(reg.test('aaaaaaaaaaaaaaaaaaaaa')); // false
</script>
 ```
 ```
<script>
        //  量词是设定某个模式出现的次数
        var reg = /^[a-zA-Z0-9_-]{6,16}$/; // 这个模式用户只能输入英文字母 数字 下划线 短横线但是有边界符和[] 这就限定了只能多选1
        // {6,16}  中间不要有空格
        // console.log(reg.test('a'));
        // console.log(reg.test('8'));
        // console.log(reg.test('18'));
        // console.log(reg.test('aa'));
        // console.log('-------------');
        // console.log(reg.test('andy-red'));
        // console.log(reg.test('andy_red'));
        // console.log(reg.test('andy007'));
        // console.log(reg.test('andy!007'));
</script>
```
###### 3. 括号总结
1.大括号  量词符.  里面表示重复次数

2.中括号 字符集合。匹配方括号中的任意字符. 

3.小括号表示优先级
```
<script>
        // 中括号 字符集合.匹配方括号中的任意字符. 
        // var reg = /^[abc]$/;
        // a 也可以 b 也可以 c 可以  a ||b || c
        // 大括号  量词符. 里面表示重复次数
        // var reg = /^abc{3}$/; // 它只是让c重复三次   abccc
        // console.log(reg.test('abc'));
        // console.log(reg.test('abcabcabc'));
        // console.log(reg.test('abccc'));

        // 小括号 表示优先级
        var reg = /^(abc){3}$/; // 它是让abcc重复三次
        console.log(reg.test('abc'));
        console.log(reg.test('abcabcabc'));
        console.log(reg.test('abccc'));
</script>
```
##### 3.3 预定义类
项目     | Value
-------- | -----
\d  | 匹配0-9之间的任一数字，相当于[0-9]。
\D  | 匹配所有0-9以外的字符，相当于[^0-9]。
\w  | 匹配任意的字母、数字和下划线，相当于[A-Za-z0-9_]
\W  | 除所有字母、数字和下划线以外的字符，相当于[^A-Za-z0-9_]
\s  | 匹配空格（包括换行符、制表符、空格符等），相当于[\t\r\n\v\f]
\S  | 匹配非空格的字符，相当于[^\t\r\n\v\f]
```
<script>
        // 座机号码验证:  全国座机号码  两种格式:   010-12345678  或者  0530-1234567
        // 正则里面的或者 符号  |  
        // var reg = /^\d{3}-\d{8}|\d{4}-\d{7}$/;
        var reg = /^\d{3,4}-\d{7,8}$/;
</script>
```
