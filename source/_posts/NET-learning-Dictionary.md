---
title: .NET学习之Dictionary学习
category: NET
tags:
  - .NET
  - Dictionary
  - OrderBy
  - OrderByDescending
date: 2017-10-22 00:00:00
---
# 1 前言

现在项目中用到数据字典配置，使用者可以直接配置字典设置页面上想要展示的内容，但是现在有个问题是，我们为了字典配置能够通用，所以`ITEMVAL`和`ITEMNAME`都是`NVARCHAR2(256)`，可是有个字典中，用户将`ITEMVAL`统一设置成了`int`数据，举个栗子，1、2、3等等，希望我们按照这个`ITEMVAL`升序显示在页面上，但是我在数据库中通过`ORDER BY ITEMVAL`，发现排出的顺序不是我想要的，正常来说应该是从值为个位数排到两位数，结果实际情况获取到的结果值是`1,10,11,12,13,2,3,4,5.....`，所以需要对取出来的值通过`Dictionary`的`OrderBy`方法进行排序，然后我顺带学习了一下这个用法，为了避免信息问题，我隐藏了数据连接的一些关键词。

<!-- more -->

# 2 解决代码

## 2.1 方法体代码

```c#
using System;
using System.Collections.Generic;
using System.Text;

//注意一定要引用这个包，要不然会说Dictionary没有OrderBy这个方法
using System.Linq;

/// <summary>
/// 获取字典名为DICNAME，ITEMVAL为具体数值的，将从数据库取出来的值，进行升序或降序排列，再进行返回
/// </summary>
/// <param name="sDICNAME"></param>
/// <param name="node"></param>
/// <param name="type">ASC|DESC</param>
/// <returns>Dictionary<int, string></returns>
public Dictionary<int, string> GetOrderDICITEM(string sDICNAME, XConnNode node,string type)
{
    Dictionary<int, string> dicReslut = new Dictionary<int, string>();
    Dictionary<int, string> dicAsc = new Dictionary<int, string>();
    string sSql = string.Format("SELECT A.ITEMVAL,A.ITEMNAME FROM XXXXX A WHERE A.DICNAME ='{0}'", sDICNAME);
    string strDBType = node.DBType["XXXX"];
    string strProviderName = node.ProviderName["XXXX"];
    string strConnString = node.ConnString["XXXX"];
    sSql = SqlHelper.ConvertSql(strDBType, sSql);
    try
    {
        using (DbDataReader dr = DbHelper.ExecuteReader(strProviderName, strConnString, CommandType.Text, sSql.ToString()))
        {
            if (dr.HasRows)
            {
                while (dr.Read())
                {
                    //先获取iITEMVAL的值
                    string sITEMVAL = dr["ITEMVAL"] == DBNull.Value ? string.Empty : dr["ITEMVAL"].ToString();
                    //然后将取出来的iITEMVAL进行格式强制转化
                    int iITEMVAL = Convert.ToInt32(sITEMVAL);
                    //再获取ITEMNAME的值
                    string sITEMNAME = dr["ITEMNAME"] == DBNull.Value ? string.Empty : dr["ITEMNAME"].ToString();
                    //然后通过设置sITEMNAME为iITEMVAL下标赋值的方式，将对应的值存储到Dictionary中去
                    dicReslut[iITEMVAL] = sITEMNAME;
                }
            }
        }
        if(type.Equals("ASC")){
          //对于取出来的值进行升序，举个栗子，从1到10
          dicAsc = dicReslut.OrderBy(o => o.Key).ToDictionary(o => o.Key, p => p.Value);
        }else if(type.Equals("DESC")){
          //对于取出来的值进行降序，举个栗子，从10到1
          dicAsc = dicReslut.OrderByDescending(o => o.Key).ToDictionary(o => o.Key, p => p.Value);
        }
        else{
          //默认是进行升序展示，举个栗子，从1到10
          dicAsc = dicReslut.OrderBy(o => o.Key).ToDictionary(o => o.Key, p => p.Value);
        }


    }
    catch (Exception ex)
    {
        ILog log = new ErrorLog();
        log.WriteLog(ex, "GetDICITEM()", string.Format("获取XXX字典失败查询错误,查询显示流程SQL语句:{0}", sSql));
    }
    return dicAsc;
}
```

## 2.2 后台调用代码

因为我是在一般处理文件(`*.ashx.cs`)中写的，然后在页面后台处理文件(`*.aspx.cs`)中，调用这个方法。

