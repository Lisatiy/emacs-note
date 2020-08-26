## [day4](https://github.com/emacs-china/Spacemacs-rocks/issues/35)

### Talk more about load, load-file, require, provide and auto-load

require 依赖于 load, load依赖于load-file. load优先加载.elc文件, load-file必须指定具体文件类型
[Further reading](http://ergoemacs.org/emacs/elisp_library_system.html)

``` elisp
(require 'init-packages)
(load "init-package")
(load-file "~/.emacs.d/lisp/init-packages.elc")
```

tip: 编译成.elc文件

``` elisp
byte-compile-file
```

### Better defaults

1. Indent-region or buffer

   ``` elisp
   (defun indent-buffer ()
     "Indent the currently visited buffer."
     (interactive)
     (indent-region (point-min) (point-max)))
   
   (defun indent-region-or-buffer ()
     "Indent a region if selected, otherwise the whole buffer. "
     (interactive)
     (save-excursion
       (if (region-active-p)
   	(progn
   	  (indent-region (region-beginning) (region-end))
   	  (message "Indented selected region."))
         (progn
   	(indent-buffer)
   	(message "Indented buffer.")))))
   (global-set-key (kbd "C-M-\\") 'indent-region-or-buffer)
   ```

   buffer内缩进对齐

2. another way to complete things in Emacs

   ``` elisp
   (setq hippie-expand-try-functions-list '(try-expand-dabbrev
   					 try-expand-dabbrev-all-buffers
   					 try-expand-dabbrev-from-kill
   					 try-complete-file-name-partially
   					 try-complete-file-name
   					 try-expand-all-abbrevs
   					 try-expand-list
   					 try-expand-line
   					 try-complete-lisp-symbol-partially
   					 try-complete-lisp-symbol))
   (global-set-key (kbd "s-/") 'hippie-expand)
   ```

   company无法补全的时候用hippie-expand

### Dired mode and file related operations

`C-x d` `enter` dired mode

1. copy, delete and rename file `C`, `d`(D 直接询问是否删除), `R`
   Copy/Delete/Rname files and folders  `C`, `d`(D 直接询问是否删除), `R`
   u 取消标记 `x` 执行

   ``` elisp
   (fset 'yes-or-no-p 'y-or  -n-p)
   (setq dired-recursive-deletes 'always)
   (setq dired-recursive-copies 'always)
   (put 'dired-find-alternate-file 'disabled nil)
   (with-eval-after-load 'dired
     (define-key dired-mode-map (kbd "RET") 'dired-find-alternate-file)) ;只有当执行dired-mode的后才会执行
   (setq dired-dwim-target t) ;效果如下图
   ```

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428225357.png)

2. add new file and folder

   `+` for adding new folder
   `C-x C-f` to create a new file 
   `g` to refresh dired buffer

3. open dired of current buffer

   ``` elisp
   (required 'dired-x)
   ```

   after applying this setting, we could press `C-x C-j` to jump to the dired buffer of current file.

4. open finder on Mac.

### Bonus Time. Use Org-mode literate programming to organize your Emacs configuration

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428230915.png)

### Exercise