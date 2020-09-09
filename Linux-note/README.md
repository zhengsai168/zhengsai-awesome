# 初始化文件

```shell
~/.bashrc  #登陆bash的时候默认执行的
~/.vimrc   #vim配置文件
```

# vim配置文件

```shell
位置  ~/.vimrc  支持python
set filetype=python
au BufNewFile,BufRead *.py,*.pyw setf python
set number
set syntax=on
set tabstop=4
set softtabstop=4
set autoindent
set smartindent
set completeopt=preview,menu
set noeb
set shiftwidth=4
set expandtab
inoremap ' ''<ESC>i
inoremap " ""<ESC>i
inoremap ( ()<ESC>i
inoremap [ []<ESC>i
inoremap { {<CR>}<ESC>O
```

# Git

```shell
git add .
git commit -m 'test'
git push


fatal: LF would be replaced by CRLF
git config --global core.autocrlf false
```

# source

```shell
source 或 . 
# 将脚本作为当前进程的一部分运行。
a.sh 如下
export JAVA_HOME=/tmp/jdk
source a.sh #会在运行完a.sh后JAVA_HOME仍然有效
```

# 重定向

```shell
1> 的缩写 为 > 即重定向标准输出
0< 的缩写 为 < 即重定向标准输入
2> 为重定向标准错误
```

# shell脚本

```shell
#!/bin/bash -eu 
# e选项，执行简单命令失败时会退出
# u选项，展开未定义变量时，会报错退出
./test.sh & # 后台执行test.sh
(sleep 5; ./test.sh) & #一起后台
```



# ls    显示文件名  

```Bash
$ ls #显示当前目录文件列表
$ ll #显示详细信息
$ ls a* #显示以a开头的文件
```

# cat  显示文件内容

```Bash
$ cat a.txt #显示文件内容
$ cat a.txt b.txt #多个文件内容拼接后显示
$ cat > a.txt <<EOF #按行输入到a（覆盖），直到EOF
$ cat >> a.txt <<EOF #按行追加到a末尾，知道EOF
```

# rm  删除文件

```shell
$ rm a.txt #删除文件
$ rm -rf ./ #强制删除当前目录所有文件
```

# cp  复制文件

```shell
$ cp a.txt b.txt #复制a到b
$ cp a.txt zs/ #复制a到zs文件夹
```

# scp

```shell
$ scp a.txt app@10.241.241.14:/data/ #复制文件到/data文件夹下
```

# mv  更改文件名/移动文件

```shell
$ rm a.txt b.txt
$ rm a.txt zs/
$ rm a.txt zs/b.txt
```

# grep  查找字符串

```shell
$ grep asd a.txt # 在a中查找asd字符串
$ grep a*d a.txt # 在a中查找a*d正则表达式
```

# head && tail

```shell
$ head a.txt # 显示文件头部
$ tail a.txt # 显示文件尾部
$ head -5 a.txt #显示文件前5行
$ tail -5 a.txt #显示文件后5行
```

# sort

```shell
$ sort a.txt # 将文件按行排序后显示
$ sort a.txt | head -5 #排序后前五行
```

# uniq

```shell
$ uniq a.txt # 忽略重复行显示a
```

# file

```shell
$ file a.txt # 显示文件a的基本信息
```

# script 记录shell会话信息

```shell
$ script
Script started, file is typescript
$ ll | head -3
total 64
drwxr-xr-x   6 app apps    73 May 14 15:53 arch
drwxr-xr-x   3 app apps   153 Sep  2 14:19 eggroll_test
$ exit
$ nano typescript  # 当前目录下产生一个文件记录了会话信息
```

# bzip2  bunzip2 bzcat

```shell
$ bzip2 a.txt # 压缩a 
-k  保留原文件(keep)，-v 显示压缩信息
$ bunzip2 a.txt.bz2 # 解压缩a
$ bzcat a.txt.bz2 #显示压缩文件的内容
$ bzcat a.txt.bz2 | head -4 # 部分内容显示
```

# tar

```shell
$ tar -czvf b.txt.tar.gz b.txt  # 压缩
$ tar -xzvf b.txt.tar.gz  #解压
$ tar -tzvf b.txt.tar.gz  #列出压缩文件列表
```

# which

```shell
$ which python  #查找命令/文件的位置
/data/projects/fate/common/python/venv/bin/python
$ which sh
/usr/bin/sh
```

# whereis

```shell
$ whereis echo #显示所有与命令相关的文件
echo: /usr/bin/echo /usr/share/man/man1/echo.1.gz /usr/share/man/man1p/echo.1p.gz
```

# locate 

```shell
$ locate python #全局搜索路径带python的文件
```

# who w finger

```shell
$ who  # 显示用户信息
supdevUser pts/0        2020-09-09 11:38 (10.241.240.10)
supdevUser pts/1        2020-09-09 11:22 (10.241.240.10)
supdevUser pts/3        2020-09-09 10:12 (10.241.240.10)
$ who am i # 显示自己的信息
$ w # 更详细的用户信息
$ w am i
```

# uptime

```shell
$ uptime
 11:47:19 up 1 day,  1:09,  4 users,  load average: 0.15, 0.19, 0.76
# 当前时间，运行时间，用户数，过去1,5,15分钟平均任务数
```

# free

```Bash
$ free -m # 按MB显示内存情况
$ free -g # 按GB显示内存情况
```

# pwd

显示当前路径

# mkdir

```shell
mkdir zs #创建zs目录
mkdir -p zs/zzs/zsds #创建多级目录
```

# chmod

```shell
$ chmod 777 a.txt  # 文件变更权限
$ chmod 777 -R zs/  # 文件夹权限
```

# 链 && 和||

```shell
$ comd1 && comd2 # 当comd1退出状态为0（真）时，执行2
$ comd1 || comd2 # 当comd2退出状态为1（假）时，执行2
```

# ps

```shell
$ ps # 前台进程？
$ ps -ef # 全部进程
```

# kill

```shell
$ kill 24234 #杀死pid为24234的进程
$ kill -9 24234 #强制杀死pid为24234的进程
$ ps -ef | grep sql  # 查找sql进程
$ kill -9 xxxx
```



11111





