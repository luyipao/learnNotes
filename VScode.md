# VScode

### Makefile

安装minGW后依然

> make : 无法将“make”项识别为 cmdlet、函数、脚本文件或可运行程序的名称。请检查名称的拼写，如果包括路径，请确保路径正确 ，然后再试一次

将minGW/bin/mingw32-make.exe文件改为make.exe

## 界面

ctrl+shift+e打开文件界面

按住终端名称拖动可以移动终端位置。

## 命令

`Measure-Command`记录运行时长

跳转到上个光标位置`alt`+`-`，跳转到下个光标位置`alt`+`+`

左右括号之间跳转：`ctrl`+`shift`+`\`

### c++clang-format

{ BasedOnStyle: Google, AfterControlStatement：false, AccessModifierOffset: 0, AlignArrayOfStructures: AIAS_Right, ColumnLimit: 0}

`alt`+`~`:调出当前文件所在目录

`alt`+`z`：自动换行