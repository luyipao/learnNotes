# Makefile

.PHONY: *** 可以防止与target同名文件误导make执行.
在makefile文件中定义变量foo 可以用$(foo)代指定义的文件. 然后make foo=***就可以实现对于***文件来处理.
利用cd进入其他文件夹然后&& $(make) target 可以实现调用其他文件夹的make命令