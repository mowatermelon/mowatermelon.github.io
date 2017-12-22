---
title: 西瓜有话说之js对象学习regexp对象篇
category: js_thinking
tags:
  - regexp
  - object
  - watermelon
  - js_thinking
date: 2017-10-30 00:00:00
---
# 1 修饰词

- `i` 忽略大小写
- `g` 全局匹配
- `m` 把`\n`识别为多行

<!--more-->

# 2 元字符

- `\` 将下一个字符标记为一个特殊字符、或一个原义字符、或一个向后引用、或一个八进制转义符。例如，“n"匹配字符"n"。"\n"匹配一个换行符。串行"\\"匹配"\"而"\("则匹配"("
- `[abc]` 中括号的任意一个字符，有点像更大范围的逻辑或。
- `[^abc]` 除了中括号中的任意一个字符
- `(abc)` 必须完全包含`abc`，这三个字符，有点像更大范围的逻辑与。
- `|` 逻辑或，x|y	匹配x或y。例如，“z|food"能匹配"z"或"food"。"(z|f)ood"则匹配"zood"或"food"。
- `.`  匹配除“\n"之外的任何单个字符。要匹配包括"\n"在内的任何字符，请使用像"(.|\n)"的模式。
- `\w` 任意一个字母、数字或下划线
- `\W` 任意一个非字母、数字和下划线
- `\d` 任意一个数字
- `\D` 任意一个非数字
- `\s` 任意一个空格
- `\S` 任意一个非空格
- `\b` 单词边界
- `\B` 非单词边界
- `\n` 代表换行符
- `\t` tab缩进

```javascript
//举个栗子

//linux或php单词
//可实现向后引用$1(replace替换时)
var str1 ="linux";
var str2 ="dddd（sdfsdfs）dddd<sdfsdfs></sdfsdfs>）";

var pattern1 = /(linux)|(php)/;
console.log(str1.match(pattern1));//["linux", "linux", undefined, index: 0, input: "linux"]
console.log(str2.match(pattern1));//null

```

# 3 量词

- `+` 1个或多个
- `*` 任意多个
- `?` 1个或0个
- `{3}` 3个
- `{3,5}` 3个到5个
- `{3,}`  3个以上
- `^` 行首，匹配输入字符串的开始位置，如果设置了RegExp对象的Multiline属性，^也匹配“\n"或"\r"之后的位置。
- `$` 行尾，匹配输入字符串的结束位置，如果设置了RegExp对象的Multiline属性，$也匹配“\n"或"\r"之前的位置。
- `?=a` 后面紧挨a的
- `?!a` 后面不紧挨a的
- `(?=pattern)` 正向肯定预查，在任何匹配`pattern`的字符串开始处匹配查找字符串。这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。预查不消耗字符，也就是说，在一个匹配发生后，在最后一次匹配之后立即开始下一次匹配的搜索，而不是从包含预查的字符之后开始。
- `(?!pattern)` 正向否定预查，在任何不匹配`pattern`的字符串开始处匹配查找字符串。这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。预查不消耗字符，也就是说，在一个匹配发生后，在最后一次匹配之后立即开始下一次匹配的搜索，而不是从包含预查的字符之后开始
- `(?<=pattern)` 反向肯定预查，与正向肯定预查类拟，只是方向相反。
- `(?<!pattern)` 反向否定预查，与正向否定预查类拟，只是方向相反。

```javascript
//举个栗子

//linux或php单词
//可实现向后引用$1(replace替换时)
var str3 ="Windows2000";
var str4 = "Windows3.1";
var str5 ="2000Windows";
var str6 = "3.1Windows";

//以下都是  获取匹配  的 案例，也就是说，该匹配需要获取供以后使用-------------案例一
var pattern1 = /Windows(95|98|NT|2000)/;
console.log(str3.match(pattern1));//["Windows2000", "2000", index: 0, input: "Windows2000"]
console.log(str4.match(pattern1));//null
console.log(str5.match(pattern1));//null
console.log(str6.match(pattern1));//null

