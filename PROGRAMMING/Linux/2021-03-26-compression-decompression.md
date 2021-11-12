# Linux压缩文件及压缩解压缩方式

## gzip 文件

文件形式：*.gz

压缩命令：

```bash
[root@hadoop101 ~]# ls
test.java
[root@hadoop101 ~]# gzip houge.txt
[root@hadoop101 ~]# ls
houge.txt.gz
```



解压缩命令：

```bash
[root@hadoop101 ~]# gunzip houge.txt.gz 
[root@hadoop101 ~]# ls
houge.txt
```



经验技巧：

（1）**只能压缩文件**不能压缩目录

（2）**不保留原来的文件**



## tar 文件

文件形式：*.tar

压缩命令：

```bash
tar -cvf name.tar file1 dir1 #将file1和dir1压缩成tar文件，名为name
```



解压缩命令：

```bash
tar -xvf archive.tar

tar -zxvf name.tar.gz #解压当前路径下名为name的tar.gz文件
tar -zxvf name.tar.gz -C target_dir #解压当前路径下名为name的tar.gz文件到 target_dir
```



经验技巧：

## zip 文件

文件形式：*.zip

压缩命令：

```bash
zip -r name.zip ./name  #将当前路径下的文件夹name压缩成name.zip -r表循环
zip name.zip ./name/* #将当前路径下的文件夹name下的所有文件压缩成name.zip 
```



解压缩命令：

```bash
unzip  name.zip #解压当前路径下名为name的zip文件
```



经验技巧：

zip 压缩命令在window/linux都通用，**可以压缩目录且保留源文件**。



## bz2 文件

文件形式：

压缩命令：

```bash
bzip2 -z name #压缩文件为bz2文件
```



解压缩命令：

```bash
bzip2 -d name.bz2 #解压bz2文件
bunzip2 name.bz2 #解压bz2文件
```



经验技巧：

## tbz 文件

文件形式：

压缩命令：

解压缩命令：

经验技巧：

## tgz 文件

文件形式：

压缩命令：

解压缩命令：

经验技巧：