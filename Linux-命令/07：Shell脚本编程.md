### Shell 脚本编程

------

Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务

##### 1：Shelll环境

- Bourne Shell（/usr/bin/sh或/bin/sh）
- Bourne Again Shell（/bin/bash）
- 在一般情况下，人们并不区分 Bourne Shell 和 Bourne Again Shell，所以，像 **#!/bin/sh**，它同样也可以改为 **#!/bin/bash**。
  - **#!** 告诉系统其后路径所指定的程序即是使用那种解释器解释该脚本文件。
  - bash：**命令行解释器**；

##### 2：运行 Shell 脚本有两种方法：

1. 作为可执行程序

   - 将上面的代码保存为 test.sh，并 cd 到相应目录：

   - 注意

     - 一定要写成 **./test.sh**，而不是 **test.sh**，运行其它二进制的程序也一样，直接写 test.sh，linux 系统会去 PATH 里寻找有没有叫 test.sh 的，而只有 /bin, /sbin, /usr/bin，/usr/sbin 等在 PATH 里，你的当前目录通常不在 PATH 里，所以写成 test.sh 是会找不到命令的，要用 ./test.sh 告诉系统说，就在当前目录找。

   - ```shell
     # 使脚本具有执行权限
     chmod 755 ./test.sh
     # 执行脚本
     ./test.sh
     ```

2. 作为解释器参数

- 这种运行方式是，直接运行解释器，其参数就是 shell 脚本的文件名，如：

```shell
/bin/sh test.sh
```

##### 3：定义变量

- 变量的命名

  - 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
  - your_name="com"

- 变量的赋值

  - 显式地直接赋值，还可以用语句给变量赋值
  - for file in `ls /etc` 或 for file in $(ls /etc)
    - 将 /etc 下目录的文件名循环出来

- 使用变量

  - ```shell
    your_name="qinjx"
    echo $your_name
    echo ${your_name}
    # 变量名外面的花括号是可选的，加不加都行，加花括号是为了帮助解释器识别变量的边界，推荐所有的都加上
    echo "My name is ${skill}haha"
    ```

- 已定义的变量，可以被重新定义

- 只读变量

  - 使用 readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变。尝试改变会报错；

  ```shell
  #!/bin/bash
  myUrl="https://www.google.com"
  readonly myUrl
  ```

- 删除变量

  - 使用 unset 命令可以删除变量，变量被删除后不能再次使用。unset 命令不能删除只读变量。

  ```shell
  unset variable_name
  ```

- 变量类型【三种变量】

  1. **局部变量**：局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
  2. **环境变量**：所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
  3. **shell变量**：shell变量是由shell程序设置的特殊变量。

##### 4：Shell 字符串

- 字符串可以用单引号，也可以用双引号，也可以不用引号；

- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；

- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

  - ```shell
    your_name='runoob'
    # 拼接字符串
    str="Hello, I know you are \"$your_name\"! \n"
    echo  ${str}
    ```

- ###### 获取字符串长度

  ```shell
  string="abcd"
  echo ${#string} #输出 4
  ```

- ###### 提取子字符串

  - 第一个字符的索引值为 **0**。

  ```shell
  # 从字符串第1个字符开始截取4个字符：
  string="runoob is a great site"
  echo ${string:1:4} # 输出 unoo
  ```

- ###### 查找子字符串

  - 查找字符 **i** 或 **o** 的位置(哪个字母先出现就计算哪个)：

  ```
  string="runoob is a great site"
  echo `expr index "$string" io`  # 输出 4，反引号
  ```

##### 5：Shell 数组

- ###### 定义数组

  - 在 Shell 中，用括号来表示数组，数组元素用"空格"符号分割开。定义数组的一般形式为：

  - 数组名=(值1 值2 ... 值n)

  - ```shell
    # 分别定义每个变量
    array_name[0]=value0
    array_name[1]=value1
    array_name[n]=valuen
    ```

- ###### 读取数组

- ```shell
  # ${数组名[下标]}
  valuen=${array_name[n]}
  ```

- 使用 **@** 符号可以获取数组中的所有元素

  ```
  echo ${array_name[@]}
  ```

- ###### 获取数组的长度

  ```
  # 取得数组元素的个数
  length=${#array_name[@]}
  ```

##### 6：Shell 注释

- 单行注释：以 **#** 开头的行就是注释，会被解释器忽略

