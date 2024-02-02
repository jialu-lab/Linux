# Linux 命令速查

## 文件操作

rm: 删除

```
* 通配符,匹配 0 或多个任意字符 eg. rm *txt; rm library*; rm *(删除目录下的所有文件)

? 通配符，匹配单个字符 eg. rm librar?.txt

[] 通配符,匹配一组单个字符 eg. rm library[12].jpg; rm library1[0-2].txt

rm -v 显示删除过程

rm -i 防止删除重要文件

rmdir 删除空目录

rm -Rf 删除文件和非空的目录(操作不当可能损坏重要文件和系统)

```

ls: 列出当前所在目录的文件及文件夹

```
ls /home/bin; ls ~/videos(~ 代表 home 目录)

ls ~/videos/*.wmv; ls ~/videos/*triger*.txt

ls -R/ls --recursive 查看多个子目录的内容 eg. ls -R ~/iso(递归地遍历iso目录,显示iso目录和他的每个子目录的内容)

ls -1 以单独一列显示内容

ls -m 以逗号分隔的列表显示内容

ls -a 查看隐藏的文件和文件夹

ls -F 显示文件类型"(*:可执行文件,/:目录,@:符号链接文件;|:管道,=:套接字,无附加符号:普通文件)"

ls --color 用不同的颜色显示内容(dircolors --print-database)

ls -l 显示权限、所有者等详细信息(l-long)(r:允许读取,w:允许改写,x:允许执行)

结合:ls -lF --color, ls -la

ls -r 以相反的顺序显示列表内容

ls -X 按文件的扩展名排序

ls -t 按日期和时间排序

ls -S 按文件大小进行排序

ls -h 用K、M、G显示文件大小

```

pwd: 显示当前目录的路径

cd: 切换到不同目录

```
cd ~ 切换到home目录

cd - 切换到以前的目录

```
	
touch: 创建新文件

mkdir: 创建新目录

```
mkdir -p downloads/pictures/dog 创建新目录和任何必要的子目录

mkdir -pv downloads/pictures/dogs (-v: --verbose)可以显示mkdir所执行的每一步操作

```
	
cp: 复制文件

```
cp 源文件 目标文件

cp downloads/dog.txt . 把其他目录下的文件复制到当前目录且文件名称也相同(.)

cp downloads/dog.txt pic 把目标文件复制到指定目录(只提供目录名)

cp 与*通配符结合使用

cp -v 显示文件复制过程

cp -i 防止复制时覆盖重要的文件

cp -R 复制目录

cp -a 复制文件到其他目录以作为完整的备份

```

mv: 移动和重命名文件

## 用户操作

su username: 变更到其他用户

```
su user1

whoami: 检验su命令是否成功

su -l user1 变更到其他用户，包括其环境变量

su 变更成root用户

su - 变更成root用户，包括其环境变量

```
	
## 学习命令

man: 查看命令(manual手册)

```
man ls

翻看内容: ⬆ ⬇ f(forward) b(backward) q(quit) /搜索内容enter,shift+n返回

man -k(--apropos)基于命令的功能来搜索命令 eg. man -k list

man -f 基于命令的名称快速查找命令 eg.man -f ls

man -u(--update) 重建命令的man数据库 eg.man -u ls

man [1-8] 读取特定命令的man page

man -t 打印man page eg. man -t ls | lpr -P hp_laserjet(|:管道,-P:lpr中标识相应打印机)

```
	
info

```
info info 学习info命令

```

whereis: 查找命令的可执行文件、源文件和man page的路径

whatis: 读取命令man page的描述,支持正则表达式和通配符

```
eg. whatis -w ls*(使用通配符搜索man数据库)

```
	
apropos: 基于功能查找命令

```
apropos list 在命令后输入一个单词或短语，描述感兴趣的命令的功能，可以使用-w和-r选项进行搜索，-e密切关注某个词或短语

```

which: 找出将要运行的命令的版本

```
whereis -b kword

which kword

```

## 组合命令

;: 连续运行多个命令


&: 只有前面的命令运行成功，，才运行下一个命令


||: 只有前面的命令运行失败，，才运行下一个命令


$(): 命令替换，，将一个命令的输出插入到另一个命令

```
eg. mkdir $(date "+%Y-%m-%d")

```
	
## 输入输出流

|: 管道，将一个命令的输出作为另一个命令的输入

```
eg. ls -l | less

```

`> : 将命令的输出重定向到文件`

```
ls -lF downloads/* > downloads_file.txt(若download_file.txt存在，则覆盖，若不存在，则新建)

防止重定向时覆盖文件: set -o noclobber, >| 代替 > [关闭noclobber: set +o noclobber]

```

`>> : 将命令的输出追加到文件`

```
慎用:如果输成了>，会把文件覆盖掉

```

<: 将文件作为命令的输入

```
通常用echo命令来重复在stdin中输入的内容 eg.echo "Hello World"

echo < downloads_file.txt 让echo命令使用downloads_file.txt文件的内容

```
    
## 查看文件

cat: 查看文件

```
cat file1 file2: 将文件拼接至标准输出设备

cat file1 file2 > file3: 将文件与其他结果拼接

cat -n file1 file2: 拼接文件，并给文件加上行号

```

less file1: 分屏查看文件

```
less键盘操作命令:

    pagedn \ e \ space - 前进一页

    pageup \ b - 后退一页

    return \ e \ j \ ⬇ - 前进一行

    y \ k \ ⬆ - 后退一行

    G \ p - 前进到文件的结尾

    lG - 回到文件的开始

    esc-) \ → - 向右滚动

    esc-( \ ⬅ - 向左滚动

    q - 退出less

less -N file: 显示行号

less的搜索命令：

    /搜索模式

    n: 向前重复搜索

    N: 向后重复搜索

```
head file: 查看文件的前10行内容

```
head file1 file2: 查看多个文件的前10行内容

head -n 数字 file: 查看一个或多个文件的前几行内容(包括空白行和文本行)

head -c 数字\数字k\数字m file: 查看文件前几个字节、几K字节或几M字节的内容

```

tail file: 查看文件的最后10行内容

```
tail file1 file2: 查看多个文件的前10行内容

tail -n 数字 file: 查看一个或多个文件的前几行内容(包括空白行和文本行)

tail -f(--follow): 查看一个文件或多个文件中不断更新的最后几行

    tail -f --pid=PID# terminates after PID dies

```



