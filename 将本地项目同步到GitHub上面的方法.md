Jianghong Jian原创 于 2025-10-30 22:18:22 发布 · 公开 

· ![](%E5%B0%86%E6%9C%AC%E5%9C%B0%E9%A1%B9%E7%9B%AE%E5%90%8C%E6%AD%A5%E5%88%B0github%E4%B8%8A%E9%9D%A2%E7%9A%84%E6%96%B9%E6%B3%95/newHeart2023Black.png) 1

· ![](%E5%B0%86%E6%9C%AC%E5%9C%B0%E9%A1%B9%E7%9B%AE%E5%90%8C%E6%AD%A5%E5%88%B0github%E4%B8%8A%E9%9D%A2%E7%9A%84%E6%96%B9%E6%B3%95/tobarCollect2.png) 0 ·

CC 4.0 BY-SA版权

版权声明：本文为博主原创文章，遵循 [CC 4.0 BY-SA](http://creativecommons.org/licenses/by-sa/4.0/) 版权协议，转载请附上原文出处链接和本声明。

## 创建GitHub仓库

Repositories-New

![](%E5%B0%86%E6%9C%AC%E5%9C%B0%E9%A1%B9%E7%9B%AE%E5%90%8C%E6%AD%A5%E5%88%B0github%E4%B8%8A%E9%9D%A2%E7%9A%84%E6%96%B9%E6%B3%95/cc8765fc01a143e8acc00534f30da546.png)

在Repository name输入仓库名（即你的项目名字），然后点击Create repository创建。属性是Public还是Private自主决定。

![](%E5%B0%86%E6%9C%AC%E5%9C%B0%E9%A1%B9%E7%9B%AE%E5%90%8C%E6%AD%A5%E5%88%B0github%E4%B8%8A%E9%9D%A2%E7%9A%84%E6%96%B9%E6%B3%95/2468ee6e8e114625b3f959be68b1381f.png)

## 进入终端

Win+R 输入cmd，进入终端，选择Git终端。（要先在本地安装Git Bash，安装方法自行了解）

![](%E5%B0%86%E6%9C%AC%E5%9C%B0%E9%A1%B9%E7%9B%AE%E5%90%8C%E6%AD%A5%E5%88%B0github%E4%B8%8A%E9%9D%A2%E7%9A%84%E6%96%B9%E6%B3%95/d701a35f86bd4522848361317cf0422b.png)

## 输入命令

### 1.进入你的项目文件夹

```bash
cd "B:\文件名" 
```

注意路径不要写出，最好是全英文路径。

### 2.初始化Git仓库

```csharp
# 2. 初始化 Git 仓库git init
```

### 3.添加远程仓库

```cobol
# 3. 添加远程仓库git remote add origin https://github.com/用户名/文件名.git  #以实际用户名和实际文件名为准
```

### 4.添加所有文件

```csharp
# 4. 添加所有文件git add .
```

这样即可上传本地项目中的所有文件。

### 5.提交文件

```cobol
# 5. 提交文件git commit -m "初始提交"
```

### 6.推送到GitHub

```less
# 6. 推送到 GitHubgit branch -M maingit push -u origin main
```

此时会弹出GitHub登录窗口，输入密码登录即可，然后跳转到项目页面，此时本地项目已经完全同步到GitHub上面。

同步成功！![](%E5%B0%86%E6%9C%AC%E5%9C%B0%E9%A1%B9%E7%9B%AE%E5%90%8C%E6%AD%A5%E5%88%B0github%E4%B8%8A%E9%9D%A2%E7%9A%84%E6%96%B9%E6%B3%95/4d768eff52764c90abf2ffb9a8f08d3b.png)