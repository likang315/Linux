### Shell 命令

------

[TOC]

##### 01：export 命令

- 用于将变量导出到子Shell进程中。当在父Shell中使用`export`命令时，**该变量将成为子Shell的环境变量**，并且在子Shell中可以使用。

- ```
  export [-fnp] [name[=value]]
  ```

  - `name`和`value`是要导出的变量名和值；
  - `value` 添加引号和不添加效果都一样；
  - `:` 变量值冒号并列作用；

- 当在Shell脚本中使用`export`命令时，**导出的变量只在脚本执行期间存在**，并在脚本执行完毕后被删除。如果要在Shell会话中永久导出变量，可以**将`export`命令添加到Shell配置文件**（如`.bashrc`或`.bash_profile`）中。

###### 可选参数

- `-f`：选项表示将函数导出为子Shell的环境变量。
- `-n`：选项表示将变量取消导出，从而从子Shell的环境中删除该变量。
- `-p`： 选项表示列出所有导出的变量。

##### 02：alias 命令

- 在Shell中，alias是一种命令别名的定义方式，用于将一个命令或一组命令的名称替换为另一个名称。

- 通过使用alias命令，用户可以方便地定义自己的命令别名，以提高Shell使用效率和方便性

- ```shell
  alias new_command='old_command'
  ```

##### 03：source 命令

- 用于执行指定的Shell脚本，并**将其中的命令和变量添加到当前Shell环境中**，使得这些命令和变量可以在当前Shell会话中直接使用。

- 与直接执行Shell脚本不同，使用source命令执行Shell脚本**不会启动一个新的Shell进程**，而是在当前Shell进程中执行脚本。这意味着，脚本中定义的变量和函数可以直接在当前Shell会话中使用，而不需要将其导出到子进程中。

- source命令也可以使用"."符号代替，**即"." filename**。这两种语法是等价的。

- ```shell
  source filename
  ```

##### 04：profile 文件

- `profile`文件是一种shell脚本，通常是用于初始化和配置用户的Shell环境的文件。
- `profile`文件通常位于用户主目录下，例如在bash shell中，`.bash_profile`文件是在用户登录时执行的脚本。这个文件包含可以**设置环境变量、别名、PATH等的命令，以及其他一些用户自定义的命令**。