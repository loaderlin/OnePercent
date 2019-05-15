# IDEA

## 快捷键

Ctrl+F12 查看file，method结构图、类继承机构图

Ctrl+Shift+Alt+U 查看Maven依赖，类图

Ctrl+E 定位到最近浏览过的文件

Ctrl+H 显示类结构图（类的继承层次）

Ctrl+D 复制上一行

Alt+1  快速打开或隐藏工程面板

Ctrl+Shift+Up/Down 向上/下移动语句

Ctrl+Shift+N 全局搜索文件名

Ctrl+Shift+R 全局搜索

Shift+F6 重命名
所有的文件，类名，函数名，属性名都可以重命名，
值得点赞的是，只要你使用Shift+F6重命名，所有使用过这个名称的地方都会跟着改变；

Ctrl+Alt+L 代码美观又符合规范；

A. 按【鼠标中键】快速打开智能提示，取代alt+enter 。

File->Settings-> Keymap-> 搜索 Show Intention Actions -> 添加快捷键为鼠标中键。

B. 按【F2】快速修改文件名，告别双手操作。

File->Settings-> Keymap-> 搜索 Rename -> 将快捷键设置为F2 。

C. 按【F3】直接打开文件所在目录，浏览一步到位。

File->Settings-> Keymap-> 搜索 Show In Explorer -> 将快捷键设置为F3 。

## 当前配置项 VS 默认配置项

### 默认配置

顶部导航栏 > File > Other Settings > Default Settings/ProjectStructs

### 当前配置项

顶部导航栏 > File > Settings

- 全局JDK（默认配置）

顶部工具栏  File > Other Settins > Default Project Structure > SDKs > JDK

- 全局Maven（默认配置）

顶部工具栏  File >Other Settings > Default Settings > Build, Execution, Deployment > Build  Tools > Maven

- 自动导包和智能移除 （默认配置）

顶部工具栏  File ->Other Settings -> Default Settings -> Auto Import

勾选

Add unambiguous imports on the fly 自动导入依赖  

Optimize imports on the fly (for current project)   优化导入和智能删除无关依赖

## 使用场景

### 神奇的Inject Lanuage

如果使用IDEA在编写JSON字符串的时候，要一个一个\去转义双引号。

使用Inject Language帮我们自动转义双引号

```java
String jsonString = "";
```

1. 先将焦点定位到双引号里面，使用alt+enter快捷键弹出Inject Language 视图，并选中

2. 选择后，切记，要直接按下enter回车键，才能弹出Inject Language列表。在列表中选择json组件

3. 选择完后。鼠标焦点自动会定位在双引号里面，这个时候你再使用alt+enter就可以看到

4. 选中Edit JSON Fragment并回车，就可以看到编辑JSON文件的视图

5. 关闭可以使用Ctrl+F4

### 行尾加分号

```java
String s = "test";
if (s == null)
```

这段代码，我们还需要为if语句加上大括号才能编辑通过，这个时候你直接输入Ctrl+Shift+Enter，IDEA会自动帮你收尾，加上大括号的。

### 批量修改

```java
HashMap map = new HashMap();
map.put("goodsCategoryId", "49CE2DD4CBD9EDF0E050AA0A1B2B1CC1");
map.put("name", "生化危机-终章2");
map.put("price", "36.8");
map.put("content", "南国影视城，周六18：30");
```

1. 使用Ctrl+W选中map这个文本

2. 依次使用5次Alt+J快捷键，逐个选中，这样五个文本就都被选中并高亮起来了。

参考链接

[Intellij IDEA神器居然还有这些小技巧](https://blog.csdn.net/linsongbin1/article/details/80211919)