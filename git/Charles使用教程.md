# 简介

Charles 是在 Mac （Charles是跨平台的 ）下常用的网络封包截取工具，在做移动开发、测试时，我们为了调试与服务器端的网络通讯协议，常常需要截取网络封包来分析。

Charles 通过将自己设置成系统的网络访问代理服务器，使得所有的网络访问请求都通过它来完成，从而实现了网络封包的截取和分析。

除了在做移动开发中调试端口外，Charles 也可以用于分析第三方应用的通讯协议。配合 Charles 的 SSL 功能，Charles 还可以分析 Https 协议。

Charles 主要的功能包括：

- 抓取 Http 和 Https 的请求和响应，抓包是最常用的了。
- 重发网络请求，方便后端调试，复杂和特殊情况下的一件重发还是非常爽的（捕获的记录，直接 repeat 就可以了，如果想修改还可以修改）。
- 修改网络请求参数（客户端向服务器发送的时候，可以修改后再转发出去）。
- 网络请求的截获和动态修改。
- 支持模拟慢速网络，主要是模仿手机上的 2G/3G/4G 的访问流程。
- 支持本地映射和远程映射，比如你可以把线上资源映射到本地某个文件夹下，这样可以方面的处理一些特殊情况下的 bug 和线上调试（网络的 css，js 等资源用的是本地代码，这些你可以本地随便修改，数据之类的都是线上的环境，方面在线调试）；
- 可以抓手机端访问的资源（如果是配置 HOST 的环境，手机可以借用 host 配置进入测试环境

**官网：** https://www.charlesproxy.com

**下载&安装：**https://www.charlesproxy.com/latest-release/download.do

**注册信息：**

~~~javascript
Registered Name: https://zhile.io
License Key: 48891cf209c6d32bf4
~~~

注册码来自于网络，注册码 Windows 和 Mac 通用。

# Charles 主界面介绍

![image-20230328143809116](C:\Users\HP288G3\AppData\Roaming\Typora\typora-user-images\image-20230328143809116.png)

## 菜单导航栏

Charles 的主菜单包括：`File`、`Edit`、`View`、`Proxy`、`Tools`、`Window`、`Help`。用的最多的主菜单分别是 `Proxy` 和 `Tools`。

### Proxy菜单

Charles 是一个 HTTP 和 SOCKS 代理服务器。代理请求和响应使 Charles 能够在请求从客户端传递到服务器时检查和更改请求，以及从服务器传递到客户端时的响应。下面主要介绍 Charles 提供的一些代理功能。Proxy 菜单的视图如下图所示：

![image-20230328145707955](C:\Users\HP288G3\AppData\Roaming\Typora\typora-user-images\image-20230328145707955.png)

- Start/Stop Recording：开始/停止记录会话。
- Start/Stop Throttling：开始/停止节流。
- Enable/Disable Breakpoints：开启/关闭断点模式。
- Recording Settings：记录会话设置。
- Throttle Settings：节流设置。
- Breakpoint Settings：断点设置。
- Reverse Proxies Settings：反向代理设置。
- Port Forwarding Settings：端口转发。
- Windows Proxy：记录计算机上的所有请求。
- Proxy Settings：代理设置。
- SSL Proxying Settings：SSL 代理设置。
- Access Control Settings：访问控制设置。
- External Proxy Settings：外部代理设置。
- Web Interface Settings：Web 界面设置。

### Tools菜单

Charles 是一个 HTTP 和 SOCKS 代理服务器，所有的请求都会经过 Charles。下面主要介绍 Charles 提供的一些实用工具。Tools 菜单的视图如下图所示：

![image-20230328145939302](C:\Users\HP288G3\AppData\Roaming\Typora\typora-user-images\image-20230328145939302.png)

