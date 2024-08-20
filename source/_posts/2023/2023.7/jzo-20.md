---
title: 判断表示数值的字符串
tags:
  - c
categories:
  - 算法
cover: 'https://miaomiao-1-1319022947.cos.ap-beijing.myqcloud.com/202307102301.jpg'
abbrlink: 86af2470
date: 2023-07-10 22:35:09
---
这是一道来自leetcode的题目（嘎嘎），官方的做法是利用有限状态机做，俺一开始想用正则表达式匹配，但是没配上，记录一下讲解的思路。

# 题目描述

实现一个函数用来判断字符串是否表示数值（包括整数和小数）。

数值（按顺序）可以分成以下几个部分：

- 若干空格

- 一个小数或者整数

- （可选）一个 'e' 或 'E' ，后面跟着一个整数

- 若干空格

小数（按顺序）可以分成以下几个部分：

- （可选）一个符号字符（'+' 或 '-'）
- 下述格式之一：
    至少一位数字，后面跟着一个点 '.'
    至少一位数字，后面跟着一个点 '.' ，后面再跟着至少一位数字
    一个点 '.' ，后面跟着至少一位数字

整数（按顺序）可以分成以下几个部分：

- （可选）一个符号字符（'+' 或 '-'）

- 至少一位数字


部分数值列举如下：

["+100", "5e2", "-123", "3.1416", "-1E-16", "0123"]

部分非数值列举如下：

["12e", "1a3.14", "1.2.3", "+-5", "12e+5.4"]

# 思路描述

有限状态机，有限状态机，相信接触过 verilog 语言或是数字电路的人应该会对此有印象，并用纸笔/ verilog 语言搭建了~~状态混乱的~~有限状态机。

好吧，其实在这里，看看如何到达判定为“是数值的状态”，看看转移规则。因为这里状态和转移方式太多了，所以用图表示。严格按照定义逐步写出即可，其实也是正则表达式的思路。

![](https://miaomiao-1-1319022947.cos.ap-beijing.myqcloud.com/20230710233307Sam.jpg)

# 思考

或许这样设定状态机的方法比正则要简单（前提是能想到）。于我，使用正则表达式的困难在于：语法不清楚且构建时结构混乱，呱呱。
