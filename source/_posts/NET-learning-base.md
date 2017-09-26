---
title: .NET学习之基础学习
category: NET
tags:
  - .NET
  - BASE
date: 2017-09-24 00:00:00
---
# 一 ASP.NET产生背景

虽然可以使用`JavaScript`、`Dom`在浏览器端完成很多工作，但是功能还是有限，所以基于`.NET`的`ASP.NET`产生了，是一种`动态网页`技术，在服务器端运行`.NET`代码，动态生成`HTML`,然后响应给`浏览器`。

<!--more-->

# 二 ASP.NET工作逻辑

从使用的角度看，`ASP.NET`的运行过程包含`页面请求`、`分析`、`编译`、`组装`、`页面缓冲`五大环节。当客户端通过`浏览器请求`（Request）页面时，服务器端首先由`页面分析器`（Parser）对被请求的页面进行分析；再将通过分析的页面内容传递给`编译器`（Compiler）；经过`编译器`编译的页面内容被传输给`组装缓存`（Assembly Cache），同时，一些需要较高资源代价的元素可以创建一次后存人`内存`（Memory）；将`组装缓存`和`内存`中的内容`有机结合`后形成一个`完整页面`（包括`数据`、`编译代码`、`HTML代码`等），`完整页面`最后被送往`输出缓存`（`Output Cache`）。`输出缓存`中的内容将作为客户端的页面请求结果被送回`浏览器`。当同一页面被第二次请求时，服务器端将跳过`所有`中间环节，直接从`输出缓存`中送出`页面请求结果`。

# 三 ASP.NET文件解析

## 3.1 概况

- ASP.NET的页面文件是`*.aspx`，每个页面对应一个`*.resx`资源文件和一个`*.aspx.cs`的代码文件。
- `*.resx`是资源文件。每个页面都有一个资源文件相对应。
- `global.asax`是`global.asa`的`.net`版
- `global.asax.cs`是`global.asax`的后台文件。
- `*.ascx`是一个用户自定义控件。
- `*.ascx.cs`是自定义控件的代码文件，`C#`的是`*.ascx.cs`
- `*.ascx.resx`是自定义控件的资源文件。
- `*.aspx.cs`是*.aspx页面的后台代码。
- `web.config`是整个`Web Application`的配置文件。
- `*.csproj`是`CS.NET`的工程文件。
- `*.vsdisco`是Web Service的文件。
- `*.csproj.webinfo`是`CS.NET`工程文件的`Web Application`文件。
- `*.sln`是`VS.NET`的解决方案文件。

其中`global.asax`,`global.asax.cs`,`web.config`,`*.csproj`,`*.vsdisco`,`*.csproj.webinfo`,`*.sln`都是在建立一个`Web Application`工程的时候自动产生的。

## 3.2 详细介绍

> 其中被加粗显示的文件类型，是我现在有所了解的，捂脸羞愧.jpg。