- No Caching Settings：禁用缓存设置。
- Block Cookies Settings：禁用 Cookie设置。
- Map Remote Settings：远程映射设置。
- Map Local Settings：本地映射设置。
- Rewrite Settings：重写设置。
- Black List Settings：黑名单设置。
- White List Settings：白名单设置。
- DNS Spoofing Settings：DNS 欺骗设置。
- Mirror Settings：镜像设置。
- Auto Save Settings：自动保存设置。
- Client Process Settings：客户端进程设置。
- Compose：编辑修改。
- Repeat：重复发包。
- Repeat Advanced：高级重复发包。
- Validate：验证。
- Publish Gist：发布要点。
- Import/Export Settings：导入/导出设置。
- Profiles：配置文件。
- Publish Gist Settings：发布要点设置。

## 工具导航栏

Charles 顶部为菜单导航栏，菜单导航栏下面为工具导航栏。视图如下图所示：

![image-20230328144320224](C:\Users\HP288G3\AppData\Roaming\Typora\typora-user-images\image-20230328144320224.png)

Charles 主要提供两种查看封包的视图，分别名为 `Structure` 和 `Sequence`。

- **Structure**： 此视图将网络请求按访问的域名分类。
- **Sequence**： 此视图将网络请求按访问的时间排序。

使用时可以根据具体的需要在这两种视图之前来回切换。请求多了有些时候会看不过来，Charles 提供了一个简单的 `Filter` 功能，可以输入关键字来快速筛选出 URL 中带指定关键字的网络请求。

> 对于某一个具体的网络请求，你可以查看其详细的请求内容和响应内容。如果请求内容是 POST 的表单，Charles 会自动帮你将表单进行分项显示。如果响应内容是 JSON 格式的，那么 Charles 可以自动帮你将 JSON 内容格式化，方便你查看。如果响应内容是图片，那么 Charles 可以显示出图片的预览。

# Charles 使用教程

## PC端抓包

Charles 会自动配置浏览器和工具的代理设置，所以说打开工具直接就已经是抓包状态了。只需要保证一下几点即可：

1. 确保 Charles 处于 Start Recording 状态。

2. 勾选 **Proxy | Windows Proxy** 。

   ![image-20230328151301493](C:\Users\HP288G3\AppData\Roaming\Typora\typora-user-images\image-20230328151301493.png)

## 移动端抓包

1、使手机和电脑在一个局域网内，不一定非要是一个 IP 段，只要是在同一个路由器下即可。

2、电脑端配置：

- 关掉电脑端的防火墙（这点很重要）。
- 打开 Charles 的代理功能：通过主菜单打开 **Proxy | Proxy Settings** 弹窗，填入代理端口(端口默认为 `8888`，不用修改)，勾选 `Enable transparent HTTP proxying`。
- 如果不需要抓取电脑上的请求，可以取消勾选 **Proxy | Windows Proxy** 和 **Proxy | Mozilla FireFox Proxy**。

3、手机端配置

- 通过 Charles 的主菜单 **Help | Local IP Address** 或者通过命令行工具输入 `ipconfig` 查看本机的 IP 地址。

  ![image-20230328150534780](C:\Users\HP288G3\AppData\Roaming\Typora\typora-user-images\image-20230328150534780.png)

- 设置代理：打开手机端的 WIFI 代理设置，输入电脑 IP 和 Charles 的代理端口。

  ![image-20230328150649977](C:\Users\HP288G3\AppData\Roaming\Typora\typora-user-images\image-20230328150649977.png)

4、设置好之后，我们打开手机上的任意需要网络请求的程序，就可以看到 Charles 弹出手机请求连接的确认菜单（只有首次弹出），点击 **Allow** 即可完成设置。

![image-20230328150735053](C:\Users\HP288G3\AppData\Roaming\Typora\typora-user-images\image-20230328150735053.png)

5、完成以上步骤，就可以进行抓包了。

![image-20230328151012464](C:\Users\HP288G3\AppData\Roaming\Typora\typora-user-images\image-20230328151012464.png)

