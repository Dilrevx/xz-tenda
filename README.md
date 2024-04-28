修改并编译 xz
====

相关的文档比较少，记录一下踩过的坑

1. 编译方法：下载 **release** 版本的代码，跑 autogen.sh -> ./configure -> make **instal**。不 install 似乎没有二进制。不 configure 没有 Makefile。autogen 我忘了有没有用了
2. MAGIC HEADER, FOOTER 并不是仅在一处定义的。该全局变量在不同模块以不同的符号名重新定义了几次。好像是 lzma 和 xz 定义了两次。（注：vscode 提示的 MACRO 并不准）
3. xz 是动态连接的，HEADER 在 lib/liblzma.so

理论上应该只修改了两处：
1. HEADER
2. 直接 if true 短路掉 crc 校验

以及 permission 相关问题可能是共享文件夹的权限不能修改导致的