- 多行注释

  - ```shell
    :<<!
    注释内容...
    注释内容...
    注释内容...
    !
    ```

##### 7：Shell 传递参数

- 可以在执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为：**$n**。**n** 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……
- $# ：传递到脚本的参数个数；
- $* ：以一个单字符串显示所有向脚本传递的参数；"1 2 3"
- $@ ：把传递的参数以每个参数的形式输出 "1" "2" "3"（传递了三个参数）

##### 8：Shell 运算符

- 原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用。

- 表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2，这与我们熟悉的大多数编程语言不一样。

- 完整的表达式要被 ` 包含，注意这个字符不是常用的单引号，反引号。

- ###### 算数运算符

  | 运算符 | 说明                                          | 举例                          |
  | :----- | :-------------------------------------------- | :---------------------------- |
  | +      | 加法                                          | `expr $a + $b` 结果为 30。    |
  | -      | 减法                                          | `expr $a - $b` 结果为 -10。   |
  | *      | 乘法，前边必须加反斜杠(\)才能实现             | `expr $a \* $b` 结果为  200。 |
  | /      | 除法                                          | `expr $b / $a` 结果为 2。     |
  | %      | 取余                                          | `expr $b % $a` 结果为 0。     |
  | =      | 赋值                                          | a=$b 将把变量 b 的值赋给 a。  |
  | ==     | 相等。用于比较两个数字，相同则返回 true。     | [ $a == $b ] 返回 false。     |
  | !=     | 不相等。用于比较两个数字，不相同则返回 true。 | [ $a != $b ] 返回 true。      |

- ###### 关系运算符

- | 运算符 | 说明                                                  | 举例                       |
  | :----- | ----------------------------------------------------- | :------------------------- |
  | -eq    | 检测两个数是否相等，相等返回 true。                   | [ $a -eq $b ] 返回 false。 |
  | -ne    | 检测两个数是否不相等，不相等返回 true。               | [ $a -ne $b ] 返回 true。  |
  | -gt    | 检测左边的数是否大于右边的，如果是，则返回 true。     | [ $a -gt $b ] 返回 false。 |
  | -lt    | 检测左边的数是否小于右边的，如果是，则返回 true。     | [ $a -lt $b ] 返回 true。  |
  | -ge    | 检测左边的数是否大于等于右边的，如果是，则返回 true。 | [ $a -ge $b ] 返回 false。 |
  | -le    | 检测左边的数是否小于等于右边的，如果是，则返回 true。 | [ $a -le $b ] 返回 true。  |
  - ```shell
    # 注意空格
    if [ $a -eq $b ]
    then
       echo "$a -ne $b: a 不等于 b"
    else
       echo "$a -ne $b : a 等于 b"
    fi
    ```

- ###### 布尔运算符

  | 运算符   | 说明                                                | 举例                                     |
  | :------- | :-------------------------------------------------- | :--------------------------------------- |
  | !        | 非运算，表达式为 true 则返回 false，否则返回 true。 | [ ! false ] 返回 true。                  |
  | -o、&&   | 或运算，有一个表达式为 true 则返回 true。           | [ $a -lt 20 -o $b -gt 100 ] 返回 true。  |
  | -a、\|\| | 与运算，两个表达式都为 true 才返回 true。           | [ $a -lt 20 -a $b -gt 100 ] 返回 false。 |
  - ```shell
    if [ $a -lt 100 -o $b -gt 100 ]
    then
       echo "$a 小于 100 或 $b 大于 100 : 返回 true"
    else
       echo "$a 小于 100 或 $b 大于 100 : 返回 false"
    fi
    ```

- ###### 文件测试运算符

  | 操作符  | 说明                                                         | 举例         |
  | :------ | :----------------------------------------------------------- | :----------- |
  | -f file | 检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。 | [ -f $file ] |
  | -d file | 检测文件是否是目录，如果是，则返回 true。                    | [ -d $file ] |
  | -e file | 检测文件（包括目录）是否存在，如果是，则返回 true。          | [ -e $file ] |
  | -r file | 检测文件是否可读，如果是，则返回 true。                      | [ -r $file ] |
  | -w file | 检测文件是否可写，如果是，则返回 true。                      | [ -w $file ] |
  | -x file | 检测文件是否可执行，如果是，则返回 true。                    | [ -x $file ] |
  | -s file | 检测文件是否为空（文件大小是否大于0），不为空返回 true。     | [ -s $file ] |
  
  ```shell
  if [ -x $file ]
  then
     echo "文件可执行"
  else
   echo "文件不可执行"
  fi
  ```
```

