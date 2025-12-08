---
created: 2025-12-08T12:56:16 (UTC +08:00)
tags: [python xx.py -u 目标url]
source: https://blog.csdn.net/2501_93097309/article/details/155423465?spm=1011.2124.3001.6209
author: 2501_93097309
---

# 渗透工具-Sqlmap的使用_python xx.py -u

> ## Excerpt
> SQL注入检测工具sqlmap使用指南：该工具支持GET/POST参数、Cookie、HTTP头等多种注入方式，可检测漏洞并获取数据库信息（库名、表名、列名及数据）。主要参数包括：-u指定URL、-r读取请求文件、--dbs获取数据库、--tables列出表名、--columns显示字段。高级选项支持设置检测等级(--level)、风险等级(--risk)、请求间隔(--delay)和代理(--proxy)。使用时需注意POST型注入需复制请求内容到文件，且高侵略性操作(--dump)需谨慎使用。_python xx.py -u 目标url

---
## **免责声明**

本文基于[Sqli-Labs](https://so.csdn.net/so/search?q=Sqli-Labs&spm=1001.2101.3001.7020)靶场进行技术研究，仅作合法学习与防御技术分享。任何个人或组织利用本文内容实施的非法行为，均由其自行承担法律责任，与笔者无关。

## 基础知识

自动化SQL注入工具，核心功能包括：

1.检测目标URL是否存在SQL注入漏洞（支持GET/POST参数、Cookie、HTTP头注入）

2.获取数据库信息（数据库类型、版本、库名、表名、列名、数据）

3.执行命令（如在目标服务器执行系统命令、上传文件）

4.反弹shell（获取目标服务器的远程控制权限）

**GET型 -u**

**POST型 -r**

**head头 -u "目标URL" --cookie**

##  URL里只有一个参数

```sql
python sqlmap.py -u 目标URL
```

## URL里有两个参数

```sql
python sqlmap.py -u "目标URL"
```

## 检测注入点

Kali Linux

```sql
sqlmap -u "目标URL" --cookie="Cookie值"
```

Windows

```sql
python sqlmap.py -u "目标URL" --cookie="Cookie值"
```

## \-dbs参数

Kali

```sql
python sqlmap.py -u "目标URL" --cookie="Cookie值" --dbs
```

## ![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/0bfeed4b09a64eccbaaceadabbc5f925.png)

可以看到注入类型有布尔盲注，报错注入，时间盲注，联合查询注入。下面是获取到的数据库名。
https://github.com/jjhJianJianghong/Articles/blob/19347edb212ffcb588e9c5d65963516f38a74dce/111.png

## \-D 数据库名 --tables参数

```sql
python sqlmap.py -u "目标URL" --cookie="Cookie值" -D 数据库名 --tables
```

## ![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/01cf4adc3be54a4fb6f617f17bf51eba.png)

结果可以到红色线处的路径去查看。这个操作是获取dvwa数据库中的表名。

![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/b499f555b7be442fa2dbd430d5fa247c.png)

这里已经成功获取到了数据库dvwa中的表名，如图所示。

## \-D 数据库名 -T 表名 --columns

```sql
python sqlmap.py -u "目标URL" --cookie="Cookie值" -D 数据库名 -T 表名 --columns
```
111.png

## ![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/ce4cc8877a9b4f0db1e5afe0ed25f029.png)

## ![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/6bb9caa21a6146c4bf95e01a147e4a26.png)

这是获取数据库dvwa中user表中的字段名，结果如图所示。

## 拖库，实战中慎用！！！--dump，-C指定列名

```sql
python sqlmap.py -u "目标URL" -D 数据库名 -T 表名 -C 列名1，列名2 --dump
```

## ![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/25f791205c3f4b718bde5bab0d2aa2c8.png)

## ![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/8a5ce63fe1b449e5b25203da9a2a9d04.png)

![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/d7d6309050364c58ba8571c41882af24.png)

这是获取列名中的数据，可以直接查看，若是遇到太多，也可以在保存结果的位置打开，查看如上图所示结果。

## \--batch为自动化测试

```sql
python sqlmap.py -u "目标URL" --batch
```

## \-random-agent参数使用随机user-agent头或者自己指定

```sql
python sqlmap.py -u "目标URL" -random-agent//自定义python sqlmap.py -u "目标URL" -user-agent="Mozilla/4.0 (c ompatible; MSIE 6.0; Windows NT 5.0; de) Opera 8.0"
```

## \-r参数指定文件

```sql
python sqlmap.py -r "文件名" //若是与Sqlmap不在同一个目录下，使用绝对路径，先复制文件的路径！
```

![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/a3db2ebe00a641d9bcbffd90c2d11437.png)

## ![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/be7e4f284f58488fba2792dd6fe70dce.png)

文件2.txt（文件名自定义，后缀最好是txt，方便直接读取）里面的内容，直接复制目标URL中POST的Raw部分，右键Copy to file即可。

![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/30e77e324d9e45819c8f2df3f80df479.png)

这是对POST型的进行注入，注意路径问题，结果如上所示。

## head头

## \-u "目标URL" --cookie

```sql
python sqlmap.py -u "目标URL" --cookie "cookie值"
```

## ![](%E6%B8%97%E9%80%8F%E5%B7%A5%E5%85%B7-sqlmap%E7%9A%84%E4%BD%BF%E7%94%A8python/b6d18db3d94b4135bc2a993b73f54f55.png)

## \--technique=XX，注入的技巧，有BE（时间盲注），UE（联合查询注入），temper等

参考：[https://cn-sec.com/archives/4096996.html](https://cn-sec.com/archives/4096996.html "https://cn-sec.com/archives/4096996.html")

## \--level=xx,测试等级

1 仅测试GET和POST

2 增加对HTTP的Cookie检测

3 增加对HTTP User-Agent和Referer的检测（可以用于检测隐藏的注入）

4 增加对HTTP Host的检测

5 最全面，测试所有HTTP头字段

level越高，测试范围越广，发送的请求数量越多，扫描时间越长

## \--risk=xx，风险等级

1 低风险（默认）

2 中风险，增加时间盲注和部分可能修改数据的payload（如UPDATA语句）

3 高风险，使用堆叠查询、文件操作等高侵略性payload，可能导致数据修改或系统命令执行

使用risk=3需要有明确授权

参考：[https://labex.io/zh/tutorials/kali-adjust-scan-aggressiveness-with-level-and-risk-in-sqlmap-594138](https://labex.io/zh/tutorials/kali-adjust-scan-aggressiveness-with-level-and-risk-in-sqlmap-594138 "https://labex.io/zh/tutorials/kali-adjust-scan-aggressiveness-with-level-and-risk-in-sqlmap-594138")

## \--delay=xx，设置请求间隔，避免触发速率限制

## \--timeout=xx，延长超时时间

## \--proxy="http://中转服务器：端口"，通过中转服务器访问
