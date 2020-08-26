### day1

#### Install emacs

#### Go over the Emacs tutorial at least once

* `C-h t` to open the tutorial.  `q` quit the buffer.
* You need to be familiar with the cursor movement (`C-f` `C-b` `C-n` `C-p` `C-a` `C-e`) and basic editing `C+k` 删除当前位置到行末并将内容放置在剪切板, `C+y`粘贴, `C+d`相当于键盘上的DELETE键
  `CTRL+@ (CTRL+SHIFT+2)` 选中区域  `Alt+w`复制 `C-x u`撤销
* You should be familiar with M(eta, alt), s(uper, command key), S(hift), C(trl) `M-x s-p S-p C-p`
* Prefix key (`C-h` is a prefix key) and `C-g` 中断

#### Learn to active some built-in functionality (org-mode)

* linum-mode to display line numbers (`M-x` linum-mode TAB补全)
* `C-x C-f` to open files, `C-x C-s` to save files, `C-x C-v` 切换文件, `C-x C-c` to quit files.
* you should always ask Emacs the right question  
  `C-h k` 寻找快捷键的帮助信息  `C-h v` 寻找变量的帮助信息 `C-h f`寻找函数的帮助信息 
* The key bindings are actually a quick way to command Emacs.

#### Learn some elisp (emacs lisp)

* use [learnxinyminutes](https://learnxinyminutes.com/docs/elisp/) website to learn emacs lisp.  

* at least you know how to define variable, functions

* you should know how to make a function callable and how to set a key binding for the function.

  ```elisp
  (+ 2 2)/ (函数表达式 参数1 参数2) 光标放在括号后面 C-x C-e 执行  
  (+ 2 (* 3 4))/ ; 2 + 3 * 4/    ; 注释  
  (setq my-name "shufei")    ; 定义my-name变量，变量名为shufei  
  (message my-name)    ; 输出变量  
  (defun my-func ()
  	(message "hello, " my-name))  ; 定义函数
  (my-func)	; C-x C-e 执行函数
  (defun my-func ()
  	(interactive)
  	(message "hello, " my-name))  ; 定义交互式函数 M-x可以调用
  (global-set-key (kbd "<f2>") 'my-func)  ; 绑定快捷键
  ```

#### start to hacking Emacs from the day one!  

* turn off tool-bar

  ```elisp
  (tool-bar-mode -1)
  ```

* turn off scroll-bar

  ``` elisp
  (scroll-bar-mode -1)
  ```

* show linum-mode

  ``` elisp
  (linum-mode t)
  ```

* turn off splash screen

  ``` elisp
  (setq inhibit-splash-screen 1)
  ```

* save your cofig

* define a function to quickly open your config file.

  ``` elisp
  (defun open-my-init-file()
    (interactive)
    (find-file "~/.emacs.d/init.el"))
  (global-set-key (kbd "<f2>") 'open-my-init-file)
  ```

#### Emacs package system in the first glance

* How to use the built-in Package system of Emacs
  options->manage emacs packages
* install company mode and active it
  * 使用 [emacs-china](http://elpa.emacs-china.org/) 社区搭建的 elpa 镜像
  * options->manage emacs packages 点击company, 点击install 
  * 文件下载到`~/.emacs.d/elpa`目录中. `M-x` company-mode启动
  * 回到init.el文件, (package-initialize) 告诉去哪找安装的package
  * `M-x` global-company-mode enable or disable, 在补全的时候可以用`M-n`或者`M-p`来选择

* Major mode and minor mode

  * major mode一个文件只能有一个
  * `C-h m` 查看使用的minor modes, 可以有多个  `M-x` xxx-xxx-mode  enable or disable xxx-xxx-mode

  ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200427232601.png)

* org-mode

  * 提纲

    ``` org-mode
    * 1级提纲
    ** 2级提纲
    *** 3级提纲
    ...
    ```

    TAB键可以方便的展开隐藏

  * TODO事项
    `C-c C-t` 变成TODO事项, 完成后再按变成DONE, 再按恢复正常