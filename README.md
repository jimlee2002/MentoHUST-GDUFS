# MentoHUST-GDUFS

**已知问题：部分栋不可用，欢迎issuse反馈**

修改自[@ivechan](https://github.com/ivechan)/**[mentohust-SYSU](https://github.com/ivechan/mentohust-SYSU)**，使其适用于 GDUFS。

基于南校区修改，北校区请自行测试可用性。

**仅作为学习EAP， EAPOL协议使用，请勿用于其他用途，造成后果自负。**

有问题欢迎提出 Issuse。

## 编译方法
请参考以下文章：
- [支持锐捷认证与IPv6的路由器配置指南：以K2P为例](https://github.com/KumaTea/MentoHUST-SYSU-Guide/blob/master/Guide.md)，作者[@KumaTea](https://github.com/KumaTea)
- [编译适用于 X86 的 MentoHUST](https://jimlee2002.github.io/posts/5ed2bcfa.html)
- [使用 WSL 交叉编译 MentoHUST](https://jimlee2002.github.io/posts/4d028789.html)

## 使用方法
首次使用：
```bash
mentohust -u <用户名> -p <密码> -n <wan口对应网卡> -e 60 -d 1
```
测试无问题后按 Ctrl+C 暂时退出程序，输入指令：
```bash
mentohust -u <用户名> -p <密码> -n <wan口对应网卡> -e 60 -d 1 -b 3 -w
```
随后，MentoHUST 会以后台运行模式进行认证，同时保存当前配置信息，以后只需键入`mentohust`即可读取已有配置进行认证。

## 参考资料

- [锐捷认证过程分析与第三方锐捷认证客户端的设计与实现](https://github.com/ShanQincheng/jmuSupplicant/blob/master/doc/锐捷认证过程分析与第三方锐捷认证客户端的设计与实现.pdf)，作者为[@ShanQincheng](https://github.com/ShanQincheng) 
- [Mentohust V4版本的心得](https://codingstory.com.cn/mo-gai-mentohust-v4ban-ben-de-xin-de/)，作者为[@ShanQincheng](https://github.com/ShanQincheng) （这里是该文于[@rensilin](https://github.com/rensilin)/[mentohust_nwafu](https://github.com/rensilin/mentohust_nwafu)上的存档，原文链接已失效）
- [issuse#282: 我校锐捷使用该V4算法，应该是丢失了许多信息，导致无法连接](https://github.com/hyrathb/mentohust/issues/282)
- [支持锐捷认证与IPv6的路由器配置指南：以K2P为例](https://github.com/KumaTea/MentoHUST-SYSU-Guide/blob/master/Guide.md)，作者为[@KumaTea](https://github.com/KumaTea)
- [@rensilin](https://github.com/rensilin)/**[mentohust_nwafu](https://github.com/rensilin/mentohust_nwafu)**
- [@ivechan](https://github.com/ivechan)/**[mentohust-SYSU](https://github.com/ivechan/mentohust-SYSU)**
- [@shanzhaozhen](https://github.com/shanzhaozhen)/**[mentohust_for_zqu](https://github.com/shanzhaozhen/mentohust_for_zqu)**

以下是原项目内容：

****

现在updateing实现了一个加载支持修改数据包内容的EAPOL认证客户端并将本工程的认证算法做成了插件，更加容易适配各个学校，建议大家尝试https://github.com/updateing/minieap

完全没怎么看原来的代码，瞎改的。
加入了V4支持。具体算法看checkV4.c

所有hash都是从算法在rhash和ampheck借来魔改的……。

建议Arch Linux用户安装AUR中的mentohust-git
#使用方法

#安装mentohust：建议Ubuntu用户使用Deb包安装，Fedora用户使用RPM包安装

#如果确定自己可以使用xrgsu认证成功，打开终端输入sudo mentohust运行即可
如果不确定，切换到锐捷所在目录，然后输入以下命令：
sudo mkdir /etc/mentohust
sudo cp ./8021x.exe  /etc/mentohust
sudo cp ./W32N55.dll /etc/mentohust
然后打开终端输入sudo mentohust运行。如果认证失败，再切换到锐捷所在目录，输入以下命令：
sudo cp ./SuConfig.dat /etc/mentohust
然后打开终端输入sudo mentohust运行即可。
如果准确按以上步骤操作后还是认证失败，请下载MentoHUSTTool，在Windows下抓包并保存为data.mpf，
然后回到Linux，切换到data.mpf所在目录，输入以下命令：
sudo cp ./data.mpf /etc/mentohust
然后打开终端输入sudo mentohust -f/etc/mentohust/data.mpf -w运行即可。以后也只需输入sudo mentohust。

#您也可以按下面的方法操作：
1、静态IP用户请事先设置好IP；
2、打开终端，输入sudo mentohust，回车；
3、［正确］输入相应信息，如果认证成功，跳到第8步；如果提示“不允许使用的客户端类型”，按Ctrl+C结束认证；
4、打开终端，输入sudo mentohust -w -f'锐捷目录下任意文件路径'，回车；
5、如果认证成功，跳到第8步；如果提示“客户端完整性被破坏”，按Ctrl+C结束认证；
6、将锐捷安装目录下的SuConfig.dat重命名为其他名字；
7、打开终端，输入sudo mentohust，回车；
8、如果是动态IP且不是Linux，打开相应设置去更新IP。
9、以后认证只需打开终端，输入sudo mentohust，回车。
10、要修改某些参数请输入mentohust -h查看帮助信息并据此修改，例如修改密码sudo mentohust -pNewPassword -w，要临时修改则不加-w参数。

#如何退出:不以后台模式运行mentohust时，按Ctrl+C即可退出；后台运行时使用sudo mentohust -k退出认证。

#查看帮助信息请输入：mentohust -h
更详细的帮助信息请参考：http://wiki.ubuntu.org.cn/锐捷、赛尔认证MentoHUST

#修改参数请根据帮助信息操作，例如修改用户名和密码：sudo mentohust -uUsername -pPassword -w
指定某些参数仅对当次认证有效请根据帮助信息操作，例如临时修改用户名和密码：sudo mentohust -uUsername -pPassword

#如果提示缺少libpcap.so.0.x而在/usr/lib/目录下已存在一个libpcap.so.0.x.y，输入以下命令：
sudo ln -s libpcap.so.0.x.y /usr/lib/libpcap.so.0.x
否则请安装libpcap。

#权责声明
1、本程序所有涉及锐捷赛尔认证的功能均是来自前辈公开代码及抓包分析。
2、本程序于个人仅供学习，于他人仅供方便认证，不得使用本程序有意妨害锐捷赛尔认证机制及相关方利益。
3、一切使用后果由用户自己承担。
4、本程序不提供任何服务及保障，编写及维护纯属个人爱好，随时可能被终止。
5、使用本程序者，即表示同意该声明。谢谢合作。

源码可在项目主页获取：http://mentohust.googlecode.com/
联系作者：在http://mentohust.googlecode.com/留言或Email：mentohust@ehust.co.cc
