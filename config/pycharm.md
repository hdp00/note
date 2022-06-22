[TOC]

### 代码提示，不区分大小写
```
Settings->Editor->Gereral->Code Completion->Match case
```

### 忽略PEP8代码风格警告信息
将鼠标移到提示的地方，按alt+Enter，选择忽略（Ignore）这个错误即好。

### PyQt5
```
Tools->External Tools
需要添加designer，pyuic5，pyrcc5
pyuic5 of Arguments：$FileName$ -o ui_$FileNameWithoutExtension$.py 
pyrcc5 of Arguments: $FileName$ -o rs_$FileNameWithoutExtension$.py
Working Directory均设为$FileDir$
```