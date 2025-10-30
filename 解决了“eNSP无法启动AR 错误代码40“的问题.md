![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/original.png)

粉丝可见 [Jianghong Jian](https://blog.csdn.net/2501_93097309 "Jianghong Jian") ![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/newUpTime2.png) 已于 2025-10-13 23:13:47 修改

版权声明：本文为博主原创文章，遵循 [CC 4.0 BY-SA](http://creativecommons.org/licenses/by-sa/4.0/) 版权协议，转载请附上原文出处链接和本声明。

当你已经完成了所有安装内容，准备打开[eNSP](https://so.csdn.net/so/search?q=eNSP&spm=1001.2101.3001.7020)启动AR，结果“启动失败”，

![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/a5c2662245f544dd8c535ab1a368c638.png)于是按照官方文档逐一排查，无果，这个时候可以看下博主的方法。

官方文档可以点击红色提示自行查看，在此不再过多赘述。

## 第一步：关闭虚拟化的安全性

win+R，输入cmd，![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/88c42c717b4c4417a03485f88b9b8f7c.png)

用ctrl+shift+enter以管理员身份打开终端，输入

```cobol
bcdedit /set hypervisorlaunchtype off
```

回车运行，

![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/192d5696c0bb4e68aeb0da2fd2a42700.png)

<u><strong>一定一定一定要重启电脑才能生效！！！</strong></u>

验证是否成功，win+r输入msinfo32，

![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/bab7319b82524538abc71f90c535a17c.png)

回车打开显示已关闭，则此步完成。

## ![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/bf74de6dc81a4386944117231d22354e.png)第二步：关闭内核隔离

设置-搜索“内核隔离”-关闭

![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/96d8a0aed7984235b99c2a185528a986.png)

## 第三步：关闭防火墙

控制面板-系统和安全-WindowsDefender防火墙-启用或关闭Windows防火墙-两个都

关闭![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/04afb8e49b1f4b799b9c244de5165c7d.png)

![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/b91f0a66b2c148bfbb1acdf14c9d418b.png)

![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/f85b1b9c4cf64feb9292b0d8527ce8d6.png)

## 第四步：设置以“管理员身份运行VirtualBox”

选中VirtualBox，右键属性，勾选“兼容性”和“以管理员身份运行这个程序”，然后应用，确定。![](%E5%8E%86%E6%97%B6%E5%85%AD%E4%B8%AA%E5%B0%8F%E6%97%B6%E7%9A%84%E6%8A%98%E7%A3%A8-%E7%BB%88%E4%BA%8E%E8%A7%A3%E5%86%B3%E4%BA%86%E8%BF%99%E4%B8%AAens/6ccc274ee0904d5fba0210a458f07705.png)

完成以上四步，再加上结合官方文档检查虚拟网卡的配置，基本上就没有问题了，现在可以正常打开AR了。

PS:相关配置修改后一定要重启软件才能生效，第一步关闭虚拟化的安全性一定一定一定要重启电脑！
