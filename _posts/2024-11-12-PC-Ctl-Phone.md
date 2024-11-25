---
title: "投屏工具"
date: 2024-11-12T15:31:29+0900
categories:
  - Leo
tags:
  - Android
  - update
---
缘起
* **两个工具**
  scrcpy:投屏工具[scrcpy](https://github.com/Genymobile/scrcpy)
  autoadb：连接后adb自动启动scrcpy[autoadb](https://github.com/rom1v/autoadb)
* **解决目标**
  实现无命令行框在电脑插入数据线后自动投屏
* **需求分析，难点及解决思路**
  scrcpy 1.17下载后自带的命令中有无控制台（命令行）的方案  scrcpy-noconsole.vbs         
  
  困难在于公司电脑无法直接运行vbs命令且不能自动投屏，因此需要autoadb建立快捷方式的方法来映射程序去自动启动scrcpy。
<u>右键建立vbs的快捷方式后在Target前加入C:\Windows\System32\wscript.exe //e:vbscript</u>
------
  #### 操作步骤
1. 从github下载最新版的两个工具文件，放置在同一目录
2. 在该目录建一个autoadb.vbs文件，启动autoadb及scrcpy
3. 右键此vbs文件建立快捷方式 在Target前加入C:\Windows\System32\wscript.exe //e:vbscript
4. Win10中按键盘上的win+R弹出Run窗口，输入shell:startup 点击OK
5. 将第3步建立的快捷方式复制到第4步打开的自动启动文件夹内 
* * *
* * *
#### 详解
- **第2步的vbs代码实现了无控制台（命令行)的自动启动，如下分别介绍**
*CreateObject("Wscript.Shell").Run "cmd /c autoadb scrcpy -s {} -Sw --window-x 1920 --window-y 27 --window-width 512 --window-height 1024", 0, false*
```
CreateObject("Wscript.Shell").Run "cmd /c .....", 0, false
```
是实现无控制台（命令行)的vbs代码
```
 autoadb scrcpy -s {} 
```
是autoadb启动scrcpy的代码
```
-Sw --window-x 1920 --window-y 27 --window-width 512 --window-height 1024 
```
是 scrcpy的参数，可根据需求进行定制
- **第3步快捷方式**

![](https://cdn.nlark.com/yuque/0/2024/png/26130036/1732513562836-0126d59f-694c-44a0-93f6-4da486797dca.png)
