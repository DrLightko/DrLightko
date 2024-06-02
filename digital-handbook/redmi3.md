# 记一台红米 3 的刷机过程

> 从老人家手里拿到一个不能开机的红米，结果插上电后就开机了，成色很新，但是 MIUI 只支持到 9 ，很多应用都用不了，所以打算刷入新的系统
1. 首先看一下机器的配置：
    - 2016年发布，699 元 6G + 16G
    - 高度为139.3毫米，宽度为69.6毫米，厚度为8.5毫米，重量为144克
    - 晓龙 616，主频最高 1.5 G
    - 代号 ido
    > 查看对应的系统主要就是对照这三条
2. 解锁 BootLoader

    - 下载[小米官方解锁工具](https://www.miui.com/unlock/index.html)

    - 手机上登录小米账号，启用USB调试，关机后按住音量上键进入fastboot模式

    - 电脑上打开工具，确认登录，安装驱动，直到解锁完毕点击重启

3. 下载必须文件

    - 下载[安卓 adb](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)，(这是没有SDK，单独的)，放入环境变量 (不放也可以，就是全程在这个目录下操作)

    - 下载 twrp

        > 可以把twrp理解为一个刷入第三方系统的工具，官方的 recovery 不支持的第三方 ROM 可以使用 twrp 完成

        - [红米3的twrp地址](https://twrp.me/xiaomi/xiaomiredmi3.html)，其他机型自己到[twrp官网](https://twrp.me/)查找

    - 下载系统，本来想下 [lineageOS](https://lineageos.org/) 的，但是官网只有红米3S和3X，有一个国内修改的版本网站没法注册，所以用了魔趣ROM

    - 魔趣的 rom 托管在 source forge，这是[魔趣仓库的地址](https://sourceforge.net/projects/mokee/files/)，幸亏release下面还有 ido 的 rom
4. 准备完毕，开始刷机
    - usb连接手机与电脑 (之前使用小米刷机时安装过驱动)

    - cmd 打开输入
        ```
        adb reboot bootloader
        ```
        > 记得打开 usb 调试

        > 或者关机后音量上 (下) 进入 fastboot

    - 确认电脑能找到fastboot设备
        ```
        fastboot devices
        ```
    - 在当前执行目录下把 twrp img 复制过来，执行
        ```
        fastboot boot twrp-3.7.0_9-0-ido.img
        ```

        > 这一步不是安装 twrp ，只是使用
    
    - 如果看到了下面的界面，说明成功了，动按钮以允许修改

    - 选择 高级 - adb sideload - 滑动已开始，之后输入

        ```c
        adb sideload D:\Default\download\MK100.0-ido-221019-RELEASE.zip

        // 最后一个参数是你的 rom 地址
        ```

        > 具体可以看[这篇文章](https://segmentfault.com/a/1190000021269145)

    - 只要你下载的是正经 rom ，等到 100% 后就应该成功了 (本人这里出现了 adb: failed to read command: No error 不过没有影响)

    - 如果联网出现叹号，参考[这篇文章](https://www.bilibili.com/read/cv16146843/)

        ```c
        adb shell "settings put global captive_portal_http_url http://connect.rom.miui.com/generate_204"; 

        adb shell "settings put global captive_portal_https_url https://connect.rom.miui.com/generate_204";

        // 开启飞行模式，关闭飞行模式，重新开机
        ```

        > 如果出现 android process media 屡次停止运行，可以尝试重启或者重置手机
- 这下就算完成了，新系统很好用