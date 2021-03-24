# awk
语法：

awk [options] pattern {action} filename

pattern和action都是可选的，如果没有pattern，则action应用到全部记录，如果没有action，则输出匹配的记录

pattern可选以下任意一种：

- /正则表达式/
- 条件表达式
- 模式匹配表达式
- 模式（指定一个行的范围）
- BEGIN，读取记录之前执行的动作
- END，读取所有记录之后执行的动作


for,while,if,do语句都与C语言相似， for还有一种形式： for (index in array)
赋值运算也与C语言相似， += 、-=等等
三目运算也与语言相似
关系操作符也与C语言相似，不同点在：
    ~ ： 前面的字符串是否匹配后面的正则表达式，只能用在 { awk命令 } 前面
   !~ ： 与~相反 

数组的下标可以是数字，也可以是字符串，如果是数字，则从1开始。

print不加参数默认就是print $0


选项：
        -F sepstring ：以sepstring作为分隔符。sepstring被视为正则表达式。默认分隔符是空白符。
        -f progfile：  从progfile文件中读取awk脚本执行
        -v var=value 定义一个变量


内置变量：
$n	当前记录的第n个字段，字段间由FS分隔
$0	当前记录
$NF 当前记录的最后一个字段 ， $(NF-1) 表示倒数第二个字段，以此类推
ARGC	命令行参数的数目
ARGIND	命令行中当前文件的位置(从0开始算)
ARGV	包含命令行参数的数组
CONVFMT	数字转换格式(默认值为%.6g)ENVIRON环境变量关联数组
ERRNO	最后一个系统错误的描述
FIELDWIDTHS	字段宽度列表(用空格键分隔)
FILENAME	当前文件名
FNR	各文件分别计数的行号
FS	字段分隔符(默认是空白符)
IGNORECASE	如果为真，则进行忽略大小写的匹配
NF	一条记录的字段的数目
NR	已经读出的记录数，就是行号，从1开始
OFMT	数字的输出格式(默认值是%.6g)
OFS	输出记录分隔符（输出换行符），输出时用指定的符号代替换行符
ORS	输出记录分隔符(默认值是一个换行符)
RSTART	由match函数所匹配的字符串的第一个位置
RLENGTH	由match函数所匹配的字符串的长度
RS	记录分隔符(默认是一个换行符)
SUBSEP	数组下标分隔符(默认值是/034)


内置函数：
字符串处理：
sub(regex, string, target)  :  对当target中匹配中正则表达式regex的内容使用字符串string进行替换， 只替换第一次命中的位置。如果没有指定targe就使用整个记录
gsub(regex, string, target) : 与sub类似，但替换所有命中的位置 
index(string, substring) : 返回子字符串substring和字符串string中匹配中的起始位置，从1开始
substr(string, start, len) : 截取子串， 从start开始，长度为len。如果没有指定len, 则返回从start到结尾的位置
split(string, array, separator) : 使用分隔符separator对字符串进行分隔，结果存放进数组array，如果没有指定分隔符，则使用FS.
length(string) : 返回字符串string的长度，如果没有指定string，则使用当前记录。
match(string, regex) : 使用正则表达式对字符串string进行匹配，返回匹配中的位置，如果没有匹配中返回0。同时刚RSTART设置为匹配中的位置，RLENGTH设置为匹配中的长度
toupper(string) : 将字符串string转成大写
tolower(string) : 将字符串string转成小写

算术函数：
int(x) : 返回x的整数部分
sqrt(x) : 返回x的平方根
rand() : 返回一个0到1之前的随机数

printf() : 与C语言中的printf函数类似


自定义函数：
function name(var1, var2, ...) {

}