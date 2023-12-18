# 🎼 如何下载Spotify上面的歌曲（PC + 安卓）

最近正使用Spotify~~免费~~听音乐，音乐库分类功能确实有用

但是上面的歌曲不开通premium不能下载，即使开通了下载的也是加密文件，出门在外的时候想要收听没有办法

话说在前，这里只是介绍一个**离线收听**的方法，本人不对任何侵权行为负责

### Windows利用Savify下载

Github项目地址：[Savify](https://github.com/LaurenceRawlings/savify)

  1. 从release下面**下载exe文件**

先说一件事，你需要有Spotify的API才能下载

[Spotify API](https://developer.spotify.com/dashboard)申请

  2. 如果你的账户还不是开发者账户的话，需要先验证一下

  3. 选择[Create App](https://developer.spotify.com/dashboard/create)

  [![photo1](https://github.com/DrLightko/DrLightko/blob/main/images/photo1.png)](https://github.com/DrLightko/DrLightko/blob/main/images/photo1.png)

  4. 这些都随便写，创建完后点开Setting，复制Client ID和收起的Client secret

[![photo2](https://github.com/DrLightko/DrLightko/blob/main/images/photo2.png)](https://github.com/DrLightko/DrLightko/blob/main/images/photo2.png)

[![photo3](https://github.com/DrLightko/DrLightko/blob/main/images/photo3.png)](https://github.com/DrLightko/DrLightko/blob/main/images/photo3.png)

  5. 右键此电脑，属性，高级系统设置，环境变量，新建两个变量名为***SPOTIPY_CLIENT_ID***和***SPOTIPY_CLIENT_SECRET***，它们的值就是刚刚复制的

[![photo3](https://github.com/DrLightko/DrLightko/blob/main/images/photo4.png)](https://github.com/DrLightko/DrLightko/blob/main/images/photo4.png)

  6. 现在你就可以先在exe文件所在文件夹**shift + 右键**，选择在终端中打开，输入
```cmd
.\savify "LINK"
```

[![photo5](https://github.com/DrLightko/DrLightko/blob/main/images/photo5.png)](https://github.com/DrLightko/DrLightko/blob/main/images/photo5.png)

  7. 如果出现这样说明成功了，然后就可以下载了，输入
```
.\savify "LINK" -o "LOCAL"
```

* 第一个双引号后面是你要下载的歌单，单曲又或是专辑的**链接**  

* 参数 **-o** 后面的双引号内**下载路径**，默认就在exe所在文件夹

* 参数设置

    * 自定义下载

```cmd
.\savify "https://open.spotify.com/track/4Dju9g4NCz0LDxwcjonSvI" -q best -f mp3 -o "/path/to/downloads" -g "%artist%/%album%"
```
> -g 会以以下格式对下载进行分组

```cmd
main
    |
    |- artist
          |
          |- album
                |
                |- music.mp3
    |
    |- artist
```
  8. 回车即开始下载，**注：全程需要魔法**，速度还行，一个小时就下了100首歌了~~满意了😅~~

### 安卓使用Spowlo进行下载

* 打开就能用，推荐设置好Client ID和Client secret再下载，速度快很多~~不设置也能下载~~

* 崩溃情况比较多，没法 😑

***THE END***
