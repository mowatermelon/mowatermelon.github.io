---
title: 样式之csshacker
category: 样式表
tags:
  - csshacker
  - 样式表
date: 2017-04-21 00:00:00
---
# 1 谷歌中默认蓝色边框

`按钮`和`input`在`谷歌`中会有一个默认蓝色边框,由于我用的是`bootstrap`，所以我这边直接就`btn`的总样式改了，还有加了`input`的选中样式修改。

<!-- more -->

```css
input,.btn{
  outline:0 none;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline:0 none;
}
input:hover,
input:focus,
input:active{
  outline:0 none;
}
```

# 2 自动填充的背景色

`自动填充`的`文本框`默认有个`黄色背景`，由于`chrome`浏览器默认的给自动填充的文本框添加了背景样式属性

```css

/*谷歌默认样式*/
input:-webkit-autofill, textarea:-webkit-autofill, select:-webkit-autofill {
    background-color: rgb(250, 255, 189);
    background-image: none;
    color: rgb(0, 0, 0);
}
/*修改版本一 没有用*/
input:-webkit-autofill, textarea:-webkit-autofill, select:-webkit-autofill {
    background-color: transparent !important;
    background-image: none;
    color: var(--c);/*用了一个css变量*/
}
/*最终建议修改样式*/
input:-webkit-autofill {
  -webkit-box-shadow: 0 0 0px 1000px white inset;
}
```

# 3 文本自动换行

> 做网页的时候，我们很经常碰到文本的显示，通常来说，文本太长就会很难看，可以用CSS控制文本自动换行。

- 方法一：你定死盒子的宽度，即给盒子一个宽度值（是数值，不是百分比）

- 方法二：强制不换行

```css
div{
    white-space：normal;
    /*默认不换行;*/
    white-space:nowrap;
    /*nowrap强制在同一行内显示所有文本，*/
    /*直到文本结束或者遭遇 <br/> 对象*/
}
```

- 方法三：自动换行

```css
div{
    word-wrap: break-word;
    /*normal 亚洲语言和非亚洲语言的文本规则，*/
    /*允许在字内换行*/
    word-break: normal;
 }
```

- 方法四：强制英文单词断行

```css
div{
    word-break:break-all;
    /*word-break可以设置强行换行;*/
}
```

# 4 table-cell设置宽度无效

> 简洁版

`table`中有多行的情况下，其中某行的中`tr`中`td`在人工设置宽度的前提下，宽度之和超过了其他`tr`的宽度，这个时候，设置的宽度会无效，解决办法是设置`table`的`table-layout`为`fixed`。

```css
table {
    table-layout: fixed;/*防止表格撑破*/
    word-wrap:break-word;/*防止单词断裂*/
}
td{
    word-break: break-all;/*强制英文单词断行*/
    word-wrap:break-word;/*防止单词断裂*/
}
```

> 啰嗦版

前期有个功能需求，需要`table`中`tbody`滚动的时候，`thead`不动，所以我在请求到后台数据之后，将`thead`中的内容放到一个`table`中，设置默认不滚动，设置每个th的`display`为`table-cell`，将`tbody`中的内容放到一个`table`中，放上页面结构。

```html
<div class="bootstrap-table">
    <div class="fixed-table-container">
        <div class="fixed-table-header">
            <table class="table table-hover">
            <thead>
            <tr>
                <th data-field="hc_date" tabindex="0"">
                    <div class="th-inner">
                        标题1
                    </div>
                </th>

                <th data-field="hc_date_00" tabindex="0"">
                    <div class="th-inner">
                        标题2
                    </div>
                </th>
                <th data-field="hc_date_01" tabindex="0"">
                    <div class="th-inner">
                        标题3
                    </div>
                </th>
            </tr>
            </thead>
            </table>
        </div>
        <div class="fixed-table-body">
            <table id="table" data-toggle="table" class="table table-hover">
            <tbody id="danger_body" class="text-center">
            <tr data-index="1">
                <td data-field="hc_date" class="text-info">
                    内容内容内容内容内容内容内容内容内容
                </td>
                <td class="pointer" data-field="hc_date_00">
                    内容内容内容内容内容内容内容内容内容
                </td>
                <td class="pointer" data-field="hc_date_01">
                    内容内容内容内容内容内容内容内容内容
                </td>
            </tr>
            </tbody>
            </table>
        </div>
    </div>
</div>
```

由于`fixed-table-header`和`fixed-table-body`中的`table`是相对独立的，所以我写了一个方法让两个`table`的每个`td`尽量保证一样的宽度，方法很烂，就是遍历`fixed-table-body table tr(0)`中从第一列到倒数第二列`td`的宽度，对应绑到`fixed-table-header table tr`的`th`中去。

```javascript
var o_header = $(".fixed-table-header table tr th"); //获取header部分的th
var o_contanier = $(".fixed-table-body table tr"); //获取body一列tr
var o_body = $(".fixed-table-body table tr").eq(0).children("td"); //获取body部分的第一排的所有td
var temp_w = 0;
for (var i = 0; i < o_header.length - 1; i++) {
    temp_w = o_body.eq(i).outerWidth();
    temp_c_w = o_body.eq(i).width();
    o_header.eq(i).attr("width", temp_w + "px").children("div").css("width",temp_c_w+"px");
}
```

前期项目加载的字段列比较少，没有出什么问题，但是有个地方部署项目之后，而且用的是比较小尺寸的笔记本，在字典中给这个`table`设置了很多列，而且每列对应的内容还比较多，`fixed-table-body table`中出现了横向滚动条，所以布局一下乱套了，我突然发现我给`fixed-table-header table tr`的`th`设置宽度没有用了，因为这个时候，我给所有`th`设置的宽度总和超过了一个`tr`的宽度，`fixed-table-header table`就不干了，说这不行，认为是出了异常，所以就忽略了我的宽度，很尴尬，我由于平时对`table`不怎么在意，所包含的属性值不太熟，所以一下有点懵。

后来发现了这个`css`属性`table-layout`，这个是`table`的一个属性，有三个可选值`inherit|auto|fixed`。

|属性值|含义|
|:---|:----|
|inherit|继承父级设置|
|auto(自动算法)|布局将基于各单元格的内容。表格在每一单元格读取计算之后才会显示出来，速度很慢，就是让`table`自己判断，超出一行`tr`长度之后，就不管单个`td`宽度设置，不满足实际需求。|
|fixed(固定布局的算法)|在这算法中，水平布局是仅仅基于表格的宽度，表格边框的宽度，单元格间距，列的宽度，而和表格内容无关。也就是说，内容可能被裁切，设置为`fixed`会保证每一个`td`的宽度加起来不会超过一行`tr`的宽度。|
