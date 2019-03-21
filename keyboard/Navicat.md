
# 快捷键

Ctrl+D 表的结构设计界面

Ctrl+O 切换回数据内容显示页

Ctrl+Q 表查询（打开查询窗口）

Ctrl+N 新开一个查询窗口

Ctrl+W 关闭当前查询窗口

## 导数据

### 导出/导入Sql文件

#### 导出

打开源数据库，选择全选数据表，点击导出向导

![导出向导](https://raw.githubusercontent.com/loaderlin/OnePercent/master/img/outsqlfile-alltable.png)

选择导出的文件格式

![导出文件格式](https://raw.githubusercontent.com/loaderlin/OnePercent/master/img/outsqlfile-selectfiletype.png)

存放的本地位置

![存放的本地位置](https://raw.githubusercontent.com/loaderlin/OnePercent/master/img/outsqlfile-position.png)

之后就是下一步，最后点击开始就正式导出了

> 但是导出的文件是各个数据表中的数据，而不是一整个数据库的数据

- 使用Python脚本将这些Sql文件合成一个Sql文件

```python
#! /usr/bin/python
# -- coding:UTF-8 --
import os
path = "/home/rocky/sql" #文件夹目录
files= os.listdir(path)  #得到文件夹下的所有文件名称
files.sort()             #排序
s = []
for file in files:       #遍历文件夹
    if not os.path.isdir(file): #判断是否是文件夹，不是文件夹才打开
        f = open(path+"/"+file);#打开文件
        iter_f = iter(f);       #创建迭代器
        str = ""
        for line in iter_f:     #遍历文件，一行行遍历，读取文本
            str = str + line
        s.append(str + '\n')    #每个文件的文本存到list中
# 新的sql文件
with open('gas.sql', 'w+') as fs:
    for line in s:
        fs.write(line)
```

- 直接使用Linux命令行将这些Sql文件合并成一个Sql文件

```sh
cat /home/rocky/sql/* >> gas.sql
```

#### 导入

- 载入

1. 打开目标数据库
2. Ctrl+Q 表查询（打开查询窗口）
3. 点击载入（选择Sql文件，运行）

![载入](https://raw.githubusercontent.com/loaderlin/OnePercent/master/img/infile-onload.png)

>这种方式有个弊端是数据多的话会出现out of memory

- 运行Sql文件

![运行Sql文件](https://raw.githubusercontent.com/loaderlin/OnePercent/master/img/infile-runsqlfile.png)

### 直接使用Navicat的数据传输

[Oracle数据库迁移(从一台服务器迁移到另一台服务器)](https://blog.csdn.net/linfanhehe/article/details/78769651)

#### 参考

[linux文件合并，去重，分割](https://www.cnblogs.com/giraffe/p/3193085.html)

# DBeaver

## DBeaver快捷键

Ctrl + Shift + F 格式化SQL

Alt + X 执行SQL

F3 新建SQL查询

## 设置手动提交

![设置DBeaver手动提交](https://raw.githubusercontent.com/loaderlin/OnePercent/master/img/manual_commit.png)

[
解决Win10快捷键Ctrl+Shift+F的冲突问题](https://blog.csdn.net/qq_34805289/article/details/70344718)