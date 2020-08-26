## day2

### Fixes some annoying stuff

1. `C-x 2` new window below    `C-x 3` new window on right

2. make cursor style to bar

   ``` elisp
   (setq-default cursor-type 'bar)
   ```

   the different between `setq` and `setq-default` in [stackoverflow](https://stackoverflow.com/questions/18172728/the-difference-between-setq-and-setq-default-in-emacs-lisp)

3. disable backup file

   ``` elisp
   (setq make-backup-files nil)
   ```

4. use `C-c '` to  open another buffer to edit source code

   `<s TAB` to insert source code

   ``` elisp
   #+BEGIN_SRC emacs-lisp
      (setq make-backup-files nil)
   #+END_SRC
   ```

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428085535.png)

5. make source code fancy in the org file.

   ```elisp
   (require 'org) ; require加载特性
   (setq org-src-fontify-natively t)
   ```

6. enable recentf-mode

   ``` elisp
   (require 'recentf)
   (recentf-mode 1)
   (setq recentf-max-menu-items 25)
   (global-set-key "\C-x\ \C-r" 'recentf-open-files)
   ```

   `M-x` eval-buffer 执行整个buffer   `C-x C-r` 打开最近的文件

7. bring electric-indent-mode back

   ``` elisp
   (electric-indent-mode t)
   ```

8. add delete selection mode

   ``` elsip
   (delete-selection-mode t)
   ```

### Make Emacs more fancy

1. open with full screen

   ``` elisp
   (setq initial-frame-alist (quote ((fullscreen . maximized))))
   ```

2. show match parents

   ``` elisp
   (add-hook 'emacs-lisp-mode-hook 'show-paren-mode)
   ```

   add-hook添加钩子, 即在emacs-lisp的major mode下添加show-paren-mode的minor mode

3. Highlight current line (global-hl-line-mode)

   ``` elisp
   (global-hl-line-mode t)
   ```

### Improve built-in package system

1. make package system more powerful with [Melpa](http://melpa.org/#/) (packages的源)
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588040024659.png)

   ``` elisp
    ;; 配置国内的源
   (when (>= emacs-major-version 24)
     (require 'package)
     (package-initialize)
     (setq package-archives '(("gnu"   . "http://elpa.emacs-china.org/gnu/")
   			   ("melpa" . "http://elpa.emacs-china.org/melpa/"))))
    ;; cl - Common Lisp Extension
    (require 'cl)
    ;; Add Packages
    (defvar lisatiy/packages '(
   		;; --- Auto-completion ---
   		company
   		;; --- Better Editor ---
   		hungry-delete
   		swiper
   		counsel
   		smartparens
   		;; --- Major Mode ---
   		js2-mode
   		;; --- Minor Mode ---
   		nodejs-repl
   		exec-path-from-shell
   		;; --- Themes ---
   		monokai-theme
   		;; solarized-theme
   		) "Default packages")
    (setq package-selected-packages lisatiy/packages)
    ;; 判断lisatiy/packages里面的package是否已经安装, 全部安装完返回nil
    (defun lisatiy/packages-installed-p ()
        (loop for pkg in my/packages
   	   when (not (package-installed-p pkg)) do (return nil)
   	   finally (return t)))
   ;; 当没有安装的时候就安装
    (unless (lisatiy/packages-installed-p)
        (message "%s" "Refreshing package database...")
        (package-refresh-contents)
        (dolist (pkg my/packages)
          (when (not (package-installed-p pkg))
   	 (package-install pkg))))
   ```

2. install a theme (monokai)

   ``` elisp
   (load-theme 'monokai t)
   ```

3. install hungry delete mode
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428104845.png)

   ```elisp
   (require 'hungry-delete)
   (global-hungry-delete-mode)
   ```

4. package-list-packages (add/delet/update packages)

   `M-x` package-list-packages
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428110105.png)

   `i`下载标记 `u`标记取消 `d` 删除标记 `U`更新标记  `x` 执行标记内容

   `M-x` package-autoremove 删除多余的package

5. install and configure smex and ivy mode

   * smex 有了下面的就不需要了

     ``` elisp
     ;; config for smex
       (require 'smex) ; Not needed if you use package.el
       (smex-initialize) ; Can be omitted. This might cause a (minimal) delay
     					; when Smex is auto-initialized on its first run.
       (global-set-key (kbd "M-x") 'smex) 
     ```

     ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428112623.png)

   * swiper + counsel

     ``` elisp
     (ivy-mode 1)
     (setq ivy-use-virtual-buffers t)
     (setq enable-recursive-minibuffers t)
     ;; enable this if you want `swiper' to use it
     ;; (setq search-default-mode #'char-fold-to-regexp)
     (global-set-key "\C-s" 'swiper)
     (global-set-key (kbd "C-c C-r") 'ivy-resume)
     (global-set-key (kbd "<f6>") 'ivy-resume)
     (global-set-key (kbd "M-x") 'counsel-M-x)
     (global-set-key (kbd "C-x C-f") 'counsel-find-file)
     (global-set-key (kbd "<f1> f") 'counsel-describe-function)
     (global-set-key (kbd "<f1> v") 'counsel-describe-variable)
     ```

     `M-x` counsel-M-x  `C-x C-f` 查找文件 `C-x b` 跳转到recent文件 `C-s`查找出现预览内容 `C-n C-p` 选择预览内容

     ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428113855.png)

6. use customize-group to customize the package settings
   `M-x` customize-group -> package(e.g., company)
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428115100.png)

7. install and configure smartparens mode

   ``` elisp
   (require 'smartparens-config)
   (add-hook 'emacs-lisp-mode-hook 'smartparens-mode)
   ```

8. Don't try to update the package daily, the updating process might failed

**tips**: press M-RET to fix the order, you could also use M-RET to add new headings, cheers!

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428120605.png)

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428120927.png)

### Setup a javascript IDE

1. Install js2-mode and start to write javascript

   ``` elisp
   (setq auto-mode-alist
         (append
          '(("\\.js\\'" . js2-mode))
          auto-mode-alist))
   ```

2. Install nodejs-repl to execute code inside Emacs

   ```
   (require 'nodejs-repl)
   ```

   Type `M-x nodejs-repl` to run Node.js REPL. 

### Learn more from Emacs itself

1. `C-h C-f` (find-function), `C-h C-v` (find-variable), `C-h C-k` (find-function-on-key)

   ```elsip
   (global-set-key (kbd "C-h C-f") 'find-function)
   (global-set-key (kbd "C-h C-v") 'find-variable)
   (global-set-key (kbd "C-h C-k") 'find-function-on-key)
   ```

   e.g. `M-x find-function`

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428123931.png)

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428124009.png)

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428124038.png)

2. Tell users to learn more about elisp (`M-x info`)
   M-x info -> **Emacs Lisp Intro** ->至少看到 **Loops & Recursion**

### Org-mode (Bonus Time)

#### Agenda files and agenda view

one gtd.org file

```elisp
(setq org-agenda-files '("~/org"))
(global-set-key (kbd "C-c a") 'org-agenda)
```

#### Learn how to schedule items and set deadline

1. `C-c C-s` todo事项的起始时间
2.  `C-c C-d` todo事项的deadline

`C-c a a` 进入agenda界面  `r` 更新agenda  `w`一周的agenda `d`一天的agenda

### Excercise

1. the difference between .emacs and .emacs.d/init.el file
2. try to configure company mode via customize-group