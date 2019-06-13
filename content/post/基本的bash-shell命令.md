---
title: "基本的bash shell命令"
date: 2019-06-09T20:28:49+08:00
draft: false
emoji: true
tags: ['shell']
categories: ['linux']
---
## 文件和目录列表 ##

### 基本列表功能 ###
* `ls -alF`:以长列表形式显示所有文件，且区分文件和文件夹
* `ls -i *data_file`:查看文件或目录的inode编号
### 过滤输出列表 ###
* `ls -l my_script`:指定特定文件的名称作为**过滤器**，该命令只会显示该文件的信息；
* `ls -l my_scr?pt`:问号用于过滤字符串中替代任意位置的**单个字符**
* `ls -l my_s*t`:星号可匹配**零个或多个字符**
* `ls -l my_scr[ai]pt`:中括号表示一个字符位置上并给出多个可能的选择
* `ls -l f[a-i]ll`:中括号也可以指定某个位置上的字符范围
* `ls -l f[!a]ll`:使用感叹号将不需要的内容排除在外

## 处理文件 ##
### 创建文件 ###
* `touch test_one`:创建空文件；此外还可用来改变文件的修改时间，不改变内容
* `touch -a test_one`:改变访问时间
* `ls -l --time=atime test_one`:显示已经更改过的文件访问时间

### 复制文件###
* `cp source destination`:复制命令需要两个参数:源对象和目的对象，
* `cp -i test_one test_two`:如果目标文件已存在，加上`-i`强制询问shell是够覆盖已有文件
* `cp -R Scripts/ Mod_Scripts`:递归地复制整个目录的内容

### 链接文件 ###
如果需要在系统上维护同一个文件的两份或多份副本，除了保存多份单独的物理文件副本之外，还可以采用保存一份物理文件副本和多个虚拟副本的方法。这种虚拟副本就称为链接。链接是目录中指向文件真实位置的占位符。  
	
1. 硬链接是同一文件的不同访问路径，其对应的索引节点是一样的，删除文件其实就是删除其中的一个硬链接，如果该文件对应的硬链接都被删除了该文件才被删除，常用于保护文件； 
2. 符号链接类似于Windows中对应的快捷方式，删除符号链接不影响源文件，删除源文件，则对应的符号链接也没有意义。要为一个文件创建符号链接，源文件也要事先存在。
3. 同一存储媒体只能创建硬链接；在不同存储媒体的文件之间创建链接，只能使用符号链接。  

	
* `ln -s data_file s1-data_file`:给data_file创建符号链接
* `ln code_file h1_code_file`:给code-file创建硬链接
	
### 重命名文件 ###
在Linux中重命名文件称为移动(moving). mv命令可以将文件和目录移动到另一个位置或重新命名。

* `mv fall fzll`:文件fall更改为fzll，inode编号和时间戳保持不变，mv命令只影响文件名。
* `mv fzll Pictures/`:也可以使用mv来移动文件的位置，同样不会改变文件inode编号或时间戳 

和cp命令类似，也可以在mv命令中使用-i参数。这样在命令试图覆盖已有的文件时，就会得到提示。  

* `mv /home/jack/Pictures/fzll /home/jack/fall`:fall移动到了/home/jack,并将名字改为fall，文件的时间戳和inode编号都没变。改变的只有位置和名称。
* `mv Mod_Scripts Old_Scripts`也可以使用mv命令移动整个目录及其内容，目录内容没有变化，只有目录名发生改变。  

### 删除文件 ###
在Linux中，删除(deleting)叫做移除(removing)  

* `rm -i fall`:命令参数-i提示你是不是要真的删除该文件
* `rm -i f?ll`:也可以使用通配符删除成组的文件,别忘了使用-i保护好自己的文件  

rm命令的另一个特性是,如果要删除很多文件且不受提示符的打扰,可以用-f参数强制删除,小心为妙.  

## 处理目录 ##

### 创建目录 ###
* `mkdir New_Dir`:创建一个New_Dir新目录
* `mkdir -p New_Dir/Sub_Dir/Under_Dir`: 同时创建多个目录和子目录

### 删除目录 ###
* `rm -i New_Dir/my_file`:先把目录中的文件删掉
* `rmdir New_Dir`:然后删除空目录
* `rm -ri My_Dir`:使用-r选项使得命令可以向下进入目录,删除其中的文件,然后在删除目录本身
* `rm -rf Small_Dir`:一口气无声无息删除目录及其所有内容的终极大法

## 查看文件内容 ##
### 查看文件类型 ###
在显示文件内容之前,应该先了解一下文件的类型.  

* `file my_file`:不仅能够确定文件中包含的文本信息,还能确定该文件的字符编码
* `file New_Dir`:区分目录的方法
* `file s1_data_file`:file命令能够告诉你链接到哪个文件上 

### 查看整个文件 ###
* `cat test1`:cat命令是显示文本文件中所有数据的得力工具
* `cat -n test1`:-n参数会给所有的行加上行号
* `cat -b test1`:-b参数只给有文本的行加上行号
* `cat -T test1`:如果不想让制表符出现,可以用-T参数
* `more /etc/bashrc.bashrc`:more命令会显示文本文件的内容,但会在显示每页数据之后停下来

### 查看部分文件 ###
* `tail log_file`:默认显示文件的末尾10行
* `tail -n 2 log_file`:加入-n参数来修改所显示的行数,这里显示末两行
* `head log_file`:默认显示文件前10行的文本
* `head -n 5 log_file`:显示前5行


