```c#
//1-------------------------首先看一般处理文件(`*.ashx.cs`)的（class）
//就是那个距离命名空间（namespace）最近的那个（class）名字

//举个栗子，这个一般处理事件的（class）名就是（DEMO）
namespace XX.XXX.XXXX
{
    /// <summary>
    /// DEMO 的摘要说明
    /// </summary>
    public class DEMO {

    }
}

//2-------------------------然后在页面后台处理文件(`*.aspx.cs`)中，先new一个一般处理事件的实例，然后就可以愉快的调用了

//就以上文一般处理事件的（class）名为（DEMO）的举个栗子
public void insertXXXX() {
    //先获取方法需要的参数，
    string strDICNAME = "测试用例";//获取字典的名字
    XConnNode node = XConnNode.CreateNode();//获取连接节点

    //实例化一般处理事件对象，请注意一定要是上文方法体中对应的class名字
    DEMO aDEMO = new DEMO();
    Dictionary<int, string> dicCSYL = aDEMO.GetDICITEM(strDICNAME, node);

    string strVar = String.Empty;

    if (dicCSYL.Count > 0)
    {
        //请注意这个时候item的类一定要是KeyValuePair，其中尖角对中的数据类型一定要和一般处理事件方法体中`Dictionary`的尖角对中的数据类型保持一致
        foreach (KeyValuePair<int, string> item in dicCSYL)
        {
            strVar += "HELLO " + item.Value + ",YOU ARE THE" + item.Key + "\n";
        }
        this.divXXX.InnerHtml = strVar;
    }
}
//然后页面上就可以愉快的显示相关信息啦，啦啦啦啦啦。
```

# 3 思考探索

## 3.1 原始数据

```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace XX.XXX.XXXX
{
    /// <summary>
    /// DEMO 的摘要说明
    /// </summary>
    public class DEMO {
      /// <summary>
      /// 添加用户询问内容
      /// </summary>
      /// <returns></returns>
      public Dictionary<int, DEMOClass> getDEMO()
      {
        DEMOClass demo1 = new DEMOClass();
        demo1.NAME = "HELLO1";
        demo1.AGE = 20;
        demo1.WAGES = 20000;
        demo1.EXPER = 1.5;

        DEMOClass demo2 = new DEMOClass();
        demo2.NAME = "HELLO2";
        demo2.AGE = 30;
        demo2.WAGES = 30000;
        demo2.EXPER = 5.5;

        DEMOClass demo3 = new DEMOClass();
        demo3.NAME = "HELLO3";
        demo3.AGE = 40;
        demo3.WAGES = 40000;
        demo3.EXPER = 10.5;

        DEMOClass demo4 = new DEMOClass();
        demo4.NAME = "HELLO4";
        demo4.AGE = 50;
        demo4.WAGES = 50000;
        demo4.EXPER = 15.5;

        Dictionary<int, DEMOClass> dicDEMO = new Dictionary<int, DEMOClass>();
        //先保证插入的数据是乱序的
        dicDEMO.Add(3, demo1);
        dicDEMO.Add(1, demo2);
        dicDEMO.Add(2, demo3);
        dicDEMO.Add(4, demo4);

        return dicDEMO;
      }

      public class DEMOClass
      {
          /// <summary>
          /// 姓名
          /// </summary>
          public string NAME { get; set; }
          /// <summary>
          /// 年龄
          /// </summary>
          public int AGE { get; set; }
          /// <summary>
          /// 薪水
          /// </summary>
          public string WAGES  { get; set; }
          /// <summary>
          /// 工作经验
          /// </summary>
          public double EXPER { get; set; }
      }

    }
}

```

## 3.2 通过自定义字段进行排序

> 关键语句

排序可以通过默认`Dictionary`初始化的序号`o => o.Key`进行排序，但是，还可以通过自定义属性`o => o.Value.AGE`进行排序

```c#
/// <summary>
/// 通过自定义的字段进行排序
/// </summary>
/// <param name="type">ASC|DESC</param>
public Dictionary<int, DEMOClass> GetCostomerData(string type) {
    //先获取方法测试的数据
    Dictionary<int, DEMOClass> dicCSYL = getDEMO();
    Dictionary<int, DEMOClass> dicOrder = new Dictionary<int, DEMOClass>();
    if(type.Equals("ASC")){
      //对于取出来的值进行升序，举个栗子，从1到10
      dicOrder = dicCSYL.OrderBy(o => o.Value.AGE).ToDictionary(p=>p.Key,o=>o.Value);
    }else if(type.Equals("DESC")){
      //对于取出来的值进行降序，举个栗子，从10到1
      dicOrder = ddicCSYL.OrderByDescending(o => o.Value.AGE).ToDictionary(p=>p.Key,o=>o.Value);
    }
    else{
      //默认是进行升序展示，举个栗子，从1到10
      dicOrder = dicCSYL.OrderBy(o => o.Value.AGE).ToDictionary(p=>p.Key,o=>o.Value);
    }
    retrun dicOrder;
}

```

