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
