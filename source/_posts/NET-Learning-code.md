---
title:  .NET学习之文字转码
category: NET
tags:
  - .NET
  - 转码
date: 2017-10-19 00:00:00
---

最近项目中需要用到了附件图片查看审批功能，业务申请的时候图片默认是上传到`FTP`的，由于之前没有写过处理`FTP`的文件，我需要将图片的路径绑到插件中去，我原本思路是直接把`FTP`路径放进去，结果发现不行，我以为是路径中中文编码有问题，所以我试了各种编码转换，结果一个后台大哥和我说，处理`FTP`文件都是先在后台启动一个`FTP`服务，将文件在本地有一个备份，再将本地的文件路径返回到页面上去，可怜我犯傻了一天，试了各种编码。

<!--more-->

再次验证了写逻辑代码，一定要清楚功能是在前台处理还是在后台处理，要不然容易出乱子，今天就是，我当时在浏览器中直接可以访问`FTP`协议路径下的文件，没有输入帐号密码之类的，所以我以为是页面局部标签渲染，也是可以直接访问这个路径，结果浪费了一天时间，想想也是，服务器中的文件不用帐号密码就可以直接访问和下载，文件安全性得不到保证。

```c#

  /// <summary>
  /// GB2312转换成UTF8
  /// </summary>
  /// <param name="text"></param>
  /// <returns></returns>
  public static string gb2312_utf8(string text)
  {
    //声明字符集
    System.Text.Encoding utf8, gb2312;
    //gb2312
    gb2312 = System.Text.Encoding.GetEncoding("gb2312");
    //utf8
    utf8 = System.Text.Encoding.GetEncoding("utf-8");
    byte[] gb;
    gb = gb2312.GetBytes(text);
    gb = System.Text.Encoding.Convert(gb2312, utf8, gb);
    //返回转换后的字符
    return utf8.GetString(gb);
  }

  /// <summary>
  /// UTF8转换成GB2312
  /// </summary>
  /// <param name="text"></param>
  /// <returns></returns>
  public static string utf8_gb2312(string text)
  {
    //声明字符集
    System.Text.Encoding utf8, gb2312;
    //utf8
    utf8 = System.Text.Encoding.GetEncoding("utf-8");
    //gb2312
    gb2312 = System.Text.Encoding.GetEncoding("gb2312");
    byte[] utf;
    utf = utf8.GetBytes(text);
    utf = System.Text.Encoding.Convert(utf8, gb2312, utf);
    //返回转换后的字符
    return gb2312.GetString(utf);
  }

  /// <summary>
  /// UTF8转换成gbk
  /// </summary>
  /// <param name="text"></param>
  /// <returns></returns>
  public static string utf8_gbk(string text)
  {
    //声明字符集
    System.Text.Encoding utf8, gbk;
    //utf8
    utf8 = System.Text.Encoding.GetEncoding("utf-8");
    //gb2312
    gbk = System.Text.Encoding.GetEncoding("gbk");
    byte[] utf;
    utf = utf8.GetBytes(text);
    utf = System.Text.Encoding.Convert(utf8, gbk, utf);
    //返回转换后的字符
    return gbk.GetString(utf);
  }


    public static int Asc(string character)
    {
        if (character.Length == 1)
        {
            System.Text.ASCIIEncoding asciiEncoding = new System.Text.ASCIIEncoding();
            int intAsciiCode = (int)asciiEncoding.GetBytes(character)[0];
            return (intAsciiCode);
        }
        else
        {
            throw new Exception("Character is not valid.");
        }
    }

        //显示图片
        private void GetFJImg(HttpContext context)
        {

            if (!string.IsNullOrEmpty(sSQBH) && !string.IsNullOrEmpty(sFJMC))
            {
                //定义FTP请求对象
                FtpWebRequest reqFTP = null;
                //定义FTP响应对象
                FtpWebResponse response = null;
                //FTP数据流
                Stream ftpStream = null;
                MemoryStream outStream = new MemoryStream();
                try
                {
                    if (string.IsNullOrEmpty(sFTPLJ))
                    {
                        Stream stream = new MemoryStream(byteFTPNR);
                        int bufferSize = 2048;
                        byte[] buffer = new byte[bufferSize];
                        int contentLen = stream.Read(buffer, 0, bufferSize);
                        while (contentLen != 0)
                        {
                            outStream.Write(buffer, 0, contentLen);
                            contentLen = stream.Read(buffer, 0, bufferSize);
                        }
                        stream.Close();


                    }
                    else
                    {
                        //FTP模式
                        string filePath = string.Empty;
                        string URL = ConfigurationManager.AppSettings["FtpAddr"];
                        string username = ConfigurationManager.AppSettings["FtpUser"];
                        string password = ConfigurationManager.AppSettings["FtpPwd"];
                        filePath = "ftp://" + URL + "/" + sSQBH + "/" + sFJMC;
                        reqFTP = (FtpWebRequest)FtpWebRequest.Create(new Uri(filePath));
                        reqFTP.Method = WebRequestMethods.Ftp.DownloadFile;
                        reqFTP.UseBinary = true;
                        reqFTP.Credentials = new NetworkCredential(username, password);
                        response = (FtpWebResponse)reqFTP.GetResponse();
                        ftpStream = response.GetResponseStream();
                        int bufferSize = 2048;
                        byte[] buffer = new byte[bufferSize];
                        int contentLen = ftpStream.Read(buffer, 0, bufferSize);
                        while (contentLen != 0)
                        {
                            outStream.Write(buffer, 0, contentLen);
                            contentLen = ftpStream.Read(buffer, 0, bufferSize);
                        }
                        ftpStream.Close();

                    }
                    context.Response.ContentType = "image/GIF";
                    context.Response.Cache.SetCacheability(HttpCacheability.Public);
                    context.Response.BufferOutput = false;
                    context.Response.BinaryWrite(outStream.ToArray());
                    context.Response.Flush();
                }
                catch (Exception ex)
                {
                    ILog log = new ErrorLog(this.GetType());
                    log.WriteLog(ex, "GetFJImg获取图片信息出错!", ex.Message);
                }
                finally
                {
                    if (response != null)
                    {
                        response.Close();
                    }
                    if (ftpStream != null)
                    {
                        ftpStream.Close();
                    }
                }
            }
        }
```