#Shadowsocks Client
shadowsocks是第三方开发的，利用SOCKS5的代理服务器软件。本教程讲述如何通过配置Shadowsocks客户端进行翻墙。
该教程提供本作者的代理服务器并已经进行了aes加密，确保网络稳定安全。但任何人利用该方法而造成的`密码账号丢失`，或者进行`违法犯罪活动`，`本人不承担任何责任`。

##必备软件和环境
* 操作系统 : windows xp/7/8/10
* 浏览器 : chrome(没有请自行安装)
* shadowsocks客户端(当前仓库中配备)
* SwitchyOmega.crx(当前仓库中配备)
 
##步骤
###一、下载当前仓库
<p>
  <img src="https://github.com/lsj9383/ss-client-configuration/blob/master/icon/DownloadZip.png?raw=true" alt="DownloadZip"/>
</p>

###二、浏览器插件
浏览器要安装插件后，才能使通信数据在代理服务器中转。本文利用的是Google提供的Chrome浏览器，安装并配置对应插件后，才能使用代理服务器。这里使用的插件就是SwitchyOmega。<br>
首先打开chrome的扩展程序，以安装插件
<p>
  <img src="https://github.com/lsj9383/ss-client-configuration/blob/master/icon/OpenPlugin.png?raw=true" alt="OpenExternApp"/>
</p>
将会显示扩展程序面板
<p>
  <img src="https://github.com/lsj9383/ss-client-configuration/blob/master/icon/ExternApp.png?raw=true" alt="ExternApp"/>
</p>
然后打开将SwitchyOmega.crx拖拉进该面板中，便会进行安装该插件，如下图所示
<p>
  <img src="https://github.com/lsj9383/ss-client-configuration/blob/master/icon/Install1.png?raw=true" alt="Install"/>
</p>
接着点击添加`扩展程序`
<p>
  <img src="https://github.com/lsj9383/ss-client-configuration/blob/master/icon/Install2.png?raw=true" alt="Install"/>
</p>
现在，已经安装好了插件，可以进行插件的配置了。对刚刚安装的插件，单击`选项`，进行配置:
<p>
  <img src="https://github.com/lsj9383/ss-client-configuration/blob/master/icon/Conf.png?raw=true" alt="Conf"/>
</p>
在配置界面中，单击`proxy`，将各项参数修改为如图所示，并单击`应用选项`，使配置生效：
<p>
  <img src="https://github.com/lsj9383/ss-client-configuration/blob/master/icon/Configuration.png?raw=true" alt="Configuration"/>
</p>
至此，浏览器已经支持了代理服务器了。只需要单击下图中的`proxy`，浏览器的发送和请求就是通过代理服务器进行的了。
<p>
  <img src="https://github.com/lsj9383/ss-client-configuration/blob/master/icon/Proxy.png?raw=true" alt="Proxy"/>
</p>

###三、Shadowsocks配置
Shadowsocks简称ss，它不需要安装，直接双击便可以使用，它是一个本地代理，所有的数据都是通过ss到远程服务器上去获取的。<br>
<p>
  <img src="https://github.com/lsj9383/ss-client-configuration/blob/master/icon/InitSS.png?raw=true" alt="InitSS"/>
</p>
* 服务器IP: `209.141.35.237`
* 服务器端口号: `9005`
* 密码: `common`
* 代理端口: `1080`

<br>单击确定后，配置完成。<br>
最后，只需要启用ss客户端即可。
<p>
  <img src="https://github.com/lsj9383/ss-client-configuration/blob/master/icon/Start.png?raw=true" alt="Start"/>
</p>
配置完成后，会在当前路径下生成`gui-config.json`文件。每次打开ss，都会读取该配置文件，以便进行自动配置。

###四、启动
每次启动，只需要双击shadowsocks.exe 并且 在浏览器中启用`proxy`即可。<br>


##Shadowsocks原理
工作架构如下图所示：
<p>
  <img src="https://github.com/lsj9383/ss-client-configuration/blob/master/icon/Frame.png?raw=true" alt="Start"/>
</p>
###Shadowsocks Server进程
ss Server进程，接收Shadowsocks Client进程的请求后，向网络请求数据，并返回数据给ss Client经常。
###shadowsocks Client进程
ss Client进程，接收浏览器进程的请求后，向ss Server请求数据，并返回数据给浏览器进程。对于ss Server来说，这个经常是客户端，但是对于浏览器来说，这个进程是个代理服务器进程。
###浏览器进程
浏览器进程，接收到人类用户的交互请求后，向ss Client进程请求数据，并将数据呈现在浏览器上。
###总结
浏览器的插件，并非直接向`远处服务器`获取数据，而是向`本地代理服务器`获取数据，再由`本地代理服务器`，向`远程服务器`获取。<br>
之所以要多一步`本地代理服务器`，是为了方便管理多用户和数据加密。这也是为什么配置浏览器插件的时候，`代理服务器`选择的是127.0.0.1这一本地IP，端口也是和ss client的代理端口一致。