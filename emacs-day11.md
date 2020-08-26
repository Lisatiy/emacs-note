## [day11](https://emacs-china.org/t/21-emacs/603) - [大纲](https://github.com/emacs-china/Spacemacs-rocks/tree/master/Season2/day11)

### 使用zilong的配置

1. 备份.emacs.d文件 `cp .emacs.d .emacs.d.bak`
2. 进入.emacs.d文件，把本地的文件都删掉, 克隆spacemacs的最新内容, `git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d`  
3. 在`~`目录新建.spacemacs.d目录将zilong的配置clone至里面
4. 打开emacs安装packages

### 自己安装配置

1. 备份.emacs.d文件 `cp .emacs.d .emacs.d.bak`

2. 进入.emacs.d文件，把本地的文件都删掉, 克隆spacemacs的最新内容, `git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d`  

3.  启动emacs, 
   preferred style: vim 推荐的
   what distribution:  spacemacs 推荐的
   生成.spacemacs配置文件, 终止进程

4. 添加下面的代码到 `.spacemacs` 的 `dotspacemacs/user-init()`

   ``` elisp
   (setq configuration-layer--elpa-archives
       '(("melpa-cn" . "http://mirrors.tuna.tsinghua.edu.cn/elpa/melpa/")
         ("org-cn"   . "http://mirrors.tuna.tsinghua.edu.cn/elpa/org/")
         ("gnu-cn"   . "http://mirrors.tuna.tsinghua.edu.cn/elpa/gnu/")))
   ```

   [emacs-chin](http://elpa.emacs-china.org/)a的[镜像](https://github.com/emacs-china/elpa)不太好使了, 换成[清华的镜像](https://mirror.tuna.tsinghua.edu.cn/help/elpa/)

5. 再启动emacs, 快速安装packages

6. `SPC f j`进入dired-mode, `+` 在`~`目录新建.spacemacs.d目录, `R`将`.spacemacs`文件移动到.spacemacs.d目录, `R`将`.spacemacs`文件重命名为`init.el`

###  安装一些layer

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588265125171.png)

`SPC f e R` 安装packages `SPC w m`退出message的buffer

### little tweak

1. fullscreen

   ``` elisp
   dotspacemacs-maximized-at-startup t
   ```

2. hanging on startup
   Try using these settings in the `dotspacemacs/user-init()` function in your `init.el` configuration:

   ```elisp
   (setq tramp-ssh-controlmaster-options
         "-o ControlMaster=auto -o ControlPath='tramp.%%C' -o ControlPersist=no")
   ```

### [Fix ivy-spacemacs-help](https://github.com/syl20bnr/spacemacs/pull/6340)

### ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588265722034.png)

### [Exclude](https://emacs-china.org/t/packages-emacs/267) some unwanted packages 

evil-lisp-state spray doc-view lorem-ipsum

``` elisp
dotspacemacs-excluded-packages '(vi-tilde-fringe)
```

### Easy way to Add packages with default package settings

``` elisp
dotspacemacs-additional-packages '(youdao-dictionary)
```

### Add your own configs in `user-config` (Port the previous configs to Spacemacs)

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588266393301.png)

`C-s` 保存 

### Fix helm tramp mode issue

user-init中

```elisp
(setq tramp-ssh-controlmaster-options "-o ControlMaster=auto -o ControlPath='tramp.%%C' -o ControlPersist=no")
```

### Make customize-group configs in its own file

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588266577764.png)

```elisp
(setq custom-file (expand-file-name "custom.el" dotspacemacs-directory))
(load custom-file 'no-error 'no-message)
```

### 主题

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588266782857.png)

### Read the [docs](https://www.spacemacs.org/doc/DOCUMENTATION.html), [FAQ](http://spacemacs.org/doc/FAQ) and Use Spacemacs every day!

### 快捷键

`SPC f e d` 进入配置文件
`SPC f j` 进入dired mode
`SPC q q` 退出
`SPC h SPC` 查看layers和packages信息 -> 每个package里面有个readme.org