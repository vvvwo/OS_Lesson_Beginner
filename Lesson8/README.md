# XV6实验内容

该部分主要介绍对应XV6课程实验，包括一些配置和注意事项，以方便学生能够顺利完成实验作业

## 1. 在XV6系统上实现一个user函数功能

我们在进入xv6系统后，实际上就可以通过命令调用使用功能函数，例如，输入命令ls能够导出系统支持的用户函数。用户函数可以在源码的usr文件夹下查看。

<img src="https://github.com/user-attachments/assets/a446fd11-e405-45b4-a0a9-a837d71b21d5" height="300px">

<img src="https://github.com/user-attachments/assets/313c5891-fcd9-4a4c-bf5f-062e692c8cb3" height="300px">

这里我们以echo函数为例，该函数就是一个IO函数，能够实现一个简单的输入输出命令，原始代码也很简单：

![image](https://github.com/user-attachments/assets/1f794549-bdee-415d-8118-86cf8768697e)

echo的原始代码：

<pre class="prettyprint"><code class=" hljs xml">#include "kernel/types.h"
#include "kernel/stat.h"
#include "user/user.h"
int
main(int argc, char *argv[])
{

  printf("Hello! this ia a first redesigned function based on XV6!\n"); 
  int i;
  for(i = 1; i < argc; i++){
    write(1, argv[i], strlen(argv[i]));
    if(i + 1 < argc){
      write(1, " ", 1);
    } else {
      write(1, "\n", 1);
    }
  }
  exit(0);
}</code></pre> 

这段代码是一段可读性非常好的c代码

我们希望写一个新的echo函数，能够提供一些新的功能，如增加一些提示语或颠倒输出的顺序：

![image](https://github.com/user-attachments/assets/428a23d4-38cc-4e21-aff6-be3e0827646c)

首先，我们在usr文件夹下，创建一个新的.c文件，命名为echo2.c

![image](https://github.com/user-attachments/assets/d7139e86-b378-43f1-a091-8dc1a8ec3197)

然后在原始的echo.c代码的基础上，修改为我们希望其执行的程序：

<pre class="prettyprint"><code class=" hljs xml">#include "kernel/types.h"
#include "kernel/stat.h"
#include "user/user.h"

int
main(int argc, char *argv[])
{

  printf("Hello! this ia a first redesigned function based on XV6!\n"); 
  int i;
  for(i = 1; i < argc; i++){
    write(1, argv[i], strlen(argv[i]));
    if(i + 1 < argc){
      write(1, " ", 1);
    } else {
      write(1, "\n", 1);
    }
  }
  exit(0);
}</code></pre> 

注意，这里我们只是写了一个c源码，为了能够让xv6的kernel函数识别并自动加载我们的函数，我们需要在makefile文件进行配置，具体如下：

![image](https://github.com/user-attachments/assets/a2cd9627-1ac3-4fe0-b34c-a7fd60f14421)

在UPROGS处添加函数的信息：

<img src="https://github.com/user-attachments/assets/c4653340-ee9b-4019-a3a0-d82c23515fcb" height="300px">

回到xv6原始的路径，运行make命令，实现对函数的链接和编译：

![image](https://github.com/user-attachments/assets/18f5b58b-68eb-4d5e-870d-cefc2fbbe68f)

此时，再次执行make qemu启动系统，调用ls，我们就能够看到新的函数被添加在可使用的函数列表：

<img src="https://github.com/user-attachments/assets/5d53e96a-80d1-4a1e-aa5f-141d751bb4b3" height="300px">

