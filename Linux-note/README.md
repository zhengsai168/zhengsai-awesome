# ls    显示文件名  

```Bash
$ ls #显示当前目录文件列表
$ ll #显示详细信息
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

# mv  更改文件名

```shell
$ rm a.txt b.txt
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







