# Windows Server 2016 安装 WebDAV

参考文献：
[在IIS7和更高版本上安装和配置WebDAV](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-webdav-on-iis) 
[使用WebDAV重定向器](https://docs.microsoft.com/en-us/iis/publish/using-webdav/using-the-webdav-redirector#troubleshooting-the-webdav-redirector)

## 编写目的

自己用Windows Server搭建了家用NAS主机，WebDAV的文件共享方式当然也是必不可少的。

网上众多WebDAV安装教程，逐个尝试未果，多个版本的Windows Server资料混杂，搭建实在不容易，经过努力编写了以下教程防止后来人踩坑，步骤详细，只要必要条件不缺失一定可以成功的。

如果遇到了错误，可以参考官网的错误代码原因：[WebDAV重定向器故障排除](https://docs.microsoft.com/en-us/iis/publish/using-webdav/using-the-webdav-redirector#troubleshooting-the-webdav-redirector)。

原创编写不易，如果能帮助到你，请点赞支持，转载请保留出处。

## 先决条件：

- 由IIS安装创建的默认网站必须仍然存在。
- 必须安装Internet Information Services管理器。
- 必须安装Windows身份验证。
- 必须安装WebDAV重定向程序。

## 服务安装：

1. 打开"**添加角色和功能**"

![img](https://pic2.zhimg.com/v2-b29aec097fb39e3a8c9cd03aaa246f01_b.png)

\2. 点击下一步直到**服务器角色选择**界面

![img](https://pic2.zhimg.com/v2-d2fac91f018264ae283218c8132dfae9_b.png)

![img](https://pic1.zhimg.com/v2-3b5eb97c8e34510ce162cd570f848cc0_b.png)

![img](https://pic2.zhimg.com/v2-6374f4bad1c88f3179549d3e399b4a19_b.png)

\3. 在**服务器角色界面**勾选"**Web 服务器(IIS)**"

![img](https://pic2.zhimg.com/v2-6e9c868244af00b09f2bee685d56e4cd_b.png)

\4. 在**功能**界面勾选"**WebDAV重定向程序**"

![img](https://pic2.zhimg.com/v2-da1c929e680188d29b44e680e0f25ca1_b.png)

\5. 在**角色服务**界面勾选"**Windows 身份验证、WebDAV发布**"

![img](https://pic4.zhimg.com/v2-58c1d89445a10b256b4d73b3543b18df_b.png)

\6. 在**确认**界面勾选"**如果需要，自动重新启动目标服务器"**，弹窗点击"**是**"，然后点击"安装"

![img](https://pic2.zhimg.com/v2-caaad6ab1ba290f12008a215d650c901_b.png)

\7. 功能安装中，安装完成后会自动重启服务器

![img](https://pic2.zhimg.com/v2-4b89f8d0fa48389a116671cabc879b21_b.png)

\8. 重启完成后自动弹出安装进度，等到安装完成后关闭窗口

![img](https://pic1.zhimg.com/v2-5d0f963197dbde88823a00bc024b5c20_b.png)

## WebDAV服务配置

1. 先创建用于WebDAV共享的文件

![img](https://pic4.zhimg.com/v2-6c7492aed41c95796d31422cbeef3a8b_b.png)

\2. 打开**"Internet Information Services (IIS)管理器"**

![img](https://pic3.zhimg.com/v2-4dfe480ada4fcead57e087813ae3405e_b.png)

\3. 在**"Default Web Site"**上右击"添加虚拟目录"

![img](https://pic4.zhimg.com/v2-c90fffcc8c14bf8c91dc6f49604605db_b.png)

\4. 填写别名为"WebDAV"，物理路径为"C:\WebDAV"

![img](https://pic2.zhimg.com/v2-e98d4d8f6a2f42d95765f90a72659741_b.png)

\5. 左侧选择**"WebDAV"**，打开**"WebDAV创作规则"**

![img](https://pic1.zhimg.com/v2-7fd460c314a03304f48af08b8abde19c_b.png)

\6. 右击**"添加制作规则"**

![img](https://pic1.zhimg.com/v2-3ab81ce2972c01a25b46b25dadd65194_b.png)

\7. 添加制作规则，选择所有用户，给予读取、源、写入权限

![img](https://pic4.zhimg.com/v2-0f6d1635cbe28c423dc9d0034c461f73_b.png)

\8. 左侧选择**"WebDAV"**，打开**"身份验证"**

![img](https://pic4.zhimg.com/v2-801ff613fb744102bbc94c50b5668b03_b.png)

\9. 启用**"Windows身份验证"**，禁用**"匿名身份验证"**

![img](https://pic3.zhimg.com/v2-cd60f90ece329da949dc390f3c10d626_b.png)

\10. 重启启动站点

![img](https://pic2.zhimg.com/v2-df1027d65f79cf76686c879532cde731_b.png)

*原创编写不易，如果能帮助到你，请点赞支持，转载请保留出处。*

## 使用WebDAV

1. 在此电脑上右击打开**"映射网络驱动器"**

![img](https://pic4.zhimg.com/v2-685c0d1518ba282c19c29f21e3cc71a3_b.png)

\2. 填写WebDAV地址**"**[**http://localhost/WebDAV**](http://localhost/WebDAV)**"**

![img](https://pic4.zhimg.com/v2-47599a1d7686b5c9ccf84c05b81d9d53_b.png)

\3. 连接成功后会弹出WebDAV的文件，到此为止可以愉快的使用WebDAV

![img](https://pic2.zhimg.com/v2-cb0282c63279c134b610942d5d118301_b.png)

原创编写不易，如果能帮助到你，请点赞支持，转载请保留出处。