##### 9：Shell test 命令

- 用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试

  ```shell
  if test num = num
  then
      echo '两个字符串相等!'
  else
      echo '两个字符串不相等!'
  fi
```

##### 10：Shell 流程控制

- ###### if else

  ```shell
  if condition
  then
      command1 
      command2
      ...
      commandN
  else
      command
  fi
  
  if [ $(ps -ef | grep -c "ssh") -gt 1 ]; then echo "true"; fi
  ```

- ###### if else if

  ```shell
  if condition1
  then
      command1
  elif condition2 
  then 
      command2
  else
      commandN
  fi
  ```

- ###### for 循环

  - 当变量值在列表里，for循环即执行一次所有命令，使用变量名获取列表中的当前取值

  ```shell
  for var in item1 item2 ... itemN
  do
      command1
      command2
      ...
      commandN
  done
  
  for var in item1 item2 ... itemN; do command1; command2… done;
  
  for loop in ${a[@]};
  do
  	echo $loop
  done
  ```

- ###### while

  - let 命令是 BASH 中用于计算的工具，用于执行一个或多个表达式，变量计算中不需要加上 $ 来表示变量。如果表达式中包含了空格或其他特殊字符，则必须引起来。

  ```shell
  while condition
  do
      command
  done
  
  # 示例
  int=1
  while read var
  do 
  	echo "是的！$var 是一个好网站 ${int}"
  	let "int++"
  done
  ```

- ###### 无限循环

  - for (( ; ; ))

- ##### case

  -  case语句为多选择语句。可以用case语句匹配一个值与一个模式，如果匹配成功，执行相匹配的命令。
  - 取值可以为变量或常数，取值后将检测匹配的每一个模式，一旦模式匹配，则执行完匹配模式相应命令后不再继续其他模式。如果无一匹配模式，使用星号 * 捕获该值，再执行后面的命令。

  ```shell
  case 值 in
  模式1)
      command1
      command2
      ...
      commandN
      # 表示break，跳出多选择语句
      ;;
  模式2）
      command1
      command2
      ...
      commandN
      ;;
  *) 
  		echo "........."
  esac
  ```

- 跳出循环
  - break
  - continue

##### 11：Shell 函数

- 定义函数

- 可以带function fun() 定义，也可以直接fun() 定义，不带任何参数

- 参数返回，可以显示加：return 返回，如果不加，将以最后一条命令运行结果，作为返回值

  ```shell
  [ function ] funname [()] {
      action;
      [return int;]
  }
  ```

- 示例

  ```shell
  funWithReturn() {
      echo "输入第一个数字: "
      read aNum
      echo "输入第二个数字: "
      read anotherNum
      echo "两个数字分别为 $aNum 和 $anotherNum !"
      return $(($aNum+$anotherNum))
  }
  # funWithReturn 参数1 参数二
  funWithReturn
  # 函数返回值在调用该函数后通过 $? 来获得。
  echo "输入的两个数字之和为 $? !"
  ```

##### 12：Shell 输入/输出重定向

| 命令            | 说明                              |
| :-------------- | :-------------------------------- |
| command > file  | 将输出重定向到 file。             |
| command < file  | 将输入重定向到 file。             |
| command >> file | 将输出以追加的方式重定向到 file。 |

- /dev/null

- dev/null 是一个特殊的文件，写入到它的内容都会被丢弃；如果尝试从该文件读取内容，那么什么也读不到。但是 /dev/null 文件非常有用，将命令的输出重定向到它，会起到"禁止输出"的效果。

  ```shell
  # 如果希望执行某个命令，但又不希望在屏幕上显示输出结果，那么可以将输出重定向到 /dev/null
  cat ss.txt > /dev/null
  ```

##### 13：Shell 文件包含

- Shell 也可以包含外部脚本。这样可以很方便的封装一些公用的代码作为一个独立的文件

```shell
. filename   # 注意点号(.)和文件名中间有一空格
或
source filename
```

```shell
# 使用 . 号来引用test1.sh 文件
. ./test1.sh
# 或者使用以下包含文件代码
# source ./test1.sh
echo "地址：$url"
```