//以下都是  非获取匹配  的 案例，也就是说，该匹配不需要获取供以后使用-------------案例二
var pattern2 = /Windows(?=95|98|NT|2000)/;
console.log(str3.match(pattern2));//["Windows", index: 0, input: "Windows2000"]
console.log(str4.match(pattern2));//null
console.log(str5.match(pattern2));//null
console.log(str6.match(pattern2));//null

var pattern3 = /Windows(?!95|98|NT|2000)/;
console.log(str3.match(pattern3));//null
console.log(str4.match(pattern3));//["Windows", index: 0, input: "Windows3.1"]
console.log(str5.match(pattern3));//["Windows", index: 4, input: "2000Windows"]
console.log(str6.match(pattern3));//["Windows", index: 3, input: "3.1Windows"]

var pattern4 = /Windows(?<=95|98|NT|2000)/;
console.log(str3.match(pattern4));//null
console.log(str4.match(pattern4));//null
console.log(str5.match(pattern4));//null
console.log(str6.match(pattern4));//null

var pattern5 = /Windows(?<!95|98|NT|2000)/;
console.log(str3.match(pattern5));//["Windows", index: 0, input: "Windows2000"]
console.log(str4.match(pattern5));//["Windows", index: 0, input: "Windows3.1"]
console.log(str5.match(pattern5));//["Windows", index: 4, input: "2000Windows"]
console.log(str6.match(pattern5));//["Windows", index: 3, input: "3.1Windows"]

var pattern6 = /(?<=95|98|NT|2000)Windows/;
console.log(str3.match(pattern6));//null
console.log(str4.match(pattern6));//null
console.log(str5.match(pattern6));//["Windows", index: 4, input: "2000Windows"]
console.log(str6.match(pattern6));//null

var pattern7 = /(?<!95|98|NT|2000)Windows/;
console.log(str3.match(pattern7));//["Windows", index: 0, input: "Windows2000"]
console.log(str4.match(pattern7));//["Windows", index: 0, input: "Windows3.1"]
console.log(str5.match(pattern7));//null
console.log(str6.match(pattern7));//["Windows", index: 3, input: "3.1Windows"]
```

> 小提示：获取匹配和非获取匹配的区别

`获取匹配`的意思是，如果`字符串`匹配到`正则`规范，则会返回`正则`中的`所有内容`，如上面案例中的`案例一`。
`非获取匹配`的意思是，如果`字符串`匹配到`正则`规范，则会返回`正则`中的`非括号内的内容`，如上面案例中的`案例二`。

# 4 相关方法

js中使用正则的字符对象的方法

- search(regexp);
- match(regexp);
- replace(regexp,str);
- split(regexp);

# 5 正则实例

## 5.1 匹配139开头的电话号码

```javascript
var phone1='13998675896';
var phone2='13498675896';
var phone3='1399867a896';
var phone4='1399867589';

var pattern=/^139\d{8}$/i;

console.log(phone1.match(pattern));//["13998675896", index: 0, input: "13998675896"]
console.log(phone2.match(pattern));//null   因为开头不是139，所以返回null
console.log(phone3.match(pattern));//null  因为139之后的八位数中包含了字母，不是纯数字，所以返回null
console.log(phone4.match(pattern));//null  因为139之后的只有七个数字，所以返回null

```

## 5.2 匹配邮箱格式

```javascript
// \w 任意一个字母、数字或下划线
// + 1个或多个
var mail1='skdd@qq.com';
var mail2='skdd@163.com';
var mail3='skdd@gmail.com';
var mail4='skddqq.com';
var mail5='skdd@qq.22.com';
var mail6='-skdd@qq.22.com';

var pattern=/^\w+@\w+\.\w+$/i;

