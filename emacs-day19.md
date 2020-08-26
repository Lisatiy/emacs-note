## [day19](https://emacs-china.org/t/21-emacs-19-elisp/971) - [outline](https://github.com/emacs-china/Spacemacs-rocks/tree/master/Season2/day19)

Topic: Elisp Hacking Tips

### Generic tips

1. hooks
   比如想在org-mode激活以后进行一些设置, 用add-hook

   ``` elisp
   (add-hook 'org-mode-hook '(lamdda()(xxx)))
   ```

2. write elisp functions
   定制如下的函数
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588423832430.png)

   ``` elisp
   (defun zilongshanren/evil-quick-replace (beg end )
     (interactive "r")		 ;; C h v interactive r--Region 获取选中内容的开头和结尾
     (when (evil-visual-state-p) ;; C 1 查看函数信息: 判断当前状态是否是visual state
       (evil-exit-visual-state)
       (let ((selection (regexp-quote (buffer-substring-no-properties beg end)))) ;; 得到选中的字符串
         (setq command-string (format "%%s /%s//g" selection)) ;; 设置替换命令
         (minibuffer-with-setup-hook				;; 添加hook
             (lambda () (backward-char 2))			;; 向后面移动两个字符
           (evil-ex command-string)))))
   ;; 绑定快捷键, evil-visual-state-map: 只有在选中区域后才会执行快捷键
   (define-key evil-visual-state-map (kbd "C-r") 'zilongshanren/evil-quick-replace)
   ```

### Advice

1. 让函数在执行前(before)或者执行后(after)执行一些代码

```elisp
;;mimic "nzz" behaviou in vim
(defadvice evil-search-next (after advice-for-evil-search-next activate)
  (evil-scroll-line-to-center (line-number-at-pos)))

(defadvice evil-search-previous (after advice-for-evil-search-previous activate)
  (evil-scroll-line-to-center (line-number-at-pos)))
```

初始时`C d` 选中一些符号 `n` 查找下一个 `N`查找上一个 `z z` 让光标居中, 添加了上述函数后, 查找时光标会自动居中

2. 让函数在执行过程中(around)执行一些代码

``` elisp
;;Don't ask me when close emacs with process is running
(defadvice save-buffers-kill-emacs (around no-query-kill-emacs activate)
  "Prevent annoying \"Active processes exist\" query when you quit Emacs."
  (flet ((process-list ())) ad-do-it))
```

### Debug elisp functions

<http://www.jianshu.com/p/f509c9a9cac0?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io>

```elisp
(defun aborn/debug-demo ()
  "debug demo function"
  (interactive)
  (let ((a "a")
        (b "value b")
    (message "middle")
    (setq c (+ 1 c))
    (xyz "a")
    (message "ggg")
    ))
```

自己更倾向与用edebug, `M-x edebug-defun` 选中内容, `C-r` 进入函数 `n`继续执行 (39m)

Write your own minor mode

<http://nullprogram.com/blog/2013/02/06/>

```elisp
(define-minor-mode
  shadowsocks-proxy-mode
  :global t
  :init-value nil
  :lighter " SS"
  (if shadowsocks-proxy-mode
      (setq url-gateway-method 'socks)
    (setq url-gateway-method 'native)))

(define-global-minor-mode
  global-shadowsocks-proxy-mode shadowsocks-proxy-mode shadowsocks-proxy-mode
  :group 'shadowsocks-proxy)
```

### 扩展阅读

<https://emacs-china.org/t/ranger-golden-ratio/964>

<https://emacs-china.org/t/topic/945/2> 

<https://emacs-china.org/t/spaceline/389>

<https://emacs-china.org/t/topic/889/3> 

<http://nullprogram.com/blog/2013/02/06/>

<http://stackoverflow.com/questions/21502367/elisp-defadvice-around-clarification> 

<http://ergoemacs.org/emacs/emacs_avoid_lambda_in_hook.html>

<http://emacs-fu.blogspot.com/2008/12/hooks.html>

对于里面的函数, `C h f`查找它们的功能