## 3.2 通过多条件进行排序

> 关键语句

排序可以通过默认`Dictionary`可以通过自定义属性`o => o.Value.AGE`进行排序之后，还可以通过`o => o.Value.EXPER`进行再次排序。

```c#
/// <summary>
/// 通过两个字段进行综合排序
/// </summary>
/// <param name="ftype">第一个字段的排序规则 ASC|DESC</param>
/// <param name="stype">第二个字段的排序规则 ASC|DESC</param>
public Dictionary<int, DEMOClass> GetMultipleOrderData(string ftype,string stype) {
    //先获取方法测试的数据
    Dictionary<int, DEMOClass> dicCSYL = getDEMO();
    Dictionary<int, DEMOClass> dicOrder = new Dictionary<int, DEMOClass>();
    if(ftype.Equals("ASC")){
      if(stype.Equals("ASC")){
        //先通过年龄进行升序，然后通过工作经验降序
        dicOrder = dicCSYL.OrderBy(o => o.Value.AGE).ThenBy(o => o.Value.EXPER).ToDictionary(p=>p.Key,o=>o.Value);
      }else if(stype.Equals("DESC")){
        //先通过年龄进行升序，然后通过工作经验升序
        dicOrder = dicCSYL.OrderBy(o => o.Value.AGE).ThenByDescending(o => o.Value.EXPER).ToDictionary(p=>p.Key,o=>o.Value);
      }else{
        //如果第二个类型填写错误  默认先通过年龄进行升序，然后通过工作经验升序
        dicOrder = dicCSYL.OrderBy(o => o.Value.AGE).ThenBy(o => o.Value.EXPER).ToDictionary(p=>p.Key,o=>o.Value);
      }
    }else if(ftype.Equals("DESC")){
      if(stype.Equals("ASC")){
        //先通过年龄进行降序，然后通过工作经验升序
        dicOrder = dicCSYL.OrderByDescending(o => o.Value.AGE).ThenBy(o => o.Value.EXPER).ToDictionary(p=>p.Key,o=>o.Value);
      }else if(stype.Equals("DESC")){
       //先通过年龄进行降序，然后通过工作经验降序
        dicOrder = dicCSYL.OrderByDescending(o => o.Value.AGE).ThenByDescending(o => o.Value.EXPER).ToDictionary(p=>p.Key,o=>o.Value);
      }else{
        //如果第二个类型填写错误  默认先通过年龄进行降序，然后通过工作经验升序
        dicOrder = dicCSYL.OrderByDescending(o => o.Value.AGE).ThenBy(o => o.Value.EXPER).ToDictionary(p=>p.Key,o=>o.Value);
      }
    }else{
      //如果两个类型都填写错误
      //默认   先通过年龄进行升序，然后通过工作经验升序
      dicOrder = dicCSYL.OrderBy(o => o.Value.AGE).ThenBy(o => o.Value.EXPER).ToDictionary(p=>p.Key,o=>o.Value);
    }
    retrun dicOrder;
}

```

# 4 总结

如果在数据库数据中通过`SQL`语句中多层`ORDER BY xx DESC, xxx DESC,....`得出的结果值是正确的，那么最好是在`SQL`中就写好，避免取出数据之后再排序，这样逻辑很累赘。

但是如果通过多层`ORDER BY xx DESC, xxx DESC,....`得出的结果值不是正确的，就像我上文中，数据库中某个字段是`NVARCHAR2()`、`VARCHAR2()`和`TEXT()`等等字符串数据类型，只能在取出来数据之后再转成`int`或者`double`等数据类型再进行排序操作，那么`Dictionary`这排序方法就很实用。

```c#
//举个栗子
dicXXX.OrderBy(o => o.Value.X).ThenBy(o => o.Value.XX).ThenByDescending(o => o.Value.XXX).ThenBy(o => o.Value.XXXX)......ToDictionary(p=>p.Key,o=>o.Value);
```

虽然这个排序方法可以无限循环下去，但是从实际情况下，感觉这个在只有一两个排序条件的时候效率比较高，但是在有多个排序条件的时候，这个效率就感觉一般了。