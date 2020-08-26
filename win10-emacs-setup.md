1. 在[镜像网站](http://mirrors.nju.edu.cn/gnu/emacs/windows/)下载emacs并解压 (**D:\InSoftware\emacs-26.3** 这是我的解压路径)
2. 设置系统环境变量。系统环境变量的path变量中增加 **D:\InSoftware\emacs-26.3\bin**
3. win + r，在弹出的框中输入 **regedit**，回车后打开了注册表编辑器，找到其中 **HKEY_LOCAL_MACHINE**->**SOFTWARE** -> **GUN**(没有的话右击SOFTWARE->新建->项，并命名为GNU) ->Emacs(没有的话右击GUN->新建->项，并命名为Emacs)->右击Emacs->新建->字符串值（将新建字符串条目的名称改为**HOME**，**数据改为**解压目录，我的为**D:\InSoftware\emacs-26.3**）
4. 最后在cmd中运行**emacs -nw**，查看安装效果。

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200427204421.png)