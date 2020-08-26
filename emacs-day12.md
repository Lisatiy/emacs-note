## [day12](https://emacs-china.org/t/21-emacs-12-spacemacs-layer/669) - [outline](https://github.com/emacs-china/Spacemacs-rocks/tree/master/Season2/day12)

### 从远程库更新

``` git
git co develop
git fetch upstream
git merge upstream/develop
```

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588299116768.png)

### Config Variables

每个layer可以配置一下变量, 这些变量在readme里面有介绍
`SPC h SPC` better default  查看该layer的config.el文件, 里面的定义 变量可以通过variables修改值

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588300003305.png)

`C-a` and `C-e`分别跳转到代码首和尾  连按`C-a` and `C-e`分别到行首和行(行中包括注释)尾
`M-x counsel-set-variable` 设置variable值 -> `exec-path-from-shell-arguments` 设置这个变量的值
`M-x customize-variable` 也可设置variable值

### 添加helm layer

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588301729108.png)

`SPC s p` 搜索默认用counsel-ag, 不如helm-ag 

### Topic: Create layer for your own configs

1. 把.emacs.d/lisp/init-better-defaults.el中配置迁移到spacemacs中

2. `M-x configuration-layer/create-layer`->configuration layer path: `.spacemacs.d` -> `zilongshanren`  会创建一个packages.el和readme, readme可以不要

3. 在packages.el添加layer并定义 函数

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588302122018.png)

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588302196396.png)

   `, d m ` macrostep transient state     

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588302327152.png)

   `, d m e` expand 不停地按`e`  会扩展出来实际配置的运行语句, 发现会有自己设置的set-leader-keys和require(因为emacs启动时会require一次, 这里实际上不需要require). condition-case出错的时候保证自己收到警告

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588302720173.png)

   设置`defer t`, 不在扩展的实际语句中`require layer`, 减少一次require. , d m e` expand 不停地按`e`  会发现只有set-leader-key, 没有require了

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588302560306.png)

4. 添加config.el和keybindings.el文件并定义相关配置

tips: `SPC h r` 查看layer structure的配置建议

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588301274042.png)

layer的结构

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588301299884.png)

packages.el 安装包, 配置和packages很相关的配置, 如私有函数
funcs.el 定义全局函数
config.el 定义emacs的一些默认配置, 如`(global-linum-mode t)`

### More tweaks of the builit layers

- config variables (chinese layer)

### Write your first layer

### 快捷键

`SPC b b` switch to buffer

`SPC h r` 在文档中搜索相关帮助, 如搜索evify layer的信息