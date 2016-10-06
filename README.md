##description DOL 框架
- 1.下载虚拟机，虚拟机上装Ubantu
 - [VMWARE教程](http://jingyan.baidu.com/article/0320e2c1ef9f6c1b87507bf6.html)
 - [VIRTUALBOX教程](http://jingyan.baidu.com/article/cdddd41c5eea3153ca00e160.html)
 - [Ubuntu下载](http://www.ubuntu.com/download/desktop)
- 2.安装必要的环境<br>
   `$ sudo apt-get update`<br>
   `$ sudo apt-get install ant`<br>
   `$ sudo apt-get install openjdk-7-jdk`<br>
   `$ sudo apt-get install unzip`<br>

- 3.下载文件<br>
 - `$ sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz`<br>
 - `$ sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_erhz.zip`<br>

- 4.解压文件<br>
 - 新建dol的文件夹 <br>
    `$ mkdir dol`
 - 将dolethz.zip解压到 dol文件夹中<br>
    `$ unzip dol_ethz.zip -d dol`
 - 解压systemc<br>
    `$ tar -zxvf systemc-2.3.1.tgz`

- 5.编译systemc<br>
 - 解压后进入systemc-2.3.1的目录下<br>
   `$ cd systemc-2.3.1`
 - 新建一个临时文件夹objdir<br>
   `$ mkdir objdir`
 - 进入该文件夹objdir<br>
   `$ cd objdir`
 - 运行configure (能根据系统的环境设置一下参数，用于编译)<br>
   `$ ../configure CXX=g++ --disable-async-updates`<br>
   运行后如图所示：<br>
   ![configure](https://cl.ly/2F431s2P1d2U)
 - 编译<br>
   `$ sudo make install`
 - 编译完后文件目录如下<br>
   ![目录](https://cl.ly/1Y1T27442P2H)<br>
   再查看路径<br>
   `$ cd ..  `      
   `$ ls`<br>
   `pwd`<br>
    比如：<br>
	![路径](https://cl.ly/0X0x473y200x)<br>
    路径为：/root/systemc-2.3.1
- 6.编译dol<br>
 - 进入刚刚dol的文件夹<br>
           <code>$ cd ../dol
 - 修改build_zip.xml文件<br>
   找到下面这段话，就是说上面编译的systemc位置在哪里，<br>
   `<property name="systemc.inc" value="YYY/include"/>`<br>
   `<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>`<br>
   把YYY改成上页pwd的结果<br>
  （注意，对于  64位 系统的机器，lib-linux要改成lib-linux64）
 - 然后是编译<br>
   `$ ant -f build_zip.xml all`
 - 若成功会显示build successful<br>
   接着试试运行第一个例子<br>
   进入build/bin/mian路径下<br>
   `$ cd build/bin/main`
 - 然后运行第一个例子<br>
   `$ ant -f runexample.xml -Dnumber=1`<br>
   如果成功，则如图所示<br>
	![成功图片](https://cl.ly/1l2U2X2e1g1M)
##how to install 安装笔记
 - 这次环境配置的实验遇到的问题比较个例，不具有普遍性<br>
   - 前期由于我的电脑是32位的WIn7系统，装载VMware虚拟机，版本只能装载到版本10，版本11和12都只能安装于64位的Win系统;
   - 于是就只能装VMware10,但是Vmware10装载后前几天运行还是正常的<br>
     但后来有一次我把虚拟机关机之后，再打开虚拟机，就无法打开Ubantu虚拟机了，创建的虚拟机文件都找得到，但就是打不开。
   - 上百度搜索了解决方法，也有人遇到这种情况但是没有解决方法；<br>于是上知乎找，上面有人给出了官方的回复，大概的意思是说：<br>
   很抱歉，这是VMware10存在的一个bug，他们在修复，然后后面有人跟帖说版本10以上的就不会有这个bug了；
   - 看到这个答案，很奔溃，既然这个bug是存在VMware10里面的，但32位系统能装的最高版本就是VMware10了，无奈之下只能将32位的WIn系统换成64位的win系统；<br>
   - 换了系统之后，安装给出的指南，一路畅通无阻，完成了DOL环境配置。
    
##experimental experience 实验感想
- 该实验遇到的问题比较个人化，不具有普遍性，使得我只能自己上百度知乎搜索，当然也问了TA，但这个问题比较少见，TA也不清楚。遇到的这个问题算是自己电脑版本较低，不得不升级的无奈。