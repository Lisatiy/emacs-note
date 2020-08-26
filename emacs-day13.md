## [day13](https://emacs-china.org/t/21-emacs-13-layer/674) - [outline](https://github.com/emacs-china/Spacemacs-rocks/tree/master/Season2/day13)

Topic: More tweaks of your own layers

### Fix evilify issues

把evilified的定义移动到user-config()中, user-config是在所有layer都加载完成之后再加载

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588343261481.png)

### Fix ivy 0.8 issues

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588344600242.png)

### post-init and pre-init

layer运行时先调pre-init, 再调init, 最后调post-init

`SPC h SPC`  搜素layer, 对应已经安装好的layer, 如company, 通过post-init配置, 如下

![1588344793077](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588344793077.png)

pre-init很少使用, 一般post-init就可满足使用

### location: builtin, elpa and github

安装package时, 默认从elpa去安装; 定制emacs内置的mode, 如occur-mode, 用location built-in

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588344793077.png)

不知道写的对不对, 看看内置的location built-in怎么写的

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588345230575.png)

自己写的和内置的写法不一样, 修正一下

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588345799566.png)

然后配置自己的函数

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588345829588.png)

tips: 使用fetcher从GitHub上安装layer(melpa上没有的package)

查看内置用法

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588345967538.png)

仿照内置用法使用, [gulpjs](https://github.com/zilongshanren/emacs-gulpjs/blob/master/gulpjs.el)是provide的名字, [zilongshanren/emacs-gulpjs](zilongshanren/emacs-gulpjs)是repo的名字, 这样会拉取GitHub上的最新的commit

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588346350892.png)

`SPC f e R` 安装

### layers.el

如果都在post-init里面对layer进行自己的偏好设置, 当layer太多是就比较麻烦了. 故创建layers.el专门负责自己对不同layer的偏好设置, 如remove原始的youdao-dictionary

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588346653093.png)

则默认的配置不会生效, 只会使用自己的youdao-dictionary里面的配置, 如下

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588346740661.png)