console.log(mail1.match(pattern));//[ 'skdd@qq.com', index: 0, input: 'skdd@qq.com' ]
console.log(mail2.match(pattern));//[ 'skdd@163.com', index: 0, input: 'skdd@163.com' ]
console.log(mail3.match(pattern));//[ 'skdd@gmail.com', index: 0, input: 'skdd@gmail.com' ]
console.log(mail4.match(pattern));//null   因为没有@符号，所以返回null
console.log(mail5.match(pattern));//null    因为@后面是qq.22.com分了三段，所以返回null

```

## 5.3 替换日期格式

将以`\`分割的日期转化成以`-`分割的日期格式

```javascript
var date1='2017/11/21';
var date2='2017/11/21 13:11:15';
var date3='2017/11/21 13/11/15';
var date4='2017/11/21 13/11';
var date5='2017-11-21';
var date6='2017#11#21';

var pattern=/(\d+)\/(\d+)\/(\d+)/g;
//$1-$2-$3是向后引用

console.log(date1.replace(pattern,'$1-$2-$3'));//2017-11-21
console.log(date2.replace(pattern,'$1-$2-$3'));//2017-11-21 13:11:15
console.log(date3.replace(pattern,'$1-$2-$3'));//2017-11-21 13-11-15
console.log(date4.replace(pattern,'$1-$2-$3'));//2017-11-21 13/11
console.log(date5.replace(pattern,'$1-$2-$3'));//2017-11-21
console.log(date6.replace(pattern,'$1-$2-$3'));//2017#11#21

```

## 5.4 检测一百以内数

检测0到100两位小数的正则不包含0包含100（包含三位小数）

```javascript
var num1 ="11";
var num2 ="11.123";
var num3 ="11.1547";
var num4 ="99.5";
var num5 ="100";
var num6 ="100.0000";
var num7 ="100.01";

var pattern=/^([1-9]\d{0,1}(\.\d{0,3})?|100)$/;

console.log(num1.match(pattern));//["11", "11", undefined, index: 0, input: "11"]
console.log(num2.match(pattern));//["11.123", "11.123", ".123", index: 0, input: "11.123"]
console.log(num3.match(pattern));//null
console.log(num4.match(pattern));//["99.5", "99.5", ".5", index: 0, input: "99.5"]
console.log(num5.match(pattern));//["100", "100", undefined, index: 0, input: "100"]
console.log(num6.match(pattern));//null
console.log(num7.match(pattern));//null
```

## 5.5 返回字符串中括号内文字

```javascript
var str1 ="dddd（sdfsdfs）";
var str2 = "dddd（sdfsdfs）dddd（sdfsdfs）dddd（sdfsdfs）";
var str3 ="dddd（sdfsdfs）dddd（sdfsdfs）dd dd（sdfsdfs）dd dd（sdfsdfs）ddsdd（sdfsdfs）dddd（sdfs dfs）ddd d（sd fsdfs）";
var str4 ="dddd（sdfsdfs）dddd<sdfsdfs></sdfsdfs>dd dd（<sdfsdfs></sdfsdfs>）dd dd（sdfsdfs）ddsdd（sdfsdfs）dddd（sdfs dfs）ddd d（sd fsdfs）";
var str5 ="dddd（sdfsdfs）dddd<sdfsdfs></sdfsdfs>dd dd（sdfsdfs）dd dd（sdfsdfs）ddsdd（sdfsdfs）dddd（sdfs dfs）ddd d（sd fsdfs）";
var pattern = /(?=.*\w)+\（+(\w+)\）+/g;

