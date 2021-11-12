# cut

cut的工作就是“剪”，具体的说就是在文件中负责剪切数据用的。cut 命令从文件的每一行剪切字节、字符和字段并将这些字节、字符和字段输出。

1）基本用法

cut [选项参数]  filename

说明：默认分隔符是制表符

2）选项参数说明

| 选项参数 | 功能                         |
| -------- | ---------------------------- |
| -f       | 列号，提取第几列             |
| -d       | 分隔符，按照指定分隔符分割列 |
| -c       | 指定具体的字符               |

3）案例实操

（1）数据准备

```bash
[atguigu@hadoop101 datas]$ touch cut.txt
[atguigu@hadoop101 datas]$ vim cut.txt
dong shen
guan zhen
wo  wo
lai  lai
le  le
```

（2）切割cut.txt第一列

```bash
[atguigu@hadoop101 datas]$ cut -d " " -f 1 cut.txt
dong
guan
wo
lai
le
```

（3）切割cut.txt第二、三列

```bash
[atguigu@hadoop101 datas]$ cut -d " " -f 2,3 cut.txt 
shen
zhen
wo
lai
le
```

（4）在cut.txt文件中切割出guan

```bash
[atguigu@hadoop101 datas]$ cat cut.txt | grep "guan" | cut -d " " -f 1
guan
```

（5）选取系统PATH变量值，第2个“：”开始后的所有路径：

```bash
[atguigu@hadoop101 datas]$ echo $PATH
/usr/lib64/qt-3.3/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/atguigu/bin

[atguigu@hadoop102 datas]$ echo $PATH | cut -d : -f 2-
/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/atguigu/bin
```

（6）切割ifconfig 后打印的IP地址

```bash
[atguigu@hadoop101 datas]$ ifconfig ens33 | grep netmask | cut -d "n" -f 2 | cut -d " " -f 2
192.168.1.102
```



p.s. awk 可以替代 cut

# awk

一个强大的文本分析工具，把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行分析处理。

**1**）基本用法

`awk [选项参数] ‘pattern1{action1} pattern2{action2}...’ filename`

pattern：表示AWK在数据中查找的内容，就是匹配模式

action：在找到匹配内容时所执行的一系列命令

**2**）选项参数说明

| 选项参数 | 功能                 |
| -------- | -------------------- |
| -F       | 指定输入文件折分隔符 |
| -v       | 赋值一个用户定义变量 |

**3**）案例实操

（1）数据准备

`[atguigu@hadoop102 datas]$ sudo cp /etc/passwd ./`

（2）搜索passwd文件以root关键字开头的所有行，并输出该行的第7列。

`[atguigu@hadoop102 datas]$ awk -F : '/^root/{print $7}' passwd `

`/bin/bash`

（3）搜索passwd文件以root关键字开头的所有行，并输出该行的第1列和第7列，中间以“，”号分割。

`[atguigu@hadoop102 datas]$ awk -F : '/^root/{print $1","$7}' passwd `

`root,/bin/bash`

注意：只有匹配了pattern的行才会执行action

（4）只显示/etc/passwd的第一列和第七列，以逗号分割，且在所有行前面添加列名user，shell在最后一行添加"dahaige，/bin/zuishuai"。

```bash
[atguigu@hadoop102 datas]$ awk -F : 'BEGIN{print "user, shell"} {print $1","$7} END{print "dahaige,/bin/zuishuai"}' passwd
user, shell
root,/bin/bash
bin,/sbin/nologin
。。。
atguigu,/bin/bash
dahaige,/bin/zuishuai
```



注意：BEGIN 在所有数据读取行之前执行；END 在所有数据执行之后执行。

（5）将passwd文件中的用户id增加数值1并输出

```bash
[atguigu@hadoop102 datas]$ awk -v i=1 -F: '{print $3+i} ' passwd
1
2
3
4
```

**4**）awk的内置变量

| 变量     | 说明                                   |
| -------- | -------------------------------------- |
| FILENAME | 文件名                                 |
| NR       | 已读的记录数                           |
| NF       | 浏览记录的域的个数（切割后，列的个数） |

**5**）案例实操

（1）统计passwd文件名，每行的行号，每行的列数

```bash
[atguigu@hadoop102 datas]$ awk -F: '{print "filename:"  FILENAME ", linenumber:" NR  ",columns:" NF}' passwd 
filename:passwd, linenumber:1,columns:7
filename:passwd, linenumber:2,columns:7
filename:passwd, linenumber:3,columns:7
```

（2）切割IP

`[atguigu@hadoop102 datas]$ ifconfig ens33 | grep netmask | awk -F " " '{print $2}'`

`192.168.1.102`

（3）查询sed.txt中空行所在的行号

`[atguigu@hadoop102 datas]$ awk '/^$/{print NR}' sed.txt `

`5`