| 文件类型  |  位置  |  说明  |
|:----|:----|:----|
| .asax  |  应用程序根目录。  |  通常是 `Global.asax` 文件，该文件包含从 `HttpApplication 类`派生并表示该应用程序的代码。 有关更多信息，请参见 `Global.asax` 语法。  |
| .ascx  |  应用程序根目录或子目录。  |  Web 用户`控件文件`，该文件定义`自定义`、`可重复`使用的`用户控件`。 有关更多信息，请参见 `ASP.NET` 用户控件。  |
| __`.ashx`__  |  应用程序根目录或子目录。  |  一般处理程序文件，该文件包含实现 `IHttpHandler` 接口以处理所有传入请求的代码。 有关更多信息，请参见 HTTP 处理程序介绍。  |
| .asmx  |  应用程序根目录或子目录。  |  `XML Web services` 文件，该文件包含通过 `SOAP` 方式可用于其他 `Web 应用程序`的类和方法。 有关更多信息，请参见 `XML Web 服务`的发布和部署。  |
| __`.aspx`__  |  应用程序根目录或子目录。  |  ASP.NET `Web 窗体文件`，该文件可包含 `Web 控件`和`其他业务逻辑`。 有关更多信息，请参见 ASP.NET 网页和 ASP.NET `Web 服务器控件`。  |
| .axd  |  应用程序根目录。  |  跟踪查看器文件，通常是 `Trace.axd`。 有关更多信息，请参见 ASP.NET `跟踪`。  |
| .browser  |  App_Browsers 子目录。  |  浏览器定义文件，用于标识客户端浏览器的启用功能。 有关更多信息，请参见 ASP.NET `Web 服务器控件`和`浏览器功能。`  |
| __`.cd`__  |  应用程序根目录或子目录。  |  类关系图文件。 有关更多信息，请参见使用`类关系图`，对于每个`.cs`后台脚本，都可以通过右键查看`类图`，显示脚本的相关内容，比如`继承的类型`、`字段`、`嵌套类型`和`方法`等  |
| .compile  |  Bin 子目录。  |  `预编译`的 `stub`（存根）文件，该文件指向相应的程序集。可执行文件类型（.aspx、ascx、.master、主题文件）已经过`预编译`并放在 `Bin` 子目录下。 有关更多信息，请参见 ASP.NET 网站`预编译`概述。  |
| __`.config`__  |  应用程序根目录或子目录。  |  通常是 `Web.config` 配置文件，该文件包含其设置配置各种 ASP.NET `功能`的 `XML 元素`。 有关更多信息，请参见 ASP.NET 配置文件。  |
| __`.cs`__、.jsl、.vb  |  App_Code 子目录；但如果是 ASP.NET 页的`代码隐藏文件`，则与网页位于同一目录。  |  运行时要编译的类源代码文件。类可以是 `HTTP 模块`、`HTTP 处理程序`，或者是 ASP.NET 页 HTTP 处理程序介绍的`代码隐藏文件`。  |
| .csproj、.vbproj、vjsproj  |  Visual Studio 项目目录。  |  Visual Studio 客户端应用程序项目的`项目文件`。 有关更多信息，请参见项目和解决方案。  |
| .disco、.vsdisco  |  App_WebReferences 子目录。  |  `XML Web services` 发现文件，用于`帮助定位`可用的 `Web services`。 有关更多信息，请参见 `XML Web` 服务的`发布`和`部署`。  |
| .dsdgm、.dsprototype  |  应用程序根目录或子目录。  |  分布式服务关系图 (DSD) 文件，该文件可以添加到任何提供或使用 `Web services`的`Visual Studio`解决方案，以便对`Web service`交互的结构视图进行`反向工程`处理。 有关更多信息，请参见 `XML Web` 服务的`发布`和`部署`。  |
| __`.dll`__  |  Bin 子目录。  |  已编译的`类库文件`。或者，可以将类的`源代码`放在 App_Code 子目录下。 有关更多信息，请参见 ASP.NET 网站中的`共享代码`文件夹。  |
| .licx、.webinfo  |  应用程序根目录或子目录。  |  `许可证文件`。控件创作者可以通过`授权方法`来检查用户是否得到`使用控件`的`授权`，从而帮助保护自己的知识产权。 有关更多信息，请参见如何：`License 组件`和`控件`。  |
| __`.master`__  |  应用程序根目录或子目录。  |  母版页，它定义`应用程序`中引用母版页的其他网页的布局。 有关更多信息，请参见 ASP.NET 母版页。  |
| __`.mdb`__、.ldb |  App_Data 子目录。  |  Access 数据库文件。 有关更多信息，请参见通过 ASP.NET `访问数据`。  |
| .mdf  |  App_Data 子目录。  |  SQL 数据库文件。 有关更多信息，请参见通过 ASP.NET `访问数据`。  |
| .msgx、.svc  |  应用程序根目录或子目录。  |  Indigo Messaging Framework (MFx) service 文件。  |
| .rem  |  应用程序根目录或子目录。  |  远程处理程序文件。 有关更多信息，请参见使用 `SOAP 扩展`修改 SOAP 消息。  |
| .resources  |  `App_GlobalResources` 或 `App_LocalResources` 子目录。  |  资源文件，该文件包含指向`图像`、`可本地化文本`或`其他数据`的资源字符串。有关更多信息，请参见应用程序中的资源或如何：为 ASP.NET 网站创建`资源文件。`  |
| .resx  |  `App_GlobalResources` 或 `App_LocalResources` 子目录。  |  资源文件，该文件包含指向`图像`、`可本地化文本`或`其他数据`的资源字符串。有关更多信息，请参见应用程序中的资源或如何：为 ASP.NET 网站创建`资源文件。`  |
| .sdm、.sdmDocument  |  应用程序根目录或子目录。  |  `系统定义模型` (SDM) 文件。 有关更多信息，请参见系统定义模型 (SDM) 概述。  |
| .sitemap  |  应用程序根目录。  |  站点地图文件，该文件包含网站的结构。ASP.NET 中附带了一个默认的`站点地图`提供程序，它使用`站点地图`文件可以很方便地在网页上显示`导航控件`。 有关更多信息，请参见 ASP.NET 站点导航。  |
| .skin  |  App_Themes 子目录。  |  用于确定显示格式的外观文件。 有关更多信息，请参见 ASP.NET `主题`和`外观`。  |
| __`.sln`__  |  Visual Web Developer 项目目录。  |  Visual Web Developer 项目的解决方案文件。 有关更多信息，请参见项目和解决方案。  |
| .soap  |  应用程序根目录或子目录。  |  SOAP 扩展文件。有关更多信息，请参见使用 SOAP 扩展修改 SOAP 消息。  |

