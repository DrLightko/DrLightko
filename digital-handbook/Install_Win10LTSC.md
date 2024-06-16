# 记安装 Win10_LTSC 的折腾事
> 淘来一台老电脑，想着给家里老人用便把原生的 Win7 格式掉安装了 Win10 的长期支持版，速度比我的 Win10 快很多
- 去[微软官方 Win10LTSC 下载页面](https://www.microsoft.com/zh-cn/evalcenter/download-windows-10-enterprise) 根据自己电脑的位数和语言下载对应版本
> 如果电脑的品牌还在，那么可以在官网提前***下载好驱动***
- 制作一个启动盘，看好主机的 uefi 还是 legacy 启动，确定硬盘是 mbr 还是 gpt (uefi 对应 gpt，legacy 对应 mbr)
> 像这一台老电脑最好以 legacy 启动
- 安装系统，过程中***使用本地账户登录，过程中不要联网***
- 开机之后拿出准备好的驱动 U 盘安装驱动
> 应为过程中没有联网，所以 Windows 不会自己安装，省的挨个核实
- 下面是激活系统，其实不激活也行，只是看的桌面上的水印难受
- 一般安装好的系统叫 *Windows 10 Enterprise LTSC 2021 评估版* ，需要先***升级到完整版***
    1. Win + R 打开 *C:\Windows\System32\spp\tokens\skus* 文件夹
    2. 下载[激活文件](https://github.com/DrLightko/DrLightko/blob/main/files/Windows_10_ltsc_2021_skus_2.zip)，把它解压到刚刚打开的文件夹
    3. 打开 cmd 以管理员运行，输入
    ```
    cscript.exe %windir%\system32\slmgr.vbs /rilc
    cscript.exe %windir%\system32\slmgr.vbs /upk >nul 2>&1
    cscript.exe %windir%\system32\slmgr.vbs /ckms >nul 2>&1
    cscript.exe %windir%\system32\slmgr.vbs /cpky >nul 2>&1
    cscript.exe %windir%\system32\slmgr.vbs /ipk M7XTQ-FN8P6-TTKYV-9D4CC-J462D
    sc config LicenseManager start= auto & net start LicenseManager
    sc config wuauserv start= auto & net start wuauserv
    clipup -v -o -altto c:\
    echo
    ```
- 下面激活系统
    1. cmd 以管理员运行
    ```c
    slmgr -upk 卸载原秘钥 // 可干可不干，因为上面的密钥相同

    slmgr -ipk M7XTQ-FN8P6-TTKYV-9D4CC-J462D

    slmgr -skms kms.03k.org

    slmgr -ato

    slmgr -dlv
    ```
- 这样既可以正常使用了，如果想下微软商店的话直接运行
> 其实 LTSC 也有微软商店，只是不显示，这样刷新下就可以了

> LTSC 连 Windwos Defender 都有，为啥没有微软商店？
```
wsreset -i
```