### Ubuntu中文版man手册配置方法

---

man默认是英文的，但ubuntu的源里也有中文版的。

以下是配置方法:

1）终端输入sudo apt-get install manpages-zh

2)  安装后修改配置文件sudo gedit /etc/manpath.config

3)  将所有的/usr/share/man替换为/usr/share/man/zh_CN

4)  保存即可。