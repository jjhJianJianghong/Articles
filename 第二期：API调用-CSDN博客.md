---
created: 2025-12-08T12:54:50 (UTC +08:00)
tags: [第二期：API调用]
source: https://blog.csdn.net/2501_93097309/article/details/155111672?spm=1011.2124.3001.6209
author: 2501_93097309
---

# 第二期：API调用-CSDN博客

> ## Excerpt
> 摘要：本文介绍了前端调用API的常见HTTP请求方法（GET、POST、PUT、PATCH、DELETE）及其实现方式。通过Node.js+Express示例展示了前后端交互过程：GET获取资源、POST创建资源、PUT替换资源、PATCH更新部分资源、DELETE删除资源。同时指出跨域问题(CORS)的解决方案，建议后端使用cors中间件允许跨域请求。文章提供了完整的代码示例，涵盖了从请求发送到响应处理的全流程。

---
## 前端调用API

常见方法是通过[HTTP请求](https://so.csdn.net/so/search?q=HTTP%E8%AF%B7%E6%B1%82&spm=1001.2101.3001.7020)。前端通过发送请求到后端API接口，来获取资源或者进行某些操作。常见请求方式由GET、POST、PUT、PATCH、DELETE等。

## 后端实现API

后端是处理前端请求的地方，它通常通过API接受前端请求并返回资源或执行操作。常见的后端技术有Node.js(Express)，Python(Flak,Django），Java(Sping），Ruby(Rails）等。

### 1.GET请求-查询资源

例：前端使用fetch向后端获取ID=123用户的个人信息。假设端API路径是/users/:id

#### 前端（获取用户信息，以fetch为例）

```cobol
const userId = 123;fetch(`https://api.example.com/users/${userId}`)  .then(response => {if (!response.ok) {      throw new Error('Network response was not ok');    }return response.json();  // 解析为 JSON  })  .then(data => {    console.log('User data:', data); // 输出用户数据  })  .catch(error => {    console.error('Error:', error);  // 错误处理  });
```

#### 后端（处理请求，返回信息，以Node.js+Express为例)

```cobol
const express = require('express');const app = express();const port = 3000;const users = [  { id: 123, name: 'John Doe', age: 30 },  { id: 124, name: 'Jane Doe', age: 28 }];// GET 请求，获取指定 ID 的用户信息app.get('/users/:id', (req, res) => {  const userId = parseInt(req.params.id);  // 获取 URL 中的 ID 参数  const user = users.find(u => u.id === userId);if (user) {    res.json(user);  // 返回用户数据  } else {    res.status(404).json({ message: 'User not found' });  // 用户未找到  }});app.listen(port, () => {  console.log(`Server is running on http://localhost:${port}`);});
```

交互过程：

前端通过fetch发送GET请求，请求https://api.example.com/users/123来获取ID为123的用户资源。

后端通过Express接受到请求，查找ID为123的用户，如果找到就返回用户的JSON资源，没有找到就返回404。

### 2.POST请求-创建资源

POST请求是创建资源，即向服务器提交资源。前端发送POST请求到后端，后端会创建新的资源并返回。

#### 前端（创建新用户，以fetch为例）

```cobol
const newUser = { name: 'John Smith', age: 31 };fetch('https://api.example.com/users', {method: 'POST',  headers: {'Content-Type': 'application/json',  },  body: JSON.stringify(newUser)  // 请求体包含新用户数据})  .then(response => response.json())  // 解析返回的 JSON 数据  .then(data => {    console.log('New user created:', data); // 输出创建的用户数据  })  .catch(error => {    console.error('Error:', error); // 错误处理  });
```

#### 后端（Node.js + Express）

```cobol
app.post('/users', (req, res) => {  const newUser = req.body;  // 获取请求体中的用户数据  newUser.id = users.length + 1;  // 简单的 ID 生成方式  users.push(newUser);  res.status(201).json(newUser);  // 返回新创建的用户});
```

### 3.PUT请求-更新全部资源(替换资源）

PUT请求用于更新资源。通常替换整个资源。前端发送完整的资源数据，后端系将器替换并返回更新后的数据。

#### 前端（更新ID=123的用户信息）

```cobol
const userId = 123;const updatedUserData = { name: 'John Smith', age: 32 };fetch(`https://api.example.com/users/${userId}`, {method: 'PUT',  headers: {'Content-Type': 'application/json',  },  body: JSON.stringify(updatedUserData)  // 请求体包含更新的用户数据})  .then(response => response.json())  // 解析返回的 JSON 数据  .then(data => {    console.log('User updated:', data); // 输出更新后的用户数据  })  .catch(error => {    console.error('Error:', error); // 错误处理  });
```

#### 后端（Node.js+Express)

```cobol
app.put('/users/:id', (req, res) => {  const userId = parseInt(req.params.id);  // 获取 URL 中的 ID 参数  const updatedUser = req.body;            // 获取请求体中的更新数据  const userIndex = users.findIndex(u => u.id === userId);if (userIndex !== -1) {// 完全替换用户数据    users[userIndex] = { id: userId, ...updatedUser };    res.json(users[userIndex]);  // 返回更新后的用户数据  } else {    res.status(404).json({ message: 'User not found' });  // 用户未找到  }});
```

### 4.PATCH请求-更新部分资源

PATCH请求用于更新部分资源。常用于更新资源中的一段数。

#### 前端（更新ID=123用户的年龄）

```cobol
const userId = 123;const updatedAge = { age: 33 };fetch(`https://api.example.com/users/${userId}`, {method: 'PATCH',  headers: {'Content-Type': 'application/json',  },  body: JSON.stringify(updatedAge)  // 请求体只包含要更新的字段})  .then(response => response.json())  // 解析返回的 JSON 数据  .then(data => {    console.log('User patched:', data); // 输出部分更新后的用户数据  })  .catch(error => {    console.error('Error:', error); // 错误处理  });
```

#### 后端（Node.js+Express)

```cobol
app.patch('/users/:id', (req, res) => {  const userId = parseInt(req.params.id);  // 获取 URL 中的 ID 参数  const updatedFields = req.body;          // 获取请求体中的部分更新字段  const userIndex = users.findIndex(u => u.id === userId);if (userIndex !== -1) {// 只更新用户的部分字段    users[userIndex] = { ...users[userIndex], ...updatedFields };    res.json(users[userIndex]);  // 返回部分更新后的用户数据  } else {    res.status(404).json({ message: 'User not found' });  // 用户未找到  }});
```

### 5.DELETE请求-删除资源

DELETE请求用以删除指定的资源。前端发送DELETE请求，后端删除对应的资源并返回相应的状态。

#### 前端（删除ID=123的用户）

```cobol
const userId = 123;fetch(`https://api.example.com/users/${userId}`, {method: 'DELETE',})  .then(response => {if (response.ok) {      console.log('User deleted successfully');    } else {      throw new Error('Failed to delete user');    }  })  .catch(error => {    console.error('Error:', error);  // 错误处理  });
```

#### 后端（Node.js+Express)

```cobol
app.delete('/users/:id', (req, res) => {  const userId = parseInt(req.params.id);  // 获取 URL 中的 ID 参数  const userIndex = users.findIndex(u => u.id === userId);if (userIndex !== -1) {// 删除用户数据    users.splice(userIndex, 1);    res.status(204).end();  // 返回 204 无内容，表示删除成功  } else {    res.status(404).json({ message: 'User not found' });  // 用户未找到  }});
```

## 跨域问题（CORS）

跨域，即前后端分离时，浏览器会限制前端网页与不同源的服务器进行交互。前后端分开部署，后端需要设置跨域资源共享策略（Cross-Origin Resource Sharing），允许前端请求资源。

例如：

```php
const cors = require('cors'); app.use(cors()); 
```
