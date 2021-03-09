# 001 JS数据类型
## 1.JS原始数据类型有哪些？引用数据类型有哪些？
    在 JS 中，存在基础数据类型和引用数据类型，分别是：
        基础数据类型：
            boolean
            null
            undefined
            number
            string
            symbol
        引用数据类型: 
            普通对象-Object
            数组对象-Array
            正则对象-RegExp
            日期对象-Date
            数学函数-Math
            函数对象-Function）
    数据类型分为两类存储
        基础类型存储在栈内存中被引用和拷贝会创建一个完全相等变量
        引用类型存储在堆内存中，存储的是地址，多个引用会指向同一个地址

## 2.数据类型检测
### 2.1 typeof 
        注意 typeof null // 'object' 是bug，null本身不是对象。
        如需判断请直接通过 === 'null' 判断就好
        引用数据类型通过typeof判断 除了function以外，其余都是object，具体类型是无法判断出来的。

### 2.2 instanceof
        可以准确判断复杂引用数据类型，不能判断基础数据类型

### 3.3 Object.prototype.toString.call()
        toString()是Object的原型方法，统一返回格式为'[object Xxx]'的字符串 

        function getType(obj){
            let type  = typeof obj;
            if (type !== "object") {    // 先进行typeof判断，如果是基础数据类型，直接返回
                return type;
            }
            // 对于typeof返回结果是object的，再进行如下的判断，正则返回结果
            return Object.prototype.toString.call(obj).replace(/^\[object (\S+)\]$/, '$1');  // 注意正则中间有个空格
        }
        /* 代码验证，需要注意大小写，哪些是typeof判断，哪些是toString判断？思考下 */
        getType([])     // "Array" typeof []是object，因此toString返回
        getType('123')  // "string" typeof 直接返回
        getType(window) // "Window" toString返回
        getType(null)   // "Null"首字母大写，typeof null是object，需toString来判断
        getType(undefined)   // "undefined" typeof 直接返回
        getType()            // "undefined" typeof 直接返回
        getType(function(){}) // "function" typeof能判断，因此首字母小写
        getType(/123/g)      //"RegExp" toString返回

## 3.数据类型转换
### 3.1 强制类型转换
        Number() 强制转换规则
            如果是布尔值，true和false分别转换为0和1
            如果是数字，返回自身
            如果是null，返回是0
            如果瘦undefined，返回是NaN
            如果是字符串遵循以下原则：
                只包含数字，转换为十进制
                字符串中包含有效的浮点格式，则转换问浮点数
                空字符串，转换为0
                如果不是以上格式，均返回NaN
            如果是Symbol，抛出错误。
            如果是对象，遵循以下原则：
                部署了 [Symbol.toPrimitive] ，那么调用此方法，
                否则调用对象的 valueOf() 方法，然后依据前面的规则转换返回的值；
                如果转换的结果是 NaN ，则调用对象的 toString() 方法，再次依照前面的顺序转换返回对应的值
        Boolean()
            除了undefined、null、false、''、0（包括+0和-0）、NaN转换出来的是false，其他都是true。

        parseInt() parseFloat() toString() String()

### 3.2 隐式类型转换
        凡是通过逻辑运算符（&&、||、!）、运算符（+、-、*、/）、关系操作符（>、<、<=、>=）、相等运算符、
        或者if、while条件的操作，如果遇到两个数据类型不一样的情况都会发生隐式类型转换

        '=='的隐式类型转换规则
            
    

