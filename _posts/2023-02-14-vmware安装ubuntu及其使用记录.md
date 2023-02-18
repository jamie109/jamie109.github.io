---
layout: post
title: VMware安装Ubuntu及其使用记录
date: 2023-02-14 14:02 +0800
author: jamie109
categories: [Software, VMware]
tags: [Ubuntu] 
---  
>安装的时候一直卡，看log记录（在virtual machine的对应虚拟机文件夹下），说是没有装VMware tools。今天搞了一下午一晚上，不弄了。我重新下了VMware17。    
>Ubuntu16和它上面的VMware tools安装成功了，装VMware tools的时候，第一个问题要答yes，剩余的直接回车就行，就安好了。   

**记录VMware安装Ubuntu、对其调试更便于使用的过程，以及我在里面安装过的包等操作。**   

今天删掉了VMware以前安装的Ubuntu，腾出了将近了20G的空间（难怪做OS实验时越用越卡），**有预感这学期我会多次卸载重装。。。**    
> 虚拟机的磁盘是随着你的文件数量、创建、删除都在增长的，直到涨到你给它分配的那个空间为止。

![oswx.jpg](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/oswx.jpg)

## 1.Ubuntu的卸载   
* 点击左侧`我的计算机`中要删除的虚拟机，主页面会出现这个虚拟机（一个黑屏，没有开机）    
* 右键`我的计算机`中该虚拟机，然后`管理`，点击`从磁盘中删除`     
* 如果`管理`是灰的，看看主页面有没有出现这个虚拟机（一个黑屏，没有开机），没有的话重复步骤一

