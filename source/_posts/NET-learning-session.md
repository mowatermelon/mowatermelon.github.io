---
title: .NET学习之一般处理文件中使用SESSION
category: NET
tags:
  - .NET
  - CS
  - SESSION
date: 2017-09-25 00:00:00
---

# 一 什么是一般处理文件

## 1.1 WHAT

虽然通过标准的方式可以创建处理程序，但是实现的步骤比较复杂，为了方便网站开发中对处理程序的应用，从`ASP.NET 2.0`开始，`ASP.NET`提供了称为`一般处理程序`的`处理程序`，允许我们使用比较简单的方式定义扩展名为`ASHX`的`专用处理程序`是一种较为简单、高效的处理程序，在`非WEB窗体处理`的请求中有着`重要`的作用。

<!--MORE-->

## 1.2 WHY

对于`ASP.NET`网站来说，网站最常规的处理结果就是`HTML`网页，`生成网页`的工作通常使用扩展名为`ASPX`的`WEB窗体`来完成。对于`非WEB窗体处理`的请求，都可以通过`一般处理程序`完成，适合产生供浏览器处理的、不需要回发处理的数据格式，例如生成`RSS`、`FEED`、`XML`、`图片`等动态内容。

`ASHX`通常是实现`IHTTPHANDLER`接口，因为不必继承自`PAGE类`，它免去了普通`.ASPX`页面的`控件解析`以及`页面处理`的过程，所以没有那么多事件需要处理，不必消耗太多资源，所以性能方面要比`ASPX`高。一般来说能够用一般处理文件实现的功能，就在`一般处理文件`中写，但是涉及到`WEB窗体`内容`读取`和`修改`的话，就会放到`ASPX.CS`中进行处理，一般在项目逻辑处理文件夹新建`REMOTEHANDLE`(远程处理文件夹)，然后把`一般处理文件`放在这个文件夹。

# 二 问题产生原因

在`WEBFORM`中`ASPX`脚本中使用`SESSION`，是不用声明直接使用的。

```C#
public void checkDemo()
{
  //声明
  //session['键名']='键值';
  session['demo'] = true;

  //使用
  //以上文的设置的demo为例
  bool isDemo = false;
  if(session['demo']){
    isDemo = true;
  }
  Response.Write(isDemo);
}

```

但是在一般处理程序`ASHX`中需要先引用对应的`命名空间`和继承对应`SESSION`接口，然后在项目中可以通过`CONTEXT.SESSION["XX"]`大法才能正常调用`SESSION`，如果是未引用正确的命名空间，会报错`SESSION对象未定义`，如果是未继承正确的接口，会报错`SESSION对象为空，不可用`。

```c#
using System.Web;
using System.Web.SessionState;
namespace XXX.XXX.RemoteHandle
{
    /// <summary>
    /// XXX 的摘要说明
    /// </summary>
    public class XX : IHttpHandler, IRequiresSessionState
    {
      public void ProcessRequest(HttpContext context)
        {
            context.Response.ContentType = "text/plain";
            string strType = context.Request["action"];

            switch (strType)
            {

                case "sessionDemo":
                    SessionDemo(context);
                    break;
            }
        }

        /// <summary>
        /// 在一般处理文件中使用session功能
        /// </summary>
        /// <param name="context"></param>
        private void SessionDemo(HttpContext context)
        {
          context.Session["DEMO"] = false;
          context.Response.Write(context.Session["DEMO"]);
        }
    }
}
```
