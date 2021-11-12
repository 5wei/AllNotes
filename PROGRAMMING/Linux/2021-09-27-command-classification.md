# [Command Classification (Ref. etutorials.org)](http://etutorials.org/Linux+systems/how+linux+works/Appendix+A+Command+Classification/)

## Table A-0: BASH BUILTINS

| 命令      | 说明                                                  |
| --------- | ----------------------------------------------------- |
| :         | 扩展参数列表，执行重定向操作                          |
| .         | 读取并执行指定文件中的命令（在当前 shell 环境中）     |
| alias     | 为指定命令定义一个别名                                |
| bg        | 将作业以后台模式运行                                  |
| bind      | 将键盘序列绑定到一个 readline 函数或宏                |
| break     | 退出 for、while、select 或 until 循环                 |
| builtin   | 执行指定的 shell 内建命令                             |
| caller    | 返回活动子函数调用的上下文                            |
| cd        | 将当前目录切换为指定的目录                            |
| command   | 执行指定的命令，无需进行通常的 shell 查找             |
| compgen   | 为指定单词生成可能的补全匹配                          |
| complete  | 显示指定的单词是如何补全的                            |
| compopt   | 修改指定单词的补全选项                                |
| continue  | 继续执行 for、while、select 或 until 循环的下一次迭代 |
| declare   | 声明一个变量或变量类型。                              |
| dirs      | 显示当前存储目录的列表                                |
| disown    | 从进程作业表中刪除指定的作业                          |
| echo      | 将指定字符串输出到 STDOUT                             |
| enable    | 启用或禁用指定的内建shell命令                         |
| eval      | 将指定的参数拼接成一个命令，然后执行该命令            |
| exec      | 用指定命令替换 shell 进程                             |
| exit      | 强制 shell 以指定的退出状态码退出                     |
| export    | 设置子 shell 进程可用的变量                           |
| fc        | 从历史记录中选择命令列表                              |
| fg        | 将作业以前台模式运行                                  |
| getopts   | 分析指定的位置参数                                    |
| hash      | 查找并记住指定命令的全路径名                          |
| help      | 显示帮助文件                                          |
| history   | 显示命令历史记录                                      |
| jobs      | 列出活动作业                                          |
| kill      | 向指定的进程 ID(PID) 发送一个系统信号                 |
| let       | 计算一个数学表达式中的每个参数                        |
| local     | 在函数中创建一个作用域受限的变量                      |
| logout    | 退出登录 shell                                        |
| mapfile   | 从 STDIN 读取数据行，并将其加入索引数组               |
| popd      | 从目录栈中删除记录                                    |
| printf    | 使用格式化字符串显示文本                              |
| pushd     | 向目录栈添加一个目录                                  |
| pwd       | 显示当前工作目录的路径名                              |
| read      | 从 STDIN 读取一行数据并将其赋给一个变量               |
| readarray | 从 STDIN 读取数据行并将其放入索引数组                 |
| readonly  | 从 STDIN 读取一行数据并将其赋给一个不可修改的变量     |
| return    | 强制函数以某个值退出，这个值可以被调用脚本提取        |
| set       | 设置并显示环境变量的值和 shell 属性                   |
| shift     | 将位置参数依次向下降一个位置                          |
| shopt     | 打开/关闭控制 shell 可选行为的变量值                  |
| source    | 读取并执行指定文件中的命令（在当前 shell 环境中）     |
| suspend   | 暂停 Shell 的执行，直到收到一个 SIGCONT 信号          |
| test      | 基于指定条件返回退出状态码 0 或 1                     |
| times     | 显示累计的用户和系统时间                              |
| trap      | 如果收到了指定的系统信号，执行指定的命令              |
| type      | 显示指定的单词如果作为命令将会如何被解释              |
| typeset   | 声明一个变量或变量类型。                              |
| ulimit    | 为系统用户设置指定的资源的上限                        |
| umask     | 为新建的文件和目录设置默认权限                        |
| unalias   | 刪除指定的别名                                        |
| unset     | 刪除指定的环境变量或 shell 属性                       |
| wait      | 等待指定的进程完成，并返回退出状态码                  |

