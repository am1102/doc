> 无论人数多少，代码都应该同出一门。

#JavaScript

## 编码风格 JSHint
1. 在编辑器中，开启 JSHint
2. 在项目根目录建立 [.jshintrc 文件](../config/.jshintrc)

### 相关阅读
[jshint](http://jshint.com/)


##Indentation,分号,单行长度
* 一律使用2个空格
* continuation-indentation 同样适用2个空格，跟上一行对齐
>>>>>>> origin/master
* Statement 之后一律以分号结束， 不可以省略
* 单行长度，理论上不要超过80列，不过如果编辑器开启 soft wrap 的话可以不考虑单行长度
* 接上一条，如果需要换行，存在操作符的情况，一定在操作符后换行，然后换的行缩进2个空格
这里要注意，如果是多次换行的话就没有必要继续缩进了，比如说右边第二段这种就是最佳格式。

**Example**
```
if (typeof qqfind === "undefined" ||
  typeof qqfind.cdnrejected === "undefined" ||
  qqfind.cdnrejected !== true) {
  url = "http://pub.idqqimg.com/qqfind/js/location4.js";
} else {
  url = "http://find.qq.com/js/location4.js";
}
```

##空行
* 变量声明后（当变量声明在代码块的最后一行时，则无需空行）
* 代码块后，逻辑块之间加空行增加可读性（在函数调用、数组、对象中则无需空行）
* 单行或多行注释前加
* 文件最后保留一个空行

##换行
换行的地方，行末必须有','或者运算符；

以下几种情况不需要换行：

* 下列关键字后：else, catch, finally
* 代码块'{'前
以下几种情况需要换行：

* 代码块'{'后和'}'前
* 变量赋值后


##变量命名
* 标准变量采用驼峰标识 如: `ceseCamel`
* 使用的ID的地方一定全大写，如：`userID`
* 使用的URL的地方一定全大写, 比如说 reportURL
* 涉及Android的，一律大写第一个字母
* 涉及iOS的，一律小写第一个，大写后两个字母
* 常量采用大写字母，下划线连接的方式，如：`NAMES_LIKE_THIS`
* 构造函数，大写第一个字母
* 类名驼峰，并且首字母要大写 CamelName
* jquery对象必须以'$'开头命名

```
var thisIsMyName;

var goodID;

var AndroidVersion;

var iOSVersion;

var MAX_COUNT = 10;

function Person(name) {
  this.name = name
}
```
##引号
最外层统一使用单引号。

```
// not good
var x = "test";

// good
var y = 'foo',
    z = '<div id="test"></div>';
```

##undefined使用场景
* 永远不要直接使用undefined进行变量判断
* 使用字符串 "undefined" 对变量进行判断


```
// Bad
var person;
console.log(person === undefined);    //true

// Good
console.log(typeof person);    // "undefined"
```

##对象声明

```
// Bad
var team = new Team();
team.title = "AlloyTeam";
team.count = 25;

// Good  semi colon 采用 符号后面接空格 的形式
var team = {
  title: 'AlloyTeam',
  count: 25
};
```

## 数组声明

```
Array Literals
// Bad
var colors = new Array("red", "green", "blue");
var numbers = new Array(1, 2, 3, 4);


// Good
var colors = [ "red", "green", "blue" ];
var numbers = [ 1, 2, 3, 4 ];
```

##括号对齐
* 标准示例 括号前后有空格， 花括号起始 不另换行，结尾新起一行
* 花括号必须要， 即使内容只有一行， 决不允许右边第二种情况
* 涉及 if for while do...while try...catch...finally 的地方都必须使用花括号

##if else else前后留有空格
```
if (condition) {
  doSomething();
} else {
  doSomethingElse();
}
```

##switch
* 采用右边的格式， switch和括号之间有空格， case需要缩进， break之后跟下一个case中间留一个blank line
* 花括号必须要， 即使内容只有一行
```
switch (condition) {
    case "first":
        // code
        break;

    case "third":
        // code
        break;

    default:
    // code
}
```

##for
* 普通for循环, 分号后留有一个空格， 判断条件等内的操作符两边不留空格， 前置条件如果有多个，逗号后留一个空格
* for-in 一定要有 hasOwnProperty 的判断， 否则 JSLint 或者 JSHint 都会有一个 warn

```
var values = [ 1, 2, 3, 4, 5, 6, 7 ],
    i, len;

for (i=0, len=values.length; i<len; i++) {
    process(values[i]);
}



var prop;

for (prop in object) {

    // 注意这里一定要有 hasOwnProperty 的判断， 否则 JSLint 或者 JSHint 都会有一个 warn ！
    if (object.hasOwnProperty(prop)) {
        console.log("Property name is " + prop);
        console.log("Property value is " + object[prop]);
    }
}
```

##变量声明
所有函数内变量声明放在函数内头部，只使用一个 var(多了JSLint报错)，
 一个变量一行， 在行末跟注释， 注释啊，注释啊，亲

```
function doSomethingWithItems(items) {

    var value = 10,    // 注释啊，注释啊，亲
        result = value + 10,    // 注释啊，注释啊
        i,    // 注释啊，注释啊，亲
        len;    // 注释啊，注释啊，亲

    for (i=0, len=items.length; i < len; i++) {
        doSomething(items[i]);
    }
}
```

###函数声明
* 一定先声明再使用， 不要利用 JavaScript engine的hoist特性, 违反了这个规则 JSLint 和 JSHint都会报 warn
* function declaration 和 function expression 的不同，function expression 的（）前后必须有空格，而function declaration 在有函数名的时候不需要空格， 没有函数名的时候需要空格。
* 函数调用括号前后不需要空格
* 立即执行函数的写法, 最外层必须包一层括号
* "use strict" 决不允许全局使用， 必须放在函数的第一行， 可以用自执行函数包含大的代码段, 如果 "use strict" 在函数外使用， JSLint 和 JSHint 均会报错

```
function doSomething(item) {
    // do something
}

var doSomething = function (item) {
    // do something
}


// Good
doSomething(item);

// Bad: Looks like a block statement
doSomething (item);


// Good
var value = (function() {

    // function body
    return {
        message: "Hi"
    }
}());


// Good
(function() {
    "use strict";

    function doSomething() {
        // code
    }

    function doSomethingElse() {
        // code
    }

})();
```

##数组、对象
* 对象属性名不需要加引号；
* 对象以缩进的形式书写，不要写在一行；
* 数组、对象最后不要有逗号。

##null
适用场景：

* 初始化一个将来可能被赋值为对象的变量
* 与已经初始化的变量做比较
* 作为一个参数为对象的函数的调用传参
* 作为一个返回对象的函数的返回值
不适用场景：

* **不要用null来判断函数调用时有无传参**
* 不要与未初始化的变量做比较


## 其他
* 尽量减少全局变量的使用.
* 语句总是以分号结尾.
* 不要在块内声明函数.
* 标准特性优于非标准特性(如果类库有提供, 优先使用类库中的函数).
* 不要封装基本类型.
* 只在解析序列化串时使用 eval() .
* 禁止使用 with .
* 减少使用 continue 和 break .
* 仅在函数内使用 this .
* 使用 Array/Object 直接量, 避免使用 Array/Object 构造器.
* 禁止修改内置对象的原型.
