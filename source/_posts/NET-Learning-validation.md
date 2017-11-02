---
title:  .NET学习之validate安全管理学习
category: NET
tags:
  - .NET
  - validate
date: 2017-10-12 00:00:00
---

今天测试和我说项目中的富文本编辑器上传图片不成功，我查了一下，是在上传图片信息的时候，违反了c#的安全信息验证，所以我在web.config中添加了以下内容，去掉了这个验证，不知道对项目中的其他的验证会不会有影响。

  <!-- more -->

```c#
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.0" />
    <!--为了保证富文本编辑器图片上传成功，需要去掉网站在这块的危险认证-->
    <httpRuntime  maxQueryStringLength="1024000" requestValidationMode="2.0" />
    <pages validateRequest="false" />
  </system.web>
</configuration>
```