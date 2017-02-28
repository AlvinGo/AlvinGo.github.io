---
title: Process Explorer常用操作介绍
category: Windows Internal Tools
---

## Process Explorer出现的背景
Process Explorer可以看成是一个加强版的任务管理器。在较早的Windows版本中，任务管理器提供的功能是非常简单的（比如查看CPU、内存的使用情况，强制结束进程等），很难满足我们高级一些的需求。在这种情况下，Process Exploere就应运而生了，大大的方便了我们工作中监测进程和排除故障的工作。
![Process Explorer](https://i-technet.sec.s-msft.com/en-us/sysinternals/bb896653.processexplorer(en-us,MSDN.10).jpg)

[下载地址](https://technet.microsoft.com/en-us/sysinternals/processexplorer.aspx)

## 功能介绍
这里我会从实际应用的角度对Process Explorer的一些功能点进行介绍。

### 1. 替换任务管理器

Process Explorer提供了相对与任务管理器更加强大实用的功能，所以有的时候就会想着直接把任务管理器给替换掉得了。Process Explorer提供了这样一个功能，可以在用户触发打开任务管理器的操作的时候直接打开Process Explorer。

**操作步骤：**

> Options -> Replace Task Manager

![Replace Task Manager](/Images/WindowsUtilities/ReplaceTaskManager.jpg)

之后在我们运行Win+Esc、Ctrl+Shift+Del的时候打开的就是Process Explorer了。

### 2. 查看当前系统中运行的进程
Process Explorer对进程以树形图的形式进行展示，这样方便我们观察父子进程之间的关系。从这里我们可以看出来，绝大部分的窗体应用程序都是explorer.exe的子进程，大部分的后台进程都在services.exe下面：
![View Processes](/Images/WindowsUtilities/ViewProcesses.jpg)

Process Explorer会以不同的颜色标示不同状态的进程，比如：
![Colors](/Images/WindowsUtilities/Color.jpg)

* 浅蓝色: 和Process Explorer属于同一个用户的进程。
* 粉红色： 服务进程，通常会包含一个或多个Windows服务。
* 黄色： .NET进程。
* 深灰色： 挂起的进程。
* 紫色： 标识包含压缩或者加密的可执行代码的进程。一些病毒软件经常会利用这种方式绕过杀毒软件。
* 红色： 刚刚退出的进程。

我们还可以通过右键点击右侧列头选择显示我们感兴趣的属性：
![Process Columns](/Images/WindowsUtilities/ProcessColumns.jpg)

### 3. 查看进程的详细信息
如果我们对某个进程的感兴趣，我们可以双击这个进程查看它的详细信息：
![Process Info](/Images/WindowsUtilities/ProcessInfo.jpg)

这里值得一提的是**Command line**和**Current directory**这两个属性。

> Command line: 启动进程的时候调用的命令。从这里我们可以了解怎么样去调用这个进程，和有关当前进程启动的详细信息。

> Current directory: 当前进程活动所在的文件夹。

### 4. 查看文件正在被什么进程占用
我们在操作文件（删除、重命名等）的时候遇到错误提示，说文件正在被其他进程占用，无法执行操作。这个时候可以打开Process Explorer对文件进行查找：

> Ctrl + f

输入要查找的文件名就可以看到有那些进程正在使用这个文件了：
![Search File](/Images/WindowsUtilities/SearchFile.jpg)

双击搜到的进程Process Explorer会在下面高亮显示出对应的文件句柄。从这里我们可以强制关闭对应的句柄以达到不让文件被继续占用的目的。

### 5. 实时监控系统的性能
通过`View -> System Info`我们可以打开Performance窗口查看过去一段时间内系统的性能数据：
![SystemInfo](/Images/WindowsUtilities/SystemInfo.jpg)

我们也可以通过设置把感兴趣的性能数据固定在任务栏里显示：
![PerformanceTray](/Images/WindowsUtilities/PerformanceTrayIcon.jpg)

### 6. 获取Dump文件
借用百度百科的介绍，Dump文件是进程的内存镜像。通常在进程没有反应或者崩溃的时候我们需要借助Dump文件来分析进程里面发生了什么。
Process Explorer提供了一个快捷的方式来获取Dump文件：

> 右键点击进程 -> Create Dump

我们可以根据需要选择获取最小的dump还是完整的dump文件。

### 7. 进程操作
Process Explorer提供了很多进程级别的操作：
![Process Ops](/Images/WindowsUtilities/ProcessOperations.jpg)

### 8. 安全验证
Process Explorer提供了强大的进程查看功能帮助我们对进程信息的合法性进行检验，包括：

* 进程签名
* 进程路径
* 运行路径
* ...

### 9. 设置Symbols显示更详细的堆栈信息
设置Symbol之前：

![Before Symbols](/Images/WindowsUtilities/before_symbol.jpg)

设置Symbol之后：

![After Symbols](/Images/WindowsUtilities/after_symbol.jpg)

详细操作步骤请参考：

[Resolve Symbols in Process Explorer-Monitor Without Installing the Debugging Tools](https://windowsexplored.com/2012/01/31/resolve-symbols-in-process-explorer-monitor-without-installing-the-debugging-tools/)