console.log(str1.replace(pattern,'<$1>'));//dddd<sdfsdfs>
console.log(str2.replace(pattern,'<$1>'));//dddd<sdfsdfs>dddd<sdfsdfs>dddd<sdfsdfs>
console.log(str3.replace(pattern,'<$1>'));//dddd<sdfsdfs>dddd<sdfsdfs>dd dd<sdfsdfs>dd dd<sdfsdfs>ddsdd<sdfsdfs>dddd（sdfs dfs）ddd d（sd fsdfs）
console.log(str4.replace(pattern,'<$1>'));//dddd<sdfsdfs>dddd<sdfsdfs></sdfsdfs>dd dd（<sdfsdfs></sdfsdfs>）dd dd<sdfsdfs>ddsdd<sdfsdfs>dddd（sdfs dfs）ddd d（sd fsdfs）
console.log(str5.replace(pattern,'<$1>'));//dddd<sdfsdfs>dddd<sdfsdfs></sdfsdfs>dd dd<sdfsdfs>dd dd<sdfsdfs>ddsdd<sdfsdfs>dddd（sdfs dfs）ddd d（sd fsdfs）

console.log(str1.replace(/\s/g,'').replace(pattern,'<$1>'));//dddd<sdfsdfs>
console.log(str2.replace(/\s/g,'').replace(pattern,'<$1>'));//dddd<sdfsdfs>dddd<sdfsdfs>dddd<sdfsdfs>
console.log(str3.replace(/\s/g,'').replace(pattern,'<$1>'));//ddddd<sdfsdfs>dddd<sdfsdfs>dddd<sdfsdfs>dddd<sdfsdfs>ddsdd<sdfsdfs>dddd<sdfsdfs>dddd<sdfsdfs>
console.log(str4.replace(/\s/g,'').replace(pattern,'<$1>'));//dddd<sdfsdfs>dddd<sdfsdfs></sdfsdfs>dddd（<sdfsdfs></sdfsdfs>）dddd<sdfsdfs>ddsdd<sdfsdfs>dddd<sdfsdfs>dddd<sdfsdfs>
console.log(str5.replace(/\s/g,'').replace(pattern,'<$1>'));//dddd<sdfsdfs>dddd<sdfsdfs></sdfsdfs>dddd<sdfsdfs>dddd<sdfsdfs>ddsdd<sdfsdfs>dddd<sdfsdfs>dddd<sdfsdfs>

```

## 5.6 检测上传文件名

需要检测上传文件路径中，是否都是同一文件名不同格式的多个文件

```javascript
function checkUnique(filePath){
    var isRight =false;
    //给数组去重
    Array.prototype.unique = function () {
        this.sort(); //先排序
        var res = [this[0]];
        for (var i = 1; i < this.length; i++) {
            if (this[i] !== res[res.length - 1]) {
                res.push(this[i]);
            }
        }
        return res;
    }
    var patt=/\.+[\w]{3}/g; //检测后缀名的正则
    var ml = filePath.replace(patt,'');//去掉文件路径中的后缀名
    ml = ml.split("，").unique();
    if(ml.length==1){
        isRight =true;
    }
    // console.log("checkUnique");
    // console.log(isRight);
    return isRight;
}

var filePath1 ="polygon.cpg，polygon.dbf，polygon.prj，polygon.shp，polygon.shx";
var filePath2 ="polygon.cpg，line.dbf，eee.prj";
console.log(checkUnique(filePath1));//true
console.log(checkUnique(filePath2));//false

```

## 5.7 检测上传文件格式

需要检测上传文件路径中，是否包含了所有要求上传的文件格式

```javascript
function checkContainer(filePath){
    var isRight =true;
    var checkType = ["dbf", "shp", "shx"];
    var patt=/[\w]+\./g;
    var ml = filePath.replace(patt,'');
    ml = ml.toLowerCase().split("，");
    var rightArray = [];
    for(var i = 0 ; i <ml.length ; i++){
      var pattern = RegExp(ml[i]);
      if(pattern.test(checkType)&& ml[i]!==undefined&&!pattern.test(rightArray)){
        rightArray.push(ml[i]);
      }
    }
    if(rightArray.length!=checkType.length){
        isRight = false;
    }
    // console.log("checkContainer");
    // console.log(isRight);
    return isRight;
}

