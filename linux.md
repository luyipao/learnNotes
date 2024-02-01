# linux

不要运行网上的命令，除非你知道具体会发生什么。今天就随便运行了一个命令，结果删除了4G的文件，其中包含texlive-full，等我再想去下载的时候却发现无法下载，缺少依赖。搞了一个下午也没有修好。最后实在没办法就下源码自己编译。

# linux用户常用命令

## 用户管理

### 添加新用户

```
ueradd -d /home/you -m you
```

其中`-d`表示用户主目录，`-m`代表`mkdir`命令，若目录不存在则创建主目录。`you`就是你的用户名。

```
useradd -s /bin/sh -g group –G adm,root gem
```

`-s`表示`shell`，指定用户登录的shell。`-g`即`group`，表示用户所属的用户组。

### 删除用户

```
userdel -r sam
```

把用户的主目录一起删除。

### 用户更改

参数设置类似`useradd`，格式为`usermod options username`。

`usermod -aG sudo YOUR_USER_NAME `

表示将用户添加到`sudo`用户组，即获取超级用户权限。`-a`即`append`，表示不移出原来的组而进入新组。

```
usermod username
```

当前用户更改为`username`。



### 用户口令的管理

```
passwd username
```

更改用户的密码，这需要超级用户权限。但我基本只有忘了密码才会该所以单纯`passwd`对我没有意义。

```
passwd -d username
```

`d`即`delete`，表示删除该用户的密码。

## 用户组管理

### 添加用户组

```
group FFF
```

添加群`FFF`。

### 删除用户组

```
groupdel FFF
```

### 修改用户组

```
group -n FIRE FFF
```

将`FFF`改为`FIRE`。







. ~/.bashrc： 更新.bashrc后重新读取内容

## [tar压缩解压缩命令详解](https://www.cnblogs.com/jyaray/archive/2011/04/30/2033362.html)

**tar命令详解**

-c: 建立压缩档案

-x：解压

-t：查看内容

-r：向压缩归档文件末尾追加文件

-u：更新原压缩包中的文件

这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个。

下面的参数是根据需要在压缩或解压档案时可选的。

-z：有gzip属性的

-j：有bz2属性的

-Z：有compress属性的

-v：显示所有过程

-O：将文件解开到标准输出

参数-f是必须的

-f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。

\# tar -cf all.tar *.jpg 这条命令是将所有.jpg的文件打成一个名为all.tar的包。-c是表示产生新的包，-f指定包的文件名。
\# tar -rf all.tar *.gif 这条命令是将所有.gif的文件增加到all.tar的包里面去。-r是表示增加文件的意思。 
\# tar -uf all.tar logo.gif 这条命令是更新原来tar包all.tar中logo.gif文件，-u是表示更新文件的意思。 
\# tar -tf all.tar 这条命令是列出all.tar包中所有文件，-t是列出文件的意思 
\# tar -xf all.tar 这条命令是解出all.tar包中所有文件，-x是解开的意思

**查看**
tar -tf aaa.tar.gz  在不解压的情况下查看压缩包的内容

**压缩**

tar –cvf jpg.tar *.jpg //将目录里所有jpg文件打包成tar.jpg

tar –czf jpg.tar.gz *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用gzip压缩，生成一个gzip压缩过的包，命名为jpg.tar.gz

tar –cjf jpg.tar.bz2 *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用bzip2压缩，生成一个bzip2压缩过的包，命名为jpg.tar.bz2

tar –cZf jpg.tar.Z *.jpg  //将目录里所有jpg文件打包成jpg.tar后，并且将其用compress压缩，生成一个umcompress压缩过的包，命名为jpg.tar.Z

**解压**

tar –xvf file.tar //解压 tar包

tar -xzvf file.tar.gz //解压tar.gz

tar -xjvf file.tar.bz2  //解压 tar.bz2tar –xZvf file.tar.Z //解压tar.Z

**总结**

1、*.tar 用 tar –xvf 解压

2、*.gz 用 gzip -d或者gunzip 解压

3、*.tar.gz和*.tgz 用 tar –xzf 解压

4、*.bz2 用 bzip2 -d或者用bunzip2 解压

5、*.tar.bz2用tar –xjf 解压

6、*.Z 用 uncompress 解压

7、*.tar.Z 用tar –xZf 解压



#### [linux后台运行和关闭、查看后台任务](https://www.cnblogs.com/kaituorensheng/p/3980334.html)

&：放在命令最后，表示后台执行

ctrl+z：放到后台，并处于暂停

jobs：查看当前后台运行的命令 ，加上`-l`显示人物PID

fg：后台回前台，多个命令可用fg %jobnumber

bg：后台暂停的命令继续执行，多命令可用bg %jobnumber

kill：杀死进程



