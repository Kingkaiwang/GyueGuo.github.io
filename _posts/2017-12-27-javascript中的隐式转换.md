---
layout: post
title: javascript中的隐式转换
date: 2017-12-27
categories: blog
tags: [javascript]
description: javascript中的隐式转换
---

#### javascript中**不同数据类型**之间进行**比较**、**运算**时会发生隐式转换。

具体是调用对象的`valueOf`和`toString`放来获取原始值，如果返回的值不为基本数据类型则调用另一个方法。

- `valueOf` 返回最适合对象的原始值
- `toString` 以字符串形式返回对象的原始值
- 字符串运算中优先调用`toString`方法
- 数值运算中优先调用`valueOf`方法
- 字符串与数值运算优先调用`toString`方法
<div id="jump"></div>
### toString
| 对象类型        | 返回值             |
| ----------- |:--------------------:|
| Array       | 数组的元素被转换为字符串，这些字符串由逗号分隔，连接在一起。其操作与 Array.toString 和 Array.join 方法相同   |
| Object      | 返回"[object ObjectName]"，其中 ObjectName 是对象类型的名称。  |
| Date        | 返回日期的文本表示 （"Wed Dec 27 2017 15:09:48 GMT+0800 (中国标准时间)"）  |
| Functon     | 字符串形式函数本身  |
| Boolean     | 字符串形式Boolean  |
| Number      | 回数值的字符串表示。还可返回以指定进制表示的字符串  |
| String      | String 对象的值   |

### valueOf
| 对象类型        | 返回值             |
| ----------- |:--------------------:|
| Array       | 数组本身              |
| Object      | 对象本身              |
| Date        | 返回1970年1月1日午夜开始计的UTC毫秒数， 与getTime返回值相同  |
| Functon     | 函数本身              |
| Boolean     | Boolean              |
| Number      | Number               |
| String      | String               |


### 比较时转换规则如下：

![转换规则](/img/2017122701.png)
也就是说 不同类型之间运算、比较前，引擎按如上规则进行转换为相同类型后再做运算、比较;

#### 特殊情况:
- 除空字符串(''),NaN,0，null,undefined这几个以外，其他类型转换为Boolean类型返回的都是true;
- undefined和null 比较返回true，二者和其他值比较返回false
```javascript
[] == false;  // true  [] -> '' -> false == false
![] == false;  // true  [] -> !true -> false == false
undefined == null; //true
```

### 运算时转换规则如下：

> 不同类型的基础数据之间的加法，数据先转换为number，然后转换为string(如果有string类型数据参与运算)

> 对象参与基础类型数据运算，先转化为基础类型。先调用其valueOf方法，如果返回的不是基础类型，再调用其toString方法,如果返回的还不是基础类型，则抛出错误。但是，Date数据刚好相反

其它类型转化数字
| 对象类型        | 返回值             |
| ----------- |:--------------------:|
| undefined       | NaN   |
| null      | 0  |
| false        | 0 |
| true     | 1  |
| 数字串     | 相应的数字  |
| 不能转化的字符串      | 	   |
| String      | String   |

其它类型转化为字符串
[参照toString](#jump)