var filePath1 ="polygon.cpg，polygon.dbf，polygon.prj，polygon.shp，polygon.shx";
var filePath2 ="polygon.cpg，line.dbf，eee.prj";
var filePath3 ="polygon.shp，line.dbf，eee.shx";
console.log(checkContainer(filePath1));//true
console.log(checkContainer(filePath2));//false
console.log(checkContainer(filePath3));//true

```

# 6 完整速查表

|字符|描述|
|:--|:--|
|\|将下一个字符标记为一个特殊字符、或一个原义字符、或一个向后引用、或一个八进制转义符。例如，`n`匹配字符`n`。`\n`匹配一个换行符。串行`\\`匹配`\`而`\(`则匹配`(`。|
|^|匹配输入字符串的开始位置。如果设置了`RegExp`对象的`Multiline`属性，`^`也匹配`\n`或`\r`之后的位置。|
|$|匹配输入字符串的结束位置。如果设置了`RegExp`对象的`Multiline`属性，`$`也匹配`\n`或`\r`之前的位置。|
|*|匹配前面的子表达式零次或多次。例如，`zo*`能匹配`z`以及`zoo`。`*`等价于`{0,}`。|
|+|匹配前面的子表达式一次或多次。例如，`zo+`能匹配`zo`以及"`zoo`"，但不能匹配`z`。`+`等价于`{1,}`。|
|?|匹配前面的子表达式零次或一次。例如，`do(es)?`可以匹配`does`或`does`中的`do`。`?`等价于`{0,1}`。|
|{n}|`n`是一个非负整数。匹配确定的`n`次。例如，`o{2}`不能匹配`Bob`中的`o`，但是能匹配`food`中的两个o。|
|{n,}|`n`是一个非负整数。至少匹配`n`次。例如，`o{2,}`不能匹配`Bob`中的`o`，但能匹配`foooood`中的所有`o`。`o{1,}`等价于`o+`。`o{0,}`则等价于`o*`。|
|{n,m}|`m`和`n`均为非负整数，其中`n<=m`。最少匹配`n`次且最多匹配`m`次。例如，`o{1,3}`将匹配`fooooood`中的前三个`o`。`o{0,1}`等价于`o?`。请注意在逗号和两个数之间不能有空格。|
|?|当该字符紧跟在任何一个其他限制符`（*,+,?，{n}，{n,}，{n,m}）`后面时，匹配模式是`非贪婪`的。`非贪婪模式`尽可能少的匹配所搜索的字符串，而默认的贪婪模式则尽可能多的匹配所搜索的字符串。例如，对于字符串`oooo`，`o+?`将匹配单个`o`，而`o+`将匹配所有`o`。|
|.|匹配除`\n`之外的任何单个字符。|
|(pattern)|匹配`pattern`并获取这一匹配。所获取的匹配可以从产生的`Matches`集合得到，在`VBScript`中使用`SubMatches`集合，在`JScript`中则使用`$0…$9`属性。要匹配圆括号字符，请使用`\(`或`\)`。|
|`(?:pattern)`|匹配`pattern`但不获取匹配结果，也就是说这是一个非获取匹配，不进行存储供以后使用。|
|`(?=pattern)`|正向肯定预查，在任何匹配`pattern`的字符串开始处匹配查找字符串。这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。|
|`(?!pattern)`|正向否定预查，在任何不匹配pattern的字符串开始处匹配查找字符串。这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。|
|`(?<=pattern)`|反向肯定预查，与正向肯定预查类拟，只是方向相反。|
|`(?<!pattern)`|反向否定预查，与正向否定预查类拟，只是方向相反。|
|[xyz]|字符集合。匹配所包含的任意一个字符。例如，`[abc]`可以匹配`plain`中的`a`。|
|[^xyz]|负值字符集合。匹配未包含的任意字符。例如，`[^abc]`可以匹配`plain`中的`p`。|
|[a-z]|字符范围。匹配指定范围内的任意字符。例如，`[a-z]`可以匹配`a`到`z`范围内的任意小写字母字符。|
|[^a-z]|负值字符范围。匹配任何不在指定范围内的任意字符。例如，`[^a-z]`可以匹配任何不在`a`到`z`范围内的任意字符。|
|\b|匹配一个单词边界，也就是指单词和空格间的位置。例如，`er\b`可以匹配`never`中的`er`，但不能匹配`verb`中的`er`。|
|\B|匹配非单词边界。`er\B`能匹配`verb`中的`er`，但不能匹配`never`中的`er`。|
|\cx|匹配由`x`指明的控制字符。例如，`\cM`匹配一个`Control-M`或回车符。`x`的值必须为`A-Z`或`a-z`之一。否则，将`c`视为一个原义的`c`字符。|
|\d|匹配一个数字字符。等价于`[0-9]`。|
|\D|匹配一个非数字字符。等价于`[^0-9]`。|
|\f|匹配一个换页符。等价于`\x0c`和`\cL`。|
|\n|匹配一个换行符。等价于`\x0a`和`\cJ`。|
|\r|匹配一个回车符。等价于`\x0d`和`\cM`。|
|\s|匹配任何空白字符，包括空格、制表符、换页符等等。等价于`[ \f\n\r\t\v]`。|
|\S|匹配任何非空白字符。等价于`[^ \f\n\r\t\v]`。|
|\t|匹配一个制表符。等价于`\x09`和`\cI`。|
|\v|匹配一个垂直制表符。等价于`\x0b`和`\cK`。|
|\w|匹配包括下划线的任何单词字符。等价于`[A-Za-z0-9_]`。|
|\W|匹配任何非单词字符。等价于`[^A-Za-z0-9_]`。|
|\xn|匹配`n`，其中`n`为十六进制转义值。十六进制转义值必须为确定的两个数字长。例如，`\x41`匹配`A`。`\x041`则等价于`\x04&1`。正则表达式中可以使用`ASCII`编码。|
|\num|匹配`num`，其中`num`是一个正整数。对所获取的匹配的引用。例如，`(.)\1`匹配两个连续的相同字符。|
|\n|标识一个八进制转义值或一个向后引用。如果`\n`之前至少`n`个获取的子表达式，则n为向后引用。否则，如果`n`为八进制数字（0-7），则`n`为一个八进制转义值。|
|\nm|标识一个八进制转义值或一个向后引用。如果`\nm`之前至少有`nm`个获得子表达式，则`nm`为向后引用。如果`\nm`之前至少有n个获取，则`n`为一个后跟文字m的向后引用。如果前面的条件都不满足，若`n`和`m`均为八进制数字`（0-7）`，则`\nm`将匹配八进制转义值`nm`。|
|\nml|如果`n`为八进制数字`（0-3）`，且`m`和`l`均为八进制数字`（0-7）`，则匹配八进制转义值`nml`。|
|\un|匹配`n`，其中`n`是一个用四个十六进制数字表示的`Unicode`字符。例如，`\u00A9`匹配版权符号`（©）`。|

# 7 常用正则表达式

- 用户名

`/^[a-z0-9_-]{3,16}$/`

- 密码

`/^[a-z0-9_-]{6,18}$/`

- 十六进制值

`/^#?([a-f0-9]{6}|[a-f0-9]{3})$/`

- 电子邮箱

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

`/^[a-z\d]+(\.[a-z\d]+)*@([\da-z](-[\da-z])?)+(\.{1,2}[a-z]+)+$/`

- URL

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

- IP 地址

`/((2[0-4]\d|25[0-5]|[01]?\d\d?)\.){3}(2[0-4]\d|25[0-5]|[01]?\d\d?)/`

`/^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/`

- HTML 标签

`/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`

- 删除代码\\注释

`/(?<!http:|\S)//.*$/`

- Unicode编码中的汉字范围

`/^[\u2E80-\u9FFF]+$/`