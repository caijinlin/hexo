---
title: Sublime常用快捷键
tags: []
date: 2016-08-12 08:00:00
---

- mac下开启vim模式
sublime => preferences => settings-user
```bash
"ignored_packages"：[],
```

- mac下使用shell以sublime方式打开文件：
```bash
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl
subl filename
```

#### 移动
```shell
h,j,k,l： 左，下，上，右。
w：下一个词的词首。
W：下一个单词(不含标点)。
e：下一个词的词尾。
E：不含标点。
b：上一个词的词首。
B：不含标点。
gg：首。
G： 尾。
```

#### 选择

```shell
ctrl+d：选中下一个相同的
ctrl+command+G：选中所有相同的
ctrl+l：选中整行，继续操作则继续选择下一行，效果和 shift+↓ 效果一样。
ctrl+shift+L 先选中多行，再按下快捷键，会在每行行尾插入光标，即可同时编辑这些行。
shift+↑：向上选中多行。
shift+↓：向下选中多行。
shift+←：向左选中文本。
shift+→：向右选中文本。
```

#### 编辑

```shell
ctrl+delete： 删除
ctrl+shif+D：复制当前行
ctrl+/：注释d当前行，或取消注释
ctrl+J： 向上折行
ctrl+K+U：转换大写
ctrl+K+L： 转换小写
ctrl+K+K：从光标处开始删除代码至行尾。
ctrl+Z： 撤销
ctrl+Y： 恢复撤销
ctrl+Enter 在下一行插入新行。举个栗子：即使光标不在行尾，也能快速向下插入一行。
ctrl+Shift+Enter 在上一行插入新行。举个栗子：即使光标不在行首，也能快速向上插入一行。
ctrl+command+up： 向上移动当前行
ctrl+command+down： 向下移动当前行
shift+home： 选择到页首行头
shift+end： 选择到页尾行
Tab：向右缩进
shfit+tab： 反缩进
```