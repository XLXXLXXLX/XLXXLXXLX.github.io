为了克服使用shell脚本“每次用到每次还要再查”的现状，尝试做一些记录，虽然还是参考[菜鸟教程](https://www.runoob.com/linux/linux-shell-process-control.html)（）

### 流程控制

下文中的condition是`[ ... ]`或者`(( ... ))`的格式，前者需要使用`-lt`等比较方法，而后者可以使用`>`、`<`等比较符

- if语句：

```shell
if condition
then
    command1 
    command2
    commandN 
fi
#或者
if condition; then; command1; command2; fi
```

- for循环：

```sh
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done

#或者
for var in item1 item2 ... itemN; do command1; command2… done;
```

- while语句：

```sh
while condition
do
    command
done
#或者
while condition; do command; done;
```

- case ... esac 多选择语句

```sh
case 值 in
模式1)
    command1
    command2
    ...
    commandN
    ;;
模式2)
    command1
    command2
    ...
    commandN
    ;;
esac
#例如
echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    4)  echo '你选择了 4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```





### Shell函数

下面是shell函数的一般格式（\[ \]内部的可以省略）

```sh
# 函数定义
[ function ] funname [()]
{
    action;
    [return int;]
}
# 函数调用
funnname
```



| 参数处理 | 说明                              |
| ---- | ------------------------------- |
| $#   | 传递到脚本或函数的参数个数                   |
| $*   | 以一个单字符串显示所有向脚本传递的参数             |
| $$   | 脚本运行的当前进程ID号                    |
| $!   | 后台运行的最后一个进程的ID号                 |
| $@   | 与$*相同，但是使用时加引号，并在引号中返回每个参数。     |
| $-   | 显示Shell使用的当前选项，与set命令功能相同。      |
| $?   | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。 |
