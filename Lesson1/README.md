# XV6环境配置

这里我们推荐两种配置方法，一种是利用windows自带的虚拟机wsl来配置XV6，一种是在双系统Linux或虚拟机上配置XV6。

## 1. 基于WSL的XV6环境配置

首先检查运行wsl环境系统程序是否启动:

<img width="293" alt="1" src="https://github.com/user-attachments/assets/f9aff3a9-7949-4619-ad08-8a9925e95a4a" />

<img width="293" alt="2" src="https://github.com/user-attachments/assets/8bd8f492-ba8c-430e-be8a-099780ab280c" />

调整配置后，应该会提示重启。重启后，我们来安装wsl。这里有两种方法，一种是在windows powershell，使用 wsl --install -d ubuntu=24.04，或者可以直接在微软的应用商店搜索ubuntu，直接安装：

<img width="878" alt="3" src="https://github.com/user-attachments/assets/641fc7fb-793a-450b-b051-068d98f7d09c" />

安装完成后，在windows powershell下（右键，选管理员模式进入）

![image](https://github.com/user-attachments/assets/66e159a0-fe79-43ca-bcff-46c4187ef086)

初次进入系统时，会提示输入用户名和密码。等到输入确认后，就正式启动了windows下的linux虚拟机

接下里就是配置必要的环境，在sudo模式下，执行下面代码：

<pre class="prettyprint"><code class=" hljs xml">sudo apt-get update && sudo apt-get upgrade
sudo apt-get install git build-essential gdb-multiarch qemu-system-misc gcc-riscv64-linux-gnu binutils-riscv64-linux-gnu</code></pre> 

当完成全部的环境配置后，接下来我们下载xv6源代码：

https://github.com/mit-pdos/xv6-riscv.git

在该文件夹下，输入指令make qemu；如果看到如下输出，证明环境配置成功！

![image](https://github.com/user-attachments/assets/56664fcd-39c0-4223-a861-30cd44b1f03b)

## 使用VSCode链接WSL调试XV6

首先下载VScode，启动后，首先安装remote for wsl和C++ package

![image](https://github.com/user-attachments/assets/90e0035f-d160-49ef-a2ab-2af0d731dc12)

按下ctrl + shift + p,输入remote - WSL,就能自动连接本地的WSL环境了。接下来就是配置vscode项目文件：

首先在xv6项目里放一个文件夹，命名为.vscode

然后在该文件夹下放入launch.json和tasks.json(两个文件已在本代码库路径提供)

当配置好一切后，在VScode里运行：

![image](https://github.com/user-attachments/assets/51033098-1fce-47e7-9e3a-797efa526069)

项目进入调试状态，视为成功！

![image](https://github.com/user-attachments/assets/5a3e148b-ec2b-476a-a037-323fdec64a1f)

注意，这里如果你在运行时碰到如下问题：

![image](https://github.com/user-attachments/assets/35aa3ff3-dd8a-4c68-8970-f7ecd759e758)

你需要将.gdbinit.tmpl-riscv文件里的这行代码注释掉：

![image](https://github.com/user-attachments/assets/e4deaa35-c5c0-4d98-a16f-3bdbf6b92092)

## 2. 基于双系统Linux或虚拟机的环境配置

这里其实和wsl的配置方法是一样的。我们使用vbox作为虚拟机平台，安装ubuntu操作系统后，就按照sudo模式下做环境配置就可以。

VScode可以在应用商店直接下载。下载后，按照上面的步骤，安装C++包，添加.vscode文件夹，添加json文件。基本操作都是一样的。

## 3. 一些可能碰到的问题：

如果你在运行make qemu的时候，程序卡住了，没有出现...init starting sh字样, 较大概率是qemu版本不匹配造成的。建议ubuntu换成最新的24.04

环境配置如果出错时，可以重复执行下面代码，确保安装完整：

<pre class="prettyprint"><code class=" hljs xml">sudo apt-get update && sudo apt-get upgrade
sudo apt-get install git build-essential gdb-multiarch qemu-system-misc gcc-riscv64-linux-gnu binutils-riscv64-linux-gnu</code></pre> 