## 3.3 SOAP小课堂

### 3.3.1 WHAT

[参考网站](http://stevenjohn.iteye.com/blog/1442776)

简单对象访问协议是交换数据的一种`协议规范`，是一种轻量的、简单的、基于`XML`（标准通用标记语言下的一个子集）的协议，它被设计成在WEB上交换`结构化`的和`固化`的信息。

- 基于类对象的传输协议。
- SOAP封装（envelop），它定义了一个框架，描述消息中的内容是什么，是谁发送的，谁应当接受并处理它以及如何处理它们；
- SOAP编码规则（encoding rules），它定义了一种序列化机制，用于表示应用程序需要使用的数据类型的实例；
- SOAP RPC表示（RPC representation），它定了一个协定，用于表示远程过程调用和应答；
- SOAP绑定（binding），它定义了SOAP使用哪种协议交换信息。使用HTTP/TCP/UDP协议都可以。

把`SOAP`绑定到`HTTP`提供了同时利用`SOAP`的样式和分散的灵活性的特点以及`HTTP`的丰富的特征库的优点。在`HTTP`上传送`SOAP`并不是说`SOAP`会覆盖现有的`HTTP`语义，而是`HTTP`上的`SOAP`语义会自然的映射到`HTTP`语义。在使用`HTTP`作为`协议绑定`的场合中，`RPC`请求映射到`HTTP请求`上，而`RPC应答`映射到`HTTP应答`。然而，在`RPC`上使用`SOAP`并不仅限于`HTTP协议`绑定。

`SOAP`、`WSDL`(WebServicesDescriptionLanguage)、`UDDI`(UniversalDescriptionDiscovery andIntegration)之一， `SOAP`用来描述传递信息的`格式`， `WSDL` 用来描述如何`访问`具体的接口， `uddi`用来管理，分发，查询`webService` 。

`SOAP` 可以和现存的许多因特网协议和格式`结合使用`，包括`超文本传输协议`（HTTP），`简单邮件传输协议`（SMTP），`多用途网际邮件扩充协议`（MIME）。它还支持从消息系统到`远程过程调用`（RPC）等大量的应用程序。`SOAP`使用基于`XML`的`数据结构`和`超文本传输协议`(HTTP)的组合定义了一个标准的方法来使用`Internet`上各种不同操作环境中的`分布式对象`。

### 3.3.2 HOW

```xml

<?xml version="1.0"?>
<soap:Envelope
xmlns:soap="http://www.w3.org/2001/12/soap-envelope"
soap:encodingStyle="http://www.w3.org/2001/12/soap-encoding">

<soap:Header>
...
</soap:Header>

<soap:Body>
...
  <soap:Fault>
  ...
  </soap:Fault>
</soap:Body>

</soap:Envelope>
```
