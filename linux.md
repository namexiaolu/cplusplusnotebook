参考：https://zhuanlan.zhihu.com/p/74935718

## windows安装ubuntu 

商店直接搜索ubuntu 点击安装

apt无法安装东西参考：

https://blog.csdn.net/qin9800/article/details/105177721

## 怎么区分文件夹还是文件？

$ ls -l   输入这个命令
-rw-r--r-- 1 xiaolu xiaolu    8 Mar 20 10:14 file.txt     这个是文件
drwxr-xr-x 2 xiaolu xiaolu 4096 Mar 20 10:13 file1    开头为d的是文件夹

- 当为 **d** 则是目录
- 当为 **-** 则是文件；
- 若是 **l** 则表示为链接文档(link file)；
- 若是 **b** 则表示为装置文件里面的可供储存的接口设备(可随机存取装置)；
- 若是 **c** 则表示为装置文件里面的串行端口设备，例如键盘、鼠标(一次性读取装置)。

## 9个权限分别代表什么

![363003_1227493859FdXT](https://www.runoob.com/wp-content/uploads/2014/06/363003_1227493859FdXT.png)

[linux](https://so.csdn.net/so/search?q=linux&spm=1001.2101.3001.7020)系统文件夹644、755、777权限设置详解 ，左至右，

第一位数字代表文件所有者的权限，
第二位数字代表同组用户的权限，
第三位数字代表其他用户的权限。

而具体的权限是由数字来表示的，

读取的权限等于4，用r表示；
写入的权限等于2，用w表示；
执行的权限等于1，用x表示；

通过4、2、1的组合，得到以下几种权限：
0（没有权限）；
4（读取权限）；
5（4+1 | 读取+执行）；
6（4+2 | 读取+写入）；
7（4+2+1 | 读取+写入+执行）

例如chmod 777 给所有用户的权限都设置为读写执行、

chmod -R 777 递归给所有子文件和子文件夹都设置为可读可写可执行。



## 怎么查看当前进程？怎么执行退出？怎么查看当前路径？
**答案：**
查看当前进程：ps

​		-A 显示所有进程

![image-20220320102825756](C:\Users\xiaolu\AppData\Roaming\Typora\typora-user-images\image-20220320102825756.png)

​		-au 显示较详细的资讯

![image-20220320103017972](C:\Users\xiaolu\AppData\Roaming\Typora\typora-user-images\image-20220320103017972.png)

​		-aux 显示所有包含其他使用者的行程 

![image-20220320103045431](C:\Users\xiaolu\AppData\Roaming\Typora\typora-user-images\image-20220320103045431.png)

执行退出：exit  q
查看当前路径：pwd

![image-20220320104457490](C:\Users\xiaolu\AppData\Roaming\Typora\typora-user-images\image-20220320104457490.png)

## ps 和top 的区别（查查）

ps 为我们提供了进程的一次性的查看，它所提供的查看结果并不动态连续的；如果想对进程时间监控，应该用 top 工具。

输入top之后：![image-20220320104548578](C:\Users\xiaolu\AppData\Roaming\Typora\typora-user-images\image-20220320104548578.png)

## netstate

Linux下netstat命令详解

一、介绍
Netstat是控制台命令,是一个监控TCP/IP网络的非常有用的工具，它可以显示路由表、实际的网络连接以及每一个网络接口设备的状态信息。Netstat用于显示与IP、TCP、UDP和ICMP协议相关的统计数据，一般用于检验本机各端口的网络连接情况。

## Ls 命令执行什么功能？可以带哪些参数，有什么区别？
**答案：**
ls 执行的功能：列出指定目录中的目录，以及文件
哪些参数以及区别：a 所有文件l 详细信息，包括大小字节数，可读可写可执行的权限等

ls -l -h 以人话显示文件占用内存

## vim简单用法

1. vi + 文件名  创建一个文件，并编辑
2. 英文状态下输入 i进入编辑模式
3. 随意写内容
4. 按esc 退出编辑模式
5. 输入  "  :wq  "  保存

## 复制文件夹

cp a文件 ~/文件夹/b文件     将当前目录下的a文件复制到 /home/文件夹  中并重命名为b文件

cp -r a文件夹 ~/文件夹/b文件夹    将当前目录下的a文件复制到 /home/文件夹  中并重命名为b文件

## 小技巧

~ 代表home目录

cd 什么也不写 代表回到home目录

cd - 代表回到上一步的目录

cd .. 回到上一层目录

mv 移动文件夹不用加-r

scp -r   ~/b/  xiaofanfan@10.1.1.1:~/a

cat 读取文件





## 用什么命令对一个文件的内容进行统计？(行号、单词数、字节数)
**答案：**

wc 命令 - c 统计字节数 - l 统计行数 - w 统计词数。

## 查找文件中的内容

cat | grep l1



## 终止进程用什么命令? 带什么参数?

kill [-s <信息名称或编号>][程序] 或 kill [-l <信息编号>]

kill-9 pid

## 搜索文件用什么命令? 格式是怎么样的?

**答案：**

find <指定目录> <指定条件> <指定动作>

whereis 加参数与文件名

locate 只加文件名

find 直接搜索磁盘，较慢。

find / -name "string*"

## 使用什么命令查看磁盘使用空间？空闲空间呢?

df -hl

## du 和 df 的定义，以及区别？
du 显示目录或文件的大小

df 显示每个<文件>所在的文件系统的信息，默认是显示所有文件系统。
（文件系统分配其中的一些磁盘块用来记录它自身的一些数据，如 i 节点，磁盘分布图，间接块，超级块等。这些数据对大多数用户级的程序来说是不可见的，通常称为 Meta Data。） du 命令是用户级的程序，它不考虑 Meta Data，而 df 命令则查看文件系统的磁盘分配图并考虑 Meta Data。
df 命令获得真正的文件系统数据，而 du 命令只查看文件系统的部分情况。
