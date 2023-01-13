---
title: Excel表列
categories: 算法
tags:
  - 数学
  - JavaScript
  - 进制转换
abbrlink: 2506288334
date: 2023-01-11 22:15:57
---
### Excel表列名称和序号的相互转换

---
#### Excel表列名称
给你一个整数 columnNumber ，返回它在 Excel 表中相对应的列名称。
例如：
```
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
...
```
示例 1：
```
输入：columnNumber = 1
输出："A"
```
示例 2：
```
输入：columnNumber = 28
输出："AB"
```
示例 3：
```
输入：columnNumber = 701
输出："ZY"
```
示例 4：
```
输入：columnNumber = 2147483647
输出："FXSHRXW"
```
提示：

+ 1 <= columnNumber <= 231 - 1

##### 解题思路
---
首先看清楚问题的本质在于26进制的转换，对给定的columnNumber进行求余找出对应的字母，但值得注意的是此时'A'对应的是0，因此是[0,25]的26进制，所以只要在处理每一位的时候进行减 1，就可以按照正常的 26 进制来处理

---
##### 代码
```
/**
 * @param {number} columnNumber
 * @return {string}
 */
var convertToTitle = function (columnNumber) {
    let res = []
    while (columnNumber--) {
        res.push(String.fromCharCode(columnNumber % 26 + 'A'.charCodeAt()))
        columnNumber = Math.floor(columnNumber / 26)
    }
    return res.reverse().join('')
};
```
---
#### Excel表列序号
给你一个字符串 columnTitle ，表示 Excel 表格中的列名称。返回 该列名称对应的列序号 。
例如：
```
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
...
```
示例 1:
```
输入: columnTitle = "A"
输出: 1
```
示例 2:
```
输入: columnTitle = "AB"
输出: 28
```
示例 3:
```
输入: columnTitle = "ZY"
输出: 701
```
提示：
+ 1 <= columnTitle.length <= 7
+ columnTitle 仅由大写英文组成
+ columnTitle 在范围 ["A", "FXSHRXW"] 内
##### 解题思路
---
我们已经知道Excel表列的本质就是一个26进制，因此只需要进行简单的循环遍历即可，值得注意的是，通过方法找到对应的code数值是同初始'A'的code数值进行做差后，需要加一

---
##### 代码
```
/**
 * @param {string} columnTitle
 * @return {number}
 */
var titleToNumber = function (columnTitle) {
    let res = 0
    for (let i = 0; i < columnTitle.length; i++) {
        res = res * 26 + columnTitle.charCodeAt(i) + 1 - 'A'.charCodeAt()
    }
    return res
};
```
---

