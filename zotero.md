# Zetero

如果对整理文献有需求，那就用zetero吧。

## 开始使用

安装zotero和浏览器插件

本文使用的版本为6.7.143

## bibtex格式参考文献导出

zetero默认导出biblatex格式形如zhangsan_sixing_2024

google学术默认bibtex格式：zhangsan2024sixing

我选择后者

zetero安装[zotero-better-bibtex](https://github.com/retorquere/zotero-better-bibtex)，需要到官网上下载，手动安装

然后将`引用格式公式`设置为`[auth:lower][year][shorttitle_1_0:lower]`。更改后需要右键已有文献`刷新bibtex引用`后才会更新Citation key。

这样就可以得到与google学术相似的pattern，但依然有差别。除了根据你文献内容可能会多出一些内容，而且出版商也有可能不同等等。最重要的是，引用名有时不同。

比如一个以`A high-order `开头的文献，better bibtex导出与google学术不同如下：

better bibtex：auth+year+highorder

google学术：auth+year+high

参考[Citation Keys](https://retorque.re/zotero-better-bibtex/citing/index.html)获得更多语法信息。