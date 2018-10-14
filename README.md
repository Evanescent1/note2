# note2
&ensp;&ensp;&ensp;&ensp;egrep    grep   -E(扩展正则表达式）
-o表示匹配到的才显示            basename取基名  birname 取目录名
(([1-9]?[0-9] |1[0-9]{2} |2[0-4][0-9] |25[0-5])\.){3}(([1-9]?[0-9] |1[0-9]{2} |2[0-4][0-9] |25[0-5])\.)
[1-9]?[0-9]表示00-99          '|'这个不是管道符，在扩展正则里表示或           1[0-9]{2}表示100-199
2[0-4][0-9}表示200-249         25[0-5]表示250-255           点前面加\表示转义      {3}表示出现了三次
xxx.xxx.xxx.xxx到x.x.x.x之间的所有数值
&ensp;&ensp;&ensp;&ensp;set list可以检查语法是否错误，有没有看不见的符号
多文件模式用命令可以相互切换
撤销不能退出，否则不能执行
vim只支持基本正则表达式      如果替换  替换的东西不能用正则表达式   只能前面用
vim分成：命令模式     插入模式   扩展命令模式(ex)       可视化模式按v键可以转换
vim默认显示的是命令模式   
模式间的切换：命令切换插入用（i,o,a,I,O,A)返回用ESC键      命令模式切换扩展命令模式用：返回用ESC      大写的R将进入替换模式                 
           大写ZZ可以在命令模式直接保存退出，ZQ是不保存退出         在扩展命令模式用wq保存退出   q!表示不保存退出
在vim模式里以点结束的才算一句话。以空行结束算一段落
-d  可以比较文件的不同
一定要加sh后缀
echo  $PATH查看变量是否有当前目录的路径  脚本需要运行一定要在PATH变量的列表里
如果要想执行脚本，直接写绝对路径或者在当前目录下写相对路径        如果想以后一直执行，把自己的目录加入到PATH目录列表下
只要脚本执行过，执行的路径会存到hash表里，如果把脚本移走，执行脚本的时候只会在hash表里找路径执行，如果文件被移走，它将不执行
alias----内部---  hash表（记录的外部命令路径）-----$PATH
把自己的目录加入到PATH变量的目录下
在 vim    /etc/profile.d/shell.sh建立一个文件shell.sh，要以自己的脚本类型做后缀.sh  
 在里面把PATH变量的目录改成PATH=/data/bin（自己文件的目录名）：$PATH（原来的PATH的目录）一定要加上原来的  改完文件不会立即生效 
   在/etc/profile.d/shell.sh加点让他立即生效
    强制转换就是如果想让数字和字符做运算必须人为的给数字做一下转换，转换成字符串（例如用函数）
linux中shell类型是弱类型，它会自动做转换，无需指定类型例如echo  'abc'10 数字10无需给它做转换，系统默认就做了
小驼峰就是第一个单词字母不大写，后面的字母都大写。大驼峰就所有的字母开头都大写  
数字。字母，下划线都可以做为单词的一部分             
设置好变量之后  用的时候前面加$，否则它认为是字符串    变量引用要加$
如果变量后面要跟字符串，用大括号把变量引起来
如果变量是赋值一段话，需要用引号把这段话引起来
如果是变量定义的是命令，在使用变量的时候，一定要加双引号
把linux存到变量里，用的时候之间$变量就行，相当于别名的效果
变量是临时存放的，注销之后就会消失
var1=chen   var2=$var1   变量一旦确定   就是var2也等于chen   如果var1被重新赋值等于wang,
var2的值不会改变，还是等于chen   变量的值一旦确定，除非重新指定，否则不会改变
默认的shell类型是不能做直接运算的，需要加特殊符号做运算，它只是把你所看到的数字当成字符串来处理
set命令可以看到所设置的变量
所定义的变量如果不用了，要及时删除，否则它会一直占用内存空间。这种情况叫内存泄漏
定义环境变量是先建立一个普通变量。用命令export  name  (name=mage定义的普通） 就能把name变成环境变量   环境变量父子进程都能用
declare  -x  =export   显示系统中所有的环境变量
小括号会开启以个子shell进程在小括号里的变量只是在小括号里有效，一旦执行结束，将恢复以前的变量    小括号里的子进程一样可以用到父进程的变量，不用把它变成环境变量
普通变量用的多，环境变量用的少，主要它的影响范围广
&ensp;&ensp;&ensp;&ensp;只读变量又叫常量：不能修改，设置只读变量用命令readonly     在子shell中设置的变量，只要退出，所设置的变量自动消失  i是数字整数的意思  r就表示常量     declare  -x  显示环境变量  -r显示只读变量
位置变量
$1会把脚本后面跟的ip自动当成$1         想表示$10必须在10上加花括号
脚本中$1 -$10 与脚本后面的1-10的关系是意义对应的 
$0表示脚本名字   $#参数的个数     如果只显示文件名用basename取基名
set --清除它所在位置以后的变量         $*会把上一级所表示的几个变量作为整体传给下个一个脚本      $ @会把几个变量作为单个参数传给下个脚本所需要变量中的一个
$?显示的结果是0表示命令执行成功  1-255表示失败
exit  数字   $1的值可以用exit命令取定义 数字的范围在（0-255）  exit是退出的，命令执行到这里会退出，后面的命令不在执行        
Ping xxx.xxx.x.x  -c   c表示Ping几次ip      /deb/null是垃圾箱    利用&>重定向可以把文件销毁
 当脚本中有exit退出命令的时候不能用点执行脚本，因为它不会开启子SHELL，相当于在当前SHELL类型中退出，就是退出终端        点后面跟配置文件
locate命令搜文件，不是在磁盘搜索，而是在locate库里搜，新创建的文件不会更新到locate的数据库了，需要命令更新数据库（updatedb)     数据库在 /var/lib/mlocate/mlocate.db     用命令搜索文件使用通配符时加上双引号，否则会认为是当前目录
touch  建立文件的数量是有参数限制的     df -i   查节点编号
echo  f{1...523435}  |xards  touch     通过管道  xards命令可以把前面的变成参数   做为touch命令的参数      
包管理工具就是官方提供的二进制，直接用就行了
红帽的rpm包管理器          嵌套定义  自己定义自己
i686表示当前的包运行在什么架构上的32位的
