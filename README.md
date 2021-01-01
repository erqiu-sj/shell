<!--
 * @Author: 邱狮杰
 * @Date: 2020-12-31 23:40:13
 * @LastEditTime: 2021-01-01 10:35:04
 * @FilePath: /shell/src/README.md
 * @Description: 描述
-->

# Shell

## 普通变量

- 赋值 `变量=值` 不可有空格

- 撤销变量=删除变量 `unset 变量名`

- 声明静态变量(只读变量),注意：不能`unset`该变量 `readonly`，

- 变量名称和 `javascript` 相似

- 环境变量名建议大写

- 在 `bash` 中所有变量默认类型都是字符类型，默认不能进行数字运算

- 定义的变量只能在该文件中应用属于局部变量，除非使用 `export 变量名`将变量作用域设为全局

## 特殊变量

- `$n`
  > `n` 为数字 `$0`表示该脚本名称 `$1~9`表示第一个到第九个参数，十以上的参数，需要加上大括号，比如：`${10}`

```shell
# sh ./index.sh 11 22 33
echo "$0 $1 $2"
# echo的结果 index.sh 11 22 33
```

- `$#` 返回输入的参数个数

```shell
#sh ./index.sh 1 2 3 4
echo "$#"
# result: 4
```

- `$*` 将命令行中所有的参数看作一个整体 输出结果与`$n`类似

- `$@` 将命令行中所有参数单独对待 输出结果与`$n`类似

- `$?` 最后一次命令执行的返回状态，如果这个变量的返回值是 0，证明上一条命令正确执行，如果非 0(具体的值由程序决定),则上一条命令执行不正确

## 运算符

_基本语法_

```shell
# $((operator)) or $[operator] operator运算符

# expr +,-,\*,/,% 加减乘除,取模

expr 1 + 2

# 3

expr `expr 2 + 3` \* 4

# 20

s=$[(2+3)*4]

echo $s

# 20
```

## 条件判断

`condition` 注意：⚠️ 前后都需要空格
注意：非空即为 `true`

```shell
[ content ] #true
[] #false
```

### 常用判断

- `=` 字符串比较

> 整数比较

- `-lt`小于
- `-le`小于等于
- `eq`等于
- `gt`大于
- `ge`大于等于
- `ne`不等于

> 文件权限

- `-r` 只读权限
- `-w` 可写权限
- `-x` 可执行权限

> 文件类型判断

- `-f` 文件存在并且只是一个常规文件
- `-e` 文件存在
- `-d` 文件存在并是一个目录

> 多条件判断

```shell
# 与javascript类似
[ 1 -eq 1 ] && echo ok || echo no
# ok
```

## 分支

- `if` `then` `elif` `fi `

```shell
# sh index.sh 1
if [ $1 -eq 1 ];then
echo "1"
elif [ $1 -eq 2 ];then
echo "2"
fi
# 1
```

- `case`

```shell

case $变量名 in
1)
# 执行
;;# ;;表示break
*) #*）表示default
#执行
esac
```

- `for`

```shell
s=0
for((i=0;i<100;i++))
do
s=$[$s+$i]
done
echo $s
# 4950
# sh index.sh one two three
for i in $* # 如果将'$*'起来参数将会变为一个整体，而 $@不会
do
echo "i like $i"
done
# i like one
# i like two
# i like three
```

- `while` `do` `done`

```shell
s=0
while [ $s -le 100  ]
do
s=$[$s + 1]
done
echo "我循环完了 $s"
# 我循环完了 101
```

## read 读取控制台输入

`read`(option)(params)

- option:

  -p:指定读取值时的提示符

  -t:指定读取值时等待的时间 单位：秒

- params:

  变量：指定读取值时的变量

```shell
read -t 5 -p "your name?" Name
echo $Name
# 如果超过五秒没有输入则会退出程序，如果输入Name 则会echo出来

```
