# The Missing Semester of Your CS Education 学习笔记

## 第一节 Shell

### Shell 是什么

**Shell**（壳）是用户与操作系统之间的接口，它是一种命令行解释器，可以接收用户输入的命令并将其传递给操作系统执行。Shell 允许用户通过命令行来与操作系统交互，执行各种任务，如文件操作、程序运行、系统管理等。

### Bash

> [Windows 环境下配置 GitBash 环境](https://zhuanlan.zhihu.com/p/418321777)

#### 语法

1. `echo`：用于向终端输出文本或变量的内容。

```bash
echo [选项] [字符串]
```

- 常用选项：
  - `-n`：告诉`echo`命令输出文本后不自动换行(默认输出换行符)。
  - `-e`：启用 转义字符 的解析（默认不进行转义字符的处理）。

2. `cd`：用于改变当前工作目录。

```bash
cd [目录路径]
```

- 示例：
- `cd ..`：切换上一级目录。
- `cd ~`：切换到当前用户的家目录。
- `cd /home/user`：切切换到 `/home/user` 目录。

3. `pwd`：显示当前所在的 工作目录 的完整路径。

```bash
pwd
```

4. `ls`：用于 列出目录内容，显示目录下的文件和子目录。

```bash
ls [选项] [目录]
```

- 示例:
  - `ls`：列出当前目录下的文件和文件夹。
  - `ls -l`：以长格式显示文件详情（包括权限、文件大小、修改时间等）。
  - `ls -a`：列出所有文件，包括隐藏文件（以 `.` 开头的文件）。

5. `mv`：用于 移动文件或目录，或者 重命名文件或目录。

```bash
mv [源路径] [目标路径]
```

- 示例：
  - `mv file.txt /home/user/Documents/`：将 `file.txt` 文件移动到指定目录。
  - `mv oldname.txt newname.txt`：将 `oldname.txt` 重命名为 `newname.txt`。

6. `cp`：用于复制文件或目录。

```bash
cp [选项] [源路径] [目标路径]
```

- 示例：
  - `cp file.txt /home/user/Documents/`：复制 `file.txt` 文件到指定目录。
  - `cp -r /source/dir /target/dir`：递归地复制整个目录（用于复制目录及其内容）。

7. `mkdir`：用于创建新目录。

```bash
mkdir [选项] [目录名称]
```

- 示例：
  - `mkdir newfolder`：在当前目录下创建一个名为 `newfolder` 的新目录。
  - `mkdir -p /home/user/newfolder/subfolder`：递归创建目录，`-p` 选项会在父目录不存在时创建父目录。

8. `cat`：用于 查看文件内容，或者将多个文件的内容连接在一起。

```bash
cat [选项] [文件]
```

- 示例：
  - `cat file.txt`：显示 `file.txt` 的内容。
  - `cat file1.txt file2.txt`：将 `file1.txt` 和 `file2.txt` 的内容合并并输出。
  - `cat > newfile.txt`：将输入内容保存到 `newfile.txt` 文件（按 `Ctrl+D` 结束输入）。

9. `sudo`：使普通用户可以临时获得更高权限来执行一些需要管理员权限的操作，而不需要直接登录为超级用户（root）。

```bash
sudo [命令]
```

#### IO 流

1. **重定向**
   - 使用 > 或 >> 将命令的输出重定向到文件中。
     - `>`：会**覆盖**文件内容（如果文件已存在，文件内容会被清空并写入新内容）。
     - `>>`：会将输出内容**追加**到文件的末尾，不会覆盖文件内容。
   - 使用 < 将文件的内容作为命令的输入。
2. **管道**  
   是将一个命令的 标准输出 直接传递给另一个命令作为 标准输入，而不是通过文件进行中转。管道符号是 `|`。
   - 示例:
     - `ls | sort`：列出当前目录下的文件，并将输出通过管道传递给 sort 命令进行排序。

### 路径导航

Linux 和 Windows 操作系统中，许多操作存在不同。

1. Linux 和 macOS：

   - **使用正斜杠 `/` 作为目录分隔符**  
     示例：`/home/user/Documents/file.txt`
   - **路径是以根目录 `/` 开始的绝对路径**  
     示例：`/home/user/Documents/file.txt`
   - **相对路径则从当前工作目录开始**  
     示例：`./Documents/file.txt` `../file.txt`
   - `/`：根目录，所有文件和目录从根目录开始。
   - `~`：表示当前用户的家目录。  
     例如：`/home/user`。
   - **路径区分大小写**  
     示例：`/home/user` 和 `/home/User` 是不同的路径。
   - **路径中空格需要用反斜杠`\`转义**  
     示例：`/home/user/My\ Documents/file.txt`

2. Windows：

   - **使用反斜杠 `\` 作为目录分隔符**
   - **使用驱动器字母来标识不同的分区或磁盘**  
     示例：`C:\Users\user\Documents\file.txt`
   - **相对路径从当前驱动器开始**  
     示例：`.\Documents\file.txt` `..\file.txt`
   - **反斜杠 `\` 是一个转义字符，所以需要使用两个反斜杠 `\\` 来表示路径**  
     示例：`C:\\Users\\user\\Documents\\file.txt`
   - `C:\Users\` 用于存放用户的个人文件
   - `%USERPROFILE%` 表示当前用户的个人目录
   - **路径不区分大小写**  
     示例：`C:\Users\user` 和 `C:\Users\USER` 是相同的路径
   - 如果路径中包含空格，通常需要将整个路径用双引号括起来  
     示例：`"C:\Program Files\MyApp\file.txt"`

3. 相同点：

- 使用 `.` 表示当前目录，`..` 表示上一级目录

### 课后习题