## 2.VMware安装Ubuntu   
1. 下载光盘映像（要desktop版的，上面写着LTS，比如Ubuntu 22.04.1 LTS），我一直使用的是**ubuntu-20.04.5-desktop-amd64.iso**，在OneDrive的backups文件夹中。 [ubuntu官网](https://ubuntu.com/download/desktop)    
2. 进入VMware，选择新建虚拟机，在弹出的窗口中选择`自定义（高级）C`，点击下一步。    
![20230214143844](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214143844.png){: width="400"}   
弹出新窗口，不用管它，下一步。这里得注意内存、处理器等的限制，后面设置的时候不能超过它们（一般情况都不会超出的，我不看，但为了流程的完整性还是要提一句的）   
![20230214144312](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214144312.png){: width="400"}   
3. 选择稍后安装OS   
![20230214144651](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214144651.png){: width="400"}      
4. 选择客户机OS（不用改，默认就是下面这样）    
![20230214144738](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214144738.png){: width="400"}     
5. 给虚拟机取名，只改名字就行，路径会自动给填上   
![20230214144923](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214144923.png){: width="400"}     
6. 处理器数量（我电脑是八核，这里设置了4核）**我又给改成了2核，把4改成了2**    
![20230214145213](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214145213.png){: width="400"}      
7. 内存默认2G，网络类型默认net，IO控制器选推荐的即可（LSI logic(L)，推荐），磁盘类型选推荐的（SCSI），选择磁盘类型（创建新新虚拟磁盘）   
8. 磁盘大小我设置了30G，选择将虚拟磁盘拆分成多个文件。    
![20230214150025](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214150025.png){: width="400"}     
9. 指定磁盘文件，直接点下一步；点击自定义硬件，移除打印机，选择CD/DVD，加入Ubuntu的映像文件。    
![20230214150523](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214150523.png){: width="400"}      
10. 点击完成，左侧`我的计算机`会出现该虚拟机。

## 3.Ubuntu正式安装   
<!-- * 第一次重装到下面的第五步，卡住了，然后我断开了网络，再次安装就很顺利，没有卡。把图中两个框的对勾取消。以后需要联网的时候在勾上就行。
    
   ![20230214161559](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214161559.png){: width="400"} 

   第二次重装，卡在了安装时复制文件。第三次重装，卡在了扫描镜像站。我打算卸掉VMware重装再装Ubuntu，那就得等考完os之后了。 -->
1. 开启该虚拟机，等一会儿，会弹出界面。选择中文简体，点击安装Ubuntu。（选English也可以，那么后面键盘布局就得选EnglishUS了）    
![20230214151743](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214151743.png){: width="400"}       

2. 会出现由于Ubuntu窗口太小，安装界面显示不全，导致无法点击继续按钮的问题。**按住Ctrl+Alt+T，出现终端窗口，然后在终端输入`xrandr -s 1280x800`，然后回车，数字之间是字母x**   
![20230214153706](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214153706.png){: width="400"}      
界面变大了！

![20230214153802](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214153802.png){: width="400"}  

3. 键盘布局选择中文（如果一开始语言选English，这里选EnglishUS），选择最小安装、安装时更新（图里没勾，记得勾上）。**这里必须选择安装时更新！！！一开始试了很多次都会在最后安装时卡住，今天把它选上了，就正常安装了。**
   <!-- 、安装时不更新。 -->
![](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/202302141547523.png){: width="400"}   
4. 耐心等几分钟。选择清除磁盘并安装Ubuntu，点击现在安装。   
![20230214154924](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214154924.png){: width="400"}     
5. 等了两分钟，弹出这个窗口，选择继续。    
![20230214155156](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230214155156.png){: width="400"}   
6. 时区选上海，设置用户名、计算机名、密码，就可以开始安装了。   
7. 安装，大约要等十几分钟。安装成功会需要重启，然后输入密码就能用了。 
      
## 4.Ubuntu使用     
### **界面太小**    
![20230215093024](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215093024.png){: width="400"}     
**解决方法：**     
1. 安装VMware tools（在虚拟机打开时）      
![20230215093437](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215093437.png){: width="400"}    

点击之后，显示正在下载VMware tools     

![20230215093547](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215093547.png){: width="400"} 

Ubuntu20.04.5，一开始好几次都遇到了点击下载VMware tools有弹窗的问题，跟着网上的答案做也没解决。都选择了重新安装。最后一次它突然没有出现弹窗，在Ubuntu窗口顶部弹出一个消息VMware tools，下面一个文件夹，我点进去，发现就是下载的VMware tools的安装包。就按步骤[VMware tool安装](https://blog.csdn.net/williamcsj/article/details/121019391)安装了，但是安装有错误core dumped，解决不了，无法从本机和虚拟机之间移动文件、复制粘贴。
<!-- 然后可能会有弹窗，如下，点击**否**     

![20230215093805](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215093805.png){: width="400"} 

2. 重新装VMware tools    
![20230215095059](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215095059.png){: width="400"}      
![20230215095443](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215095443.png){: width="400"}    
![20230215095522](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215095522.png){: width="400"}     
![20230215100048](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215100048.png){: width="400"} 

![20230215100124](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215100124.png){: width="400"}


![20230215100347](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215100347.png){: width="400"}    
![20230215100628](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215100628.png){: width="400"} -->

<!-- 关闭Ubuntu，修改CD/DVD，把它改成**VMware**安装目录下的**linux.iso**。
![20230215094306](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215094306.png)      -->
<!-- 重新安装VMware tools（跟1中步骤一样），出现下面弹窗选择**是**     -->
**装好了VMware tools但无法从本机win10复制文件到Ubuntu**，关机，打开共享文件选项，重启。  

![20230215123815](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215123815.png)

### 测试网络   
打开控制台，输入ping www.baidu.com，显示可以ping通，网络没有问题。其实网络的设置什么的都不用改，跟着安装流程走就可以。

![20230215092848](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215092848.png){: width="400"} 


### 换源     
  
```
备份文件（Ubuntu默认的源存在了sources.list）
sudo cp /etc/apt/sources.list sources_backup.list
修改文件   
sudo gedit /etc/apt/sources.list
更新源，把下面的代码粘到已经打开的sources.list中，原来的内容删掉
# Ubuntu16的阿里云源
deb http://mirrors.aliyun.com/ubuntu/ xenial main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main

deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main

deb http://mirrors.aliyun.com/ubuntu/ xenial universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates universe

deb http://mirrors.aliyun.com/ubuntu/ xenial-security main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main
deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security universe

更新源，执行下面这三条指令
sudo apt-get update
sudo apt-get -f install
sudo apt-get upgrade

```
![20230215124708](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215124708.png)

### Ubuntu16.04.1 i386 文件全屏打开找不到关闭按钮     
把鼠标移动到橙色框的位置，关闭、最小化按钮等就出来了。  

![20230215124211](https://cdn.jsdelivr.net/gh/jamie109/my-img/for-VSCode/20230215124211.png)

### Ubuntu与本机VSCode连接   
[CSDN链接](http://t.csdn.cn/bKhNI)  Ubuntu16.04.4连接报错，说the remote host's architecture is not support，网上找的帖子解决不了。