Ref. [Shell内建命令（内置命令）](http://c.biancheng.net/view/1136.html)

## Table A-1: File Management Commands

| **Command** | **Description**                              |
| ----------- | -------------------------------------------- |
| chgrp       | Changes a file's group                       |
| chmod       | Changes a file's permissions                 |
| chown       | Changes a file's user ownership              |
| cp          | Copies a file                                |
| dd          | Converts and copies                          |
| df          | Displays disk usage statistics               |
| du          | Displays directory space usage               |
| file        | Identifies a file type                       |
| find        | Searches for a file                          |
| ln          | Creates a symbolic or hard link              |
| ls          | Lists files                                  |
| mkdir       | Creates a directory                          |
| mkfifo      | Creates a named pipe                         |
| mknod       | Creates a special file                       |
| mv          | Renames or moves a file                      |
| rm          | Removes a file                               |
| touch       | Creates a file or updates a file's timestamp |

## Table A-2: Text Processing and Scripting Commands

| **Command** | **Description**                                              |
| ----------- | ------------------------------------------------------------ |
| awk         | The awk general-purpose text processing language             |
| basename    | Strips extensions and directories from filenames             |
| cat         | Displays and concatenates files                              |
| cmp         | Compares binary files                                        |
| cut         | Extracts columns of lines                                    |
| diff        | Compares text files                                          |
| dirname     | Extracts the directory from a filename                       |
| echo        | Prints text                                                  |
| ed          | A classic line-based text editor                             |
| egrep       | Extended grep                                                |
| ex          | A newer line-based text editor                               |
| expr        | Evaluates a mathematical expression                          |
| false       | Returns a nonzero exit code                                  |
| fmt         | Breaks long lines and reformats text                         |
| grep        | Searches for lines matching a regular expression             |
| groff       | A multi-purpose typesetting utility                          |
| head        | Displays the first lines of a file                           |
| ispell      | A spelling checker                                           |
| less        | Displays a text file                                         |
| more        | Displays a text file                                         |
| nroff       | Formats roff documents for text display                      |
| patch       | Incorporates changes into files; the opposite of diff        |
| perl        | A general-purpose scripting language                         |
| sed         | A stream editor                                              |
| sort        | Sorts lines in a file                                        |
| split       | Chops a file into pieces                                     |
| tail        | Displays the last lines of a file                            |
| tee         | Duplicates a file stream                                     |
| test        | ([) Checks a condition                                       |
| tr          | Translates (or substitutes) characters                       |
| true        | Returns an exit code of 0 (true)                             |
| uniq        | Removes duplicate adjacent lines                             |
| vi          | A visual full-screen editor                                  |
| wc          | Counts words, lines, and characters in a file                |
| xargs       | Executes a command repeatedly with arguments from the input stream |

## Table A-3: Online Documentation Commands

| **Command** | **Description**                             |
| ----------- | ------------------------------------------- |
| info        | Displays GNU-style documentation            |
| man         | Displays the traditional Unix online manual |

## Table A-4: Process and System Utility Commands

| **Command** | **Description**                                             |
| ----------- | ----------------------------------------------------------- |
| at          | Runs a program at a certain time                            |
| chfn        | Changes finger information                                  |
| chsh        | Changes shells                                              |
| crontab     | Runs a periodic job                                         |
| groups      | Shows group membership                                      |
| id          | Shows the current user ID                                   |
| kill        | Sends a signal to a process                                 |
| logger      | Records a message to the system logger                      |
| login       | Allows a user to login                                      |
| lsof        | Lists open files and other information                      |
| mount       | Attaches a filesystem to a directory tree                   |
| newgrp      | Changes the current default group                           |
| nice        | Runs a process with a suggested priority                    |
| passwd      | Changes a password                                          |
| printenv    | Prints environment variables                                |
| ps          | Displays processes                                          |
| renice      | Changes the suggested priority for a process                |
| reset       | Attempts to reset the terminal                              |
| strace      | Traces system calls                                         |
| su          | Switches users                                              |
| sync        | Writes kernel buffers to disk                               |
| time        | Displays how much processor and system time a process takes |
| top         | Shows the processes with the most resource consumption      |
| umount      | Detaches a filesystem from a directory tree                 |

##  Table A-5: System Information Commands

| **Command** | **Description**                                              |
| ----------- | ------------------------------------------------------------ |
| arch        | Displays the system architecture                             |
| df          | Displays disk usage statistics                               |
| dmesg       | Displays buffered kernel messages                            |
| finger      | Displays user information                                    |
| free        | Displays free memory statistics                              |
| hostname    | Displays the current host's name                             |
| last        | Shows the last users who logged in                           |
| tty         | Displays the current terminal name                           |
| uptime      | Displays system load and how long the system has been running |
| vmstat      | Displays virtual memory statistics                           |
| uname       | Displays kernel identification information                   |
| w           | Displays uptime information and current users                |
| who         | Displays current users                                       |
| whoami      | Displays the current user                                    |

##  Table A-6: Archival and Compression Commands

| **Command** | **Description**                                  |
| ----------- | ------------------------------------------------ |
| bunzip2     | A decompression program                          |
| bzip2       | A decompression program                          |
| cpio        | An archival program                              |
| gunzip      | A decompression program                          |
| gzip        | A compression program                            |
| tar         | An archival program                              |
| uncompress  | A decompression program                          |
| unshar      | A de-archival program                            |
| uudecode    | A decoding program (the counterpart of uuencode) |
| uuencode    | Encodes binary file into a text file             |
| zcat        | Decompresses into a file stream                  |

## Table A-7: Miscellaneous Utility Commands

| **Command** | **Description**                                         |
| ----------- | ------------------------------------------------------- |
| bc          | A simple calculator                                     |
| cal         | Shows a calendar                                        |
| date        | Displays the current date                               |
| dc          | Runs the RPN calculator                                 |
| pwd         | Prints the working directory                            |
| script      | Starts a shell where all output is recorded in a file   |
| sleep       | Pauses for a specified number of seconds                |
| strings     | Attempts to show any text embedded in a binary file     |
| yes         | Prints an endless stream of lines                       |
| which       | Displays the first matching program in the current path |

## Table A-8: Development Commands

| **Command** | **Description**                                       |
| ----------- | ----------------------------------------------------- |
| ar          | A library archiver                                    |
| as          | An assembler                                          |
| c++         | A C++ compiler                                        |
| cc          | A C compiler                                          |
| cpp         | A C preprocessor                                      |
| g++         | A C++ compiler (see c++)                              |
| gcc         | A C compiler (see cc)                                 |
| gdb         | The GNU debugger                                      |
| install     | Copies a file into a location with certain parameters |
| ld          | linker                                                |
| ldd         | Displays dynamic libraries                            |
| make        | A package-building tool                               |
| perl        | A general-purpose scripting language                  |

## Table A-9: Shells

| **Command** | **Description**                                              |
| ----------- | ------------------------------------------------------------ |
| bash        | The Bourne Again Shell                                       |
| csh         | The C Shell                                                  |
| exit        | usage: `exit [n]` Cause  the  shell to exit with a status of n. |
| ksh         | The Korn Shell                                               |
| sh          | The Bourne Shell                                             |
| tcsh        | The TC Shell                                                 |