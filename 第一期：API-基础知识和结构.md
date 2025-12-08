---
created: 2025-12-08T12:53:05 (UTC +08:00)
tags: [第一期：API-基础知识和结构]
source: https://blog.csdn.net/2501_93097309/article/details/155111181?spm=1011.2124.3001.6209
author: 2501_93097309
---

# 第一期：API-基础知识和结构

> ## Excerpt
> 文章浏览阅读862次，点赞34次，收藏20次。本文摘要：API（应用程序编程接口）是不同应用间的通信协议，REST是一种网络应用架构风格。文章介绍了API分类（RESTAPI、非RESTAPI和RESTfulAPI）、RESTAPI相较于SOAP协议的优势，以及完整的API请求响应结构（包含URL、方法、头信息、状态码和响应体）。通过具体示例展示了GET、POST、PUT、PATCH和DELETE等HTTP方法的使用场景，说明了前后端如何通过API进行数据交互。

---
## API相关知识

## **1.****定义**

### **API**

（Application Programming Interface)应用程序编程接口，即不同应用程序之间相互交流的协议。

### **REST**

（Representational State Transfer)，表现层状态转换，是一种用于构建网络应用的架构风格。

#### **核心**

资源、表现形式、状态转换。

资源：可以是文本、视频、图像等

表现形式：可以是JSON、XML、HTML、PNG等

状态转换：通常是根据HTTP的GET、POST、PUT、DELETE等

#### **六大约束条件**

客户端-服务器架构、无状态、可缓存、统一接口、分层系统、按需代码

#### **优点**

扩展性高、轻量化

## **2.****API分类**

REST API 、非REST API、RESTful API（有的分为前两类）

### **REST API**

由请求决定进行哪类CURD（create、update、read、delete）操作，同一个路径可以进行多种操作。通过URI（统一资源标识符）进行表示，通常用标准的HTTP方法（如GET（获取）、POST（创建）、PUT（更新）、DELETE（删除））来对资源进行操作。

### **非REST API**

请求方式不决定CURD操作，一个请求路径只对应一次操作，一般只使用GET、POST。

### **RESTful API**

是更严格的REST API，遵循六大约束条件。

要求每个资源都具有明确的表示形式（通常是JSON或XML），且所有操作都是无状态的。

## **3.****为什么需要REST API？**

