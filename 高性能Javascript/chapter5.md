# 字符串和正则表达式
* regular expression (regex)
* 每个浏览器都实现了自己的正则表达式引擎

## 字符串合并常用方法
1、+, +=
2、Array.join
3、str.concat

## 正则表达式优化
###  正则表达式工作原理
1、编译：浏览器正则表达式引擎，会将正则表达式编译为可执行代码，用于执行匹配工作；如果我们将定义的正则表达式赋值给变量，可以避免重复编译
2、设置起始位置：
```
* lastIndex 代表下一次匹配的开始索引，只对全局正则起作用，是可读可写的
* lastIndex 可写：对于exec, test方法，如果正则是全局正则，从第二次执行该方法，可以通过设置 lastIndex 配置正则匹配的起始位置
* 第一次匹配，引擎会自动查找匹配的开始位置，并返回lastIndex
* 各大浏览器厂商对正则表达式引擎的算法都进行了优化，其中一点是在开始就决定跳过一些不必要的步骤，避免大量无意义的工作，比如：以 ^ 开始的正则表达式，会先判断起始位置是否匹配，如果起始位置匹配失败，则可以避免后续无意义的工作。另一个例子：匹配第三个字母是 x的字符串：先找到x的位置，然后将起始位置回退两个字符。
```
3、匹配每个正则表达式字元
* 一旦确定匹配开始位置，引擎边开始逐字对每个正则表达式模式进行匹配，如果其中一个模式匹配失败，则试着回溯到之前尝试匹配的地方，进行另一个模式的匹配
4、匹配成功或失败
* 如果在字符串中发现一个完全匹配，则宣布匹配成功
* 如果正则表达式的所有模式都匹配失败，则回退到第2步，从起始位置的下一个字符开始重新匹配
* 只有当字符串中每个字符（包括最后一个字符后面的位置）都经历匹配失败的过程，还没有匹配成功，则宣告匹配失败

### 回溯
```
概念：分支(|)、量词（+?, +, {2,}）
决策点
```
1、分支与回溯过程
2、重复和回溯过程

