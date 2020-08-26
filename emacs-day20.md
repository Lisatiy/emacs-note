## [day20](https://emacs-china.org/t/21-emacs-20-spacemacs/972) - [outline](https://github.com/emacs-china/Spacemacs-rocks/tree/master/Season2/day20)

Topic: Revisit my Spacemacs config

### The new layer design

1. One aggregate layer with five other layers
   zilongshanren的layer声明在init.el中, 其他5个layer声明在zilongshanren的layer.el中, 所有的快捷键绑定在zilongshanren的keybindings.el中
2. The generic keybindings are all in one place
3. keep `user-config` minimal
   一些临时的配置
4. update constantly with the upstream

### Revisit my configs layer by layer

#### init.el

##### package

1. prodigy 启动一些web服务 `SPC a S`
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588427563802.png)
2. deft 搜索配置 `SPC a n`
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588427666734.png)
3. org `SPC a r` preview文件
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588427752985.png)

##### user-init

1. 添加了镜像

2. 修复启动速度的bug

   ``` elisp
   (setq tramp-ssh-controlmaster-options
   	"-o ControlMaster=auto -o ControlPath='tramp.%%C' -o ControlPersist=no")
   ```

3. 翻墙

   ``` elisp
   (setq socks-server '("Default server" "127.0.0.1" 1080 5))
   ```

4. 编译时的警告不要出现

   ``` elisp
   (setq byte-compile-warnings '(not obsolete))
   ```

##### user-config

1. `SPC v v`选中时不进入系统剪切板 `g v y` 选中yank后才进入系统剪切板

   ``` elisp
   (fset 'evil-visual-update-x-selection 'ignore)
   ```

2. 变量放在custom.el里面

   ``` elisp
   (setq custom-file (expand-file-name "custom.el" dotspacemacs-directory))
   ```

#### better-default-config.el

##### hexl-mode

``` elisp
(defun ffap-hexl-mode ()
  (interactive)
  (let ((ffap-file-finder 'hexl-find-file))
    (call-interactively 'ffap)))
```

`SPC f h` 使用十六进制打开文件, 转回去 `M-x set-buffer-file-coding-system` `utf-8`

##### pop-up-frames

``` elisp
(when (spacemacs/window-system-is-mac)
  (setq ns-pop-up-frames nil))
```

右键打开文件选择方式为emacs时, 不会弹出新的窗口

##### 不让BOM影响文件读取

``` elisp
(setq auto-coding-regexp-alist
      (delete (rassoc 'utf-16be-with-signature auto-coding-regexp-alist)
              (delete (rassoc 'utf-16le-with-signature auto-coding-regexp-alist)
                      (delete (rassoc 'utf-8-with-signature auto-coding-regexp-alist)
                              auto-coding-regexp-alist))))
```

##### lambda符号显示

``` elisp
(global-prettify-symbols-mode 1)
```

##### 英文拼写修正 `C ;` 

##### 括号补全与不补全

``` elisp
(delete-selection-mode t)
(define-minor-mode dubcaps-mode
  "Toggle `dubcaps-mode'.  Converts words in DOuble CApitals to
Single Capitals as you type."
  :init-value nil
  :lighter (" DC")
  (if dubcaps-mode
      (add-hook 'post-self-insert-hook #'dcaps-to-scaps nil 'local)
    (remove-hook 'post-self-insert-hook #'dcaps-to-scaps 'local)))
```

##### 只用fundamental-mode打开大文件

防止激活太多的minor-mode使得打开文件变卡

``` elisp
(defun spacemacs/check-large-file ()
  (when (> (buffer-size) 500000)
    (progn (fundamental-mode)
           (hl-line-mode -1)))
  (if (and (executable-find "wc")
           (> (string-to-number (shell-command-to-string (format "wc -l %s" (buffer-file-name))))
              5000))
      nil))

(add-hook 'find-file-hook 'spacemacs/check-large-file)
```

##### 查找文件时, 不存在的文件名是否创建目录

``` elisp
(defadvice find-file (before make-directory-maybe
                             (filename &optional wildcards) activate)
  "Create parent directory if not exists while visiting file."
  (unless (file-exists-p filename)
    (let ((dir (file-name-directory filename)))
      (when dir
        (unless (file-exists-p dir)
          (make-directory dir t))))))
```

