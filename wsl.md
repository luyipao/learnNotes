# wsl

## 版本操作

### 升级

升级前需要启用window更新否者可能出现下面的错误。

> 正在安装: 适用于 Linux 的 Windows 子系统
>
> 请求的操作需要提升。

启用后运行`wsl --update`。

如何禁用windows更新？我用的是52上的一个软件，因为用了很久已经忘记具体在哪了。

## 可视化处理

[Run Linux GUI apps on the Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/tutorials/gui-apps)

在`.bashrc`文件中添加`alias emacs='emacs -nw'`防止每次开emacs都要打开新窗口。

## 提升网速



[low internet speed in WSL 2](https://answers.microsoft.com/en-us/windows/forum/all/low-internet-speed-in-wsl-2/21524829-18be-4611-bb5f-cabccd2cae31)

网络适配器->vEthernet (WSL)->配置

```
Large Send Offload Version 2 (IPv4)  disable
Large Send Offload Version 2 (IPv6)  disable
```

保存。

## WSL2 被防火墙拦截

wsl2 中ping主机地址不通。关闭防火墙后通

在主机管理员模式下运行一下命令

```text
New-NetFirewallRule -DisplayName "WSL" -Direction Inbound  -InterfaceAlias "vEthernet (WSL)"  -Action Allow
```