1.  Web应用早期阶段是用一种基于XML的SOAP（Simple Object Access Protocol)，即简单对象协议访问，该方法繁琐且不易扩展，所需要的带宽资源多且只允许XML格式的数据传输。(SOAP是一种协议）
2.  而REST API简单且允许使用多种数据格式，缺点是没有SOAP安全。（REST是一种架构）

## **4.****API结构**

## **API结构**

### **API请求结构**

#### **1.请求URL**

-   基本格式

```cobol
https://example.com/api/resource
```

[https://example.com是服务器地址，/api/resource是请求的路径资源](https://example.xn--com,-x29f53r9obxds90mp2b/api/resource%E6%98%AF%E8%AF%B7%E6%B1%82%E7%9A%84%E8%B7%AF%E5%BE%84%E8%B5%84%E6%BA%90 "https://example.com是服务器地址，/api/resource是请求的路径资源")

-   带有查讯参数的URL：查询参数通常用于过滤或者指定某些信息。

例如：

```cobol
https://example.com/api/users?id=123
```

id=123是查询参数，意味着要查询ID=123的用户信息。

#### **2.请求方法**

常见的HTTP请求方法：

GET：从服务器获取数据（查询操作）

POST：向服务器发送数据（创建操作）

PUT：更新服务器上的数据（全部更新操作）

PATCH：更新部分数据（部分更新操作）

DELETE：删除服务器上的数据（删除操作）

例如，获取ID=123的用户信息，用GET方法：

```cobol
GET https://example.com/api/users?id=123
```

#### **3.请求头**

请求头包含了一些额外的信息，用来描述请求性质和服务器如何处理请求。

例如：

```cobol
Authorization: Bearer ACCESS_TOKENContent-Type: application/jsonAccept: application/json
```

Authorization：认证消息，用于身份验证，如Bearer ACCESS\_TOKEN。

Content-Type：请求体的数据格式。如application/json表示请求体数据格式为JSON。

Accept：客户端希望接收的数据格式，通常是application/json或者application/xml。

#### **4.请求体**

请求体包含了要发送到服务器的数据，通常在POST、PUT（通常用于替换资源）、PATCH（更新部分资源）请求中使用。通常为JSON格式。

例如：

```perl
{"name": "Jora","email": "jora@outlook.com"}  
```

这里是向服务器发送了一个JSON对象，包含了用户的名字和邮件地址。

### **API响应结构**

服务器处理完请求后，会返回响应。通常包括：状态码、响应头、响应体。

#### **1.状态码**

状态码是服务器返回的数字代码，表示请求的处理结构。

常见的HTTP状态码类型：

1XX表示通知信息

2XX表示成功

3XX表示重定向

4XX表示客户的差错

5XX表示服务器的差错

常用的状态码如下：

200 OK：请求成功，服务器返回数据

201 Created：请求成功，资源已经创建（通常是POST请求）

400 Bad Request：请求格式错误或者参数错误

401 Unauthorized：用户未授权

403 Forbidden：资源禁止访问，权限不够

404 Not Found：资源不存在，没有找到

500 Internal Server Error：服务器内部错误

#### **2.响应头**

响应头包含了响应的数据，如响应的内容类型、长度等。

Content-Type：服务器返回的数据类型

Content\_Length：响应体的大小（单位：字节）

Set-Cookie：服务器通过这个头来设置cookie，用于会话管理

例如：

```less
Content-Type: application/jsonContent-Length: 156
```

3.响应体

包含了服务器返回的实际数据。通常为JSON或者XML格式。

例如：

```perl
{"id": 123,"name": "Jora","email": "jora@outlook.com"}
```

这是一个成功响应后返回的JSON对象，表示ID为123的用户信息。

```csharp
{"error": "Invalid API Key","message": "The API key provided is invalid or expired."}
```

这个是响应失败，返回了错误信息。

通常为JSON，前端收到数据后可以进行页面渲染，显示数据等操作，后端可以根据前端的请求需求返回不同的数据或者状态码。

### **完整请求与响应例子**

#### **GET请求**

用于查询数据。

##### **请求**

```cobol
GET https://example.com/api/users?id=123Authorization: Bearer ACCESS_TOKENAccept: application/json
```

##### **响应**

```cobol
HTTP/1.1 200 OKContent-Type: application/jsonContent-Length: 112{"id": 123,"name": "Jora","email": "jora@outlook.com"}
```

表示客户端请求ID为123的用户信息，服务器返回了该用户的姓名和邮件地址。

#### **POST请求**

用于创建新数据。

##### **请求**

```cobol
POST https://example.com/api/usersContent-Type: application/jsonAuthorization: Bearer ACCESS_TOKEN{"name": "LiHua","email": "LiHua@outlook.com"}
```

##### **响应**

```cobol
HTTP/1.1 201 CreatedContent-Type: application/jsonContent-Length: 150{"id": 124,"name": "LiHua","email": "LiHua@outlook.com"}
```

表示客户端请求创建一个名为LiHua的新用户，服务器返回了创建成功的响应，并且给出的新用户的ID。

#### **PUT请求**

用于 更新/替换 现有数据的全部内容。

##### **请求**

```cobol
PUT https://api.example.com/users/123Content-Type: application/jsonAuthorization: Bearer YOUR_ACCESS_TOKEN{"name": "Mike","email": "Mike@outlook.com"}
```

##### **响应**

```cobol
HTTP/1.1 200 OKContent-Type: application/jsonContent-Length: 132{"id": 123,"name": "Mike","email": "Mike@outlook.com"}
```

这里表示把ID为123的用户更新为Mike，并且邮件地址也换成了Mike的。

#### **PATCH请求**

用于更新部分数据，比如一个数据里面的某些字段。

##### **请求**

```cobol
PATCH https://api.example.com/users/123Content-Type: application/jsonAuthorization: Bearer ACCESS_TOKEN{"email": "jora.doe@newemail.com"}
```

##### **响应**

```cobol
HTTP/1.1 200 OKContent-Type: application/jsonContent-Length: 126{"id": 123,"name": "Jora","email": "jora.doe@163.com"}
```

这个表示更新了ID为123用户的电子邮件。

#### **DELETE请求**

用于删除指定的数据。通常返回一个空响应或一个确认消息，即表示删除成功。

##### **请求**

```cobol
DELETE https://api.example.com/users/123Authorization: Bearer YOUR_ACCESS_TOKEN
```

##### **响应**

```cobol
HTTP/1.1 204 No Content
```

这里表示删除ID为123的用户，响应状态码**204 No Content**表示数据已成功删除，并且没有返回内容。

### **API请求和响应的关键点**

### **请求**

URL：指定访问的资源

请求方法：指定操作类型，如GET、POST、PUT、DELETE等

请求头：提供附加的请求信息，如认证，数据格式等

请求体：发送到服务器的数据，在POST/PUT请求中使用

### **响应**

状态码：表示请求处理的结构，如200、403、500等

响应头：包含响应的信息，如数据类型，长度等

响应体：服务器返回的数据，通常是JSON或者XML格式

前端：通过Fetch或Axios发送请求到后端API

后端：通过框架（如Express、Flask）定义API接口，处理请求并返回响应。

API响应通常是JSON格式，前后端接收后可以进行渲染或进行后续处理。

 **平台和参考文章**

-   一体化平台 [https://app.apifox.com](https://app.apifox.com/ "https://app.apifox.com")
-   帮助文档 [https://docs.apifox.com/](https://docs.apifox.com/ "https://docs.apifox.com/")
-   基础知识[https://docs.apifox.com/request-url-and-method](https://docs.apifox.com/request-url-and-method "https://docs.apifox.com/request-url-and-method")
-   API与REST API 、RESTful API的相关文章：

[文章1](https://apifox.com/apiskills/restapi-vs-restfulapi/ "文章1")

[文章2](https://cloud.tencent.com/developer/article/1448167 "文章2")

[文章3](https://cloud.tencent.com/developer/article/2520721?policyId=1003 "文章3")

最后，感谢你愿意看到这里，希望你能有收获，祝你生活愉快，工作顺利！
