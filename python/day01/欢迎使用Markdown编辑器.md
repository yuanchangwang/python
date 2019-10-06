[TOC]

# 欢迎使用Markdown编辑器

你好！ 这是你第一次使用 **Markdown编辑器** 所展示的欢迎页。如果你想学习如何使用Markdown编辑器, 可以仔细阅读这篇文章，了解一下Markdown的基本语法知识。

## 新的改变

我们对Markdown编辑器进行了一些功能拓展与语法支持，除了标准的Markdown编辑器功能，我们增加了如下几点新功能，帮助你用它写博客：

1. **全新的界面设计** ，将会带来全新的写作体验；
2. 在创作中心设置你喜爱的代码高亮样式，Markdown **将代码片显示选择的高亮样式** 进行展示；
3. 增加了 **图片拖拽** 功能，你可以将本地的图片直接拖拽到编辑区域直接展示；
4. 全新的 **KaTeX数学公式** 语法；
5. 增加了支持**甘特图的mermaid语法[^1]** 功能；
6. 增加了 **多屏幕编辑** Markdown文章功能；
7. 增加了 **焦点写作模式、预览模式、简洁写作模式、左右区域同步滚轮设置** 等功能，功能按钮位于编辑区域与预览区域中间；
8. 增加了 **检查列表** 功能。 [^1]: [mermaid语法说明](https://mermaidjs.github.io/)

## 功能快捷键

撤销：Ctrl/Command + Z 重做：Ctrl/Command + Y 加粗：Ctrl/Command + B 斜体：Ctrl/Command + I 标题：Ctrl/Command + Shift + H 无序列表：Ctrl/Command + Shift + U 有序列表：Ctrl/Command + Shift + O 检查列表：Ctrl/Command + Shift + C 插入代码：Ctrl/Command + Shift + K 插入链接：Ctrl/Command + Shift + L 插入图片：Ctrl/Command + Shift + G 查找：Ctrl/Command + F 替换：Ctrl/Command + G

## 合理的创建标题，有助于目录的生成

直接输入1次#，并按下space后，将生成1级标题。 输入2次#，并按下space后，将生成2级标题。 以此类推，我们支持6级标题。有助于使用`TOC`语法后生成一个完美的目录。

## 如何改变文本的样式

*强调文本* *强调文本*

**加粗文本** **加粗文本**

==标记文本==

~~删除文本~~

> 引用文本

H~~2~~O is是液体。

2^10^ 运算结果是 1024.

## 插入链接与图片

链接: [link](https://mp.csdn.net/).

图片: ![Alt](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hdmF0YXIuY3Nkbi5uZXQvNy83L0IvMV9yYWxmX2h4MTYzY29tLmpwZw)

带尺寸的图片: ![Alt](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hdmF0YXIuY3Nkbi5uZXQvNy83L0IvMV9yYWxmX2h4MTYzY29tLmpwZw =30x30)

居中的图片: ![Alt](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hdmF0YXIuY3Nkbi5uZXQvNy83L0IvMV9yYWxmX2h4MTYzY29tLmpwZw#pic_center)

居中并且带尺寸的图片: ![Alt](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hdmF0YXIuY3Nkbi5uZXQvNy83L0IvMV9yYWxmX2h4MTYzY29tLmpwZw#pic_center =30x30)

当然，我们为了让用户更加便捷，我们增加了图片拖拽功能。

## 如何插入一段漂亮的代码片

去[博客设置](https://mp.csdn.net/configure)页面，选择一款你喜欢的代码片高亮样式，下面展示同样高亮的 `代码片`.

```
// An highlighted block
var foo = 'bar';
```

## 生成一个适合你的列表

- 项目
  - 项目
    - 项目

1. 项目1
2. 项目2
3. 项目3

-  计划任务
-  完成任务

## 创建一个表格

一个简单的表格是这么创建的：

| 项目 | Value |
| ---- | ----- |
| 电脑 | $1600 |
| 手机 | $12   |
| 导管 | $1    |

### 设定内容居中、居左、居右

使用`:---------:`居中 使用`:----------`居左 使用`----------:`居右

| 第一列         | 第二列         | 第三列         |
| -------------- | -------------- | -------------- |
| 第一列文本居中 | 第二列文本居右 | 第三列文本居左 |

### SmartyPants

SmartyPants将ASCII标点字符转换为“智能”印刷标点HTML实体。例如：

| TYPE             | ASCII                           | HTML                          |
| ---------------- | ------------------------------- | ----------------------------- |
| Single backticks | `'Isn't this fun?'`             | 'Isn't this fun?'             |
| Quotes           | `"Isn't this fun?"`             | "Isn't this fun?"             |
| Dashes           | `-- is en-dash, --- is em-dash` | -- is en-dash, --- is em-dash |

## 创建一个自定义列表

Markdown : Text-to-HTML conversion tool

Authors : John : Luke

## 如何创建一个注脚

一个具有注脚的文本。[^2](https://gitee.com/oldboy-python-full-stack-26/19083026021/blob/master/预科/预科day03/注脚的解释)

## 注释也是必不可少的

Markdown将文本转换为 HTML。

*[HTML]: 超文本标记语言

## KaTeX数学公式

您可以使用渲染LaTeX数学表达式 [KaTeX](https://khan.github.io/KaTeX/):

Gamma公式展示 Γ(n)=(n−1)!∀n∈NΓ(n)=(n−1)!∀n∈N 是通过欧拉积分



Γ(z)=∫∞0tz−1e−tdt,.Γ(z)=∫0∞tz−1e−tdt,.



> 你可以找到更多关于的信息 **LaTeX** 数学表达式[here](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference).

## 新的甘特图功能，丰富你的文章

```
gantt
        dateFormat  YYYY-MM-DD
        title Adding GANTT diagram functionality to mermaid
        section 现有任务
        已完成               :done,    des1, 2014-01-06,2014-01-08
        进行中               :active,  des2, 2014-01-09, 3d
        计划一               :         des3, after des2, 5d
        计划二               :         des4, after des3, 5d
```

- 关于 **甘特图** 语法，参考 [这儿](https://mermaidjs.github.io/),

## UML 图表

可以使用UML图表进行渲染。 [Mermaid](https://mermaidjs.github.io/). 例如下面产生的一个序列图：:

```
sequenceDiagram
张三 ->> 李四: 你好！李四, 最近怎么样?
李四-->>王五: 你最近怎么样，王五？
李四--x 张三: 我很好，谢谢!
李四-x 王五: 我很好，谢谢!
Note right of 王五: 李四想了很长时间, 文字太长了<br/>不适合放在一行.

李四-->>张三: 打量着王五...
张三->>王五: 很好... 王五, 你怎么样?
```

这将产生一个流程图。:

```
graph LR
A[长方形] -- 链接 --> B((圆))
A --> C(圆角长方形)
B --> D{菱形}
C --> D
```

- 关于 **Mermaid** 语法，参考 [这儿](https://mermaidjs.github.io/),

## FLowchart流程图

我们依旧会支持flowchart的流程图：

```
flowchat
st=>start: 开始
e=>end: 结束
op=>operation: 我的操作
cond=>condition: 确认？

st->op->cond
cond(yes)->e
cond(no)->op
```

- 关于 **Flowchart流程图** 语法，参考 [这儿](http://adrai.github.io/flowchart.js/).

## 导出与导入

### 导出

如果你想尝试使用此编辑器, 你可以在此篇文章任意编辑。当你完成了一篇文章的写作, 在上方工具栏找到 **文章导出** ，生成一个.md文件或者.html文件进行本地保存。

### 导入

如果你想加载一篇你写过的.md文件，在上方工具栏可以选择导入功能进行对应扩展名的文件导入， 继续你的创作。