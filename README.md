# 学校已经更新了ubuntu下的easy-connect包，不需要这个了
# zju-rvpn-ubuntu
这份文档将帮助你在 ubuntu16.04_64位 上搭建 rvpn 服务，让我们开始吧！

## 安装jre(java runtime environment)
选择1 安装旧版本的jre  
(1)下载 Linux 的 Java虚拟机安装文件: jre-版本-linux-x64.bin  
登录java(oracle) http://www.oracle.com/technetwork/java/javase/downloads/index.html  
用邮箱注册一个账号  
在上述页面找到 Java Archive, 点击 DOWNLOAD, 然后点击 Java SE 6, 找到 Java SE Runtime Environment 6u27, 选择 Accept License Agreement,  点击 jre-6u27-linux-x64.bin, 下载到 ~/Downloads 或者 ~/下载  
(2)打开终端  
```Bash
cd /usr/local/  
sudo mkdir java # 或者 sudo mkdir -p /usr/local/java  
cd ~/下载  # 或者在下载页面右键打开终端  
sudo cp -r jre-6u27-linux-x64.bin /usr/local/java # 拷贝一份  
cd /usr/local/java  
sudo chmod a+x jre-6u27-linux-x64.bin  
su # root一下  
./jre-6u27-linux-x64.bin # 运行文件  
# 成功后，Ctrl + D 关闭root  
```
```Bash
sudo gedit ~/.bashrc # 在文件末尾加上下面的代码(例子）    
# set Java environment  
export JAVA_HOME=/usr/local/java  
export JRE_HOME=${JAVA_HOME}/jre1.6.0_27  
export CLASSPATH=${JRE_HOME}/lib  
export PATH=${JRE_HOME}/bin:$PATH  
# 保存并关闭  
source ~/.bashrc # 生效  
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/local/java/jre1.6.0_27/bin/java" 1  
sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/local/java/jre1.6.0_27/bin/javaws" 1  
sudo update-alternatives --set java /usr/local/java/jre1.6.0_27/bin/java  
sudo update-alternatives --set javaws /usr/local/java/jre1.6.0_27/bin/javaws  
# 检查安装是否成功  
# 新打开终端  
java -version  
# 会出现如下字样，则安装成功  
java version "1.6.0_27"  
Java(TM) SE Runtime Environment (build 1.6.0_27-b07)  
Java HotSpot(TM) 64-Bit Server VM (build 20.2-b06, mixed mode)  
# 可以重启一下  
```
选择2 安装最新版jre  
待完善  

## 安装旧版 firefox/chrome 浏览器(以firefox为例)
因为高版本的这两种浏览器已经不支持java插件，所以需要安装旧版本的浏览器  
```Bash
# ubuntu16.04默认安装了高版本的firefox浏览器，先卸载  
sudo apt-get remove firefox  
```
下载旧版本: http://ftp.mozilla.org/pub/firefox/releases/31.0/linux-x86_64/zh-CN/  
这里使用31版本  
```Bash
cd ~/下载  
sudo tar -jxvf firefox-31.0.tar.bz2 # 解压  
sudo cp -R firefox /opt/  
```

## 关联插件与浏览器
```Bash
# 打开终端  
sudo mkdir -p /usr/lib/mozilla/plugins/  
cd /usr/lib/mozilla/plugins/  
sudo ln -s /usr/local/java/jre1.6.0_27/lib/amd64/libnpjp2.so  
# 如果 plugins 中有旧的 libnpjp2.so 需要删除  
```

## 打开浏览器
```Bash
cd /opt/firefox  
./firefox  
```
在首选项中改掉默认主页，关闭更新  
在网址栏输入 about:plugins 或者打开附加组件，可以看到 java 的一堆插件，证明关联成功  
访问 https://rvpn.zju.edu.cn 登录，浏览器会运行 java 插件，同意  
如果成功，会出现一个绿色图标  
如果卡在初始化界面，请往下看～  
```Bash
cd ~/.sangfor/ssl/shell/  
sudo ./sslservice.sh  
```
报错: error while loading shared libraries: libstdc++.so.6: cannot open shared object file: No such file or directory  
Ctrl + Z 结束任务  
```Bash
sudo apt-get install libstdc++6  
sudo apt-get install lib32stdc++6  
```
再次登录，如果还是卡在初始化界面，运行 sslcheck.sh 或者其他几个 .sh 文件  
再再次登录，成功。上述方法会使CPU被占用，无法杀死进程，万事重启之  
重启登录就不用运行 .sh 了  

又可以水98了~  
![](https://github.com/stormchasingg/zju-rvpn-ubuntu/blob/master/1.png)  
