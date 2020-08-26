## [day5](https://github.com/emacs-china/Spacemacs-rocks/issues/59)

### Fix smartparen quote issue

``` elisp
;; 单引号问题
(require 'smartparens-config) or (sp-local-pair 'emacs-lisp-mode "'" nil :action nil)
;; 高亮
(defadvice show-paren-function (around fix-show-paren-function activate)
  (cond ((looking-at-p "\\s(") ad-do-it)
	(t (save-excursion
	     (ignore-errors (backward-up-list))
	     ad-do-it)))
  )
```

tips: `M-x counsel-git-grep` 全局搜索 `M-x ibuffer D x` delete一个buffer `C-x k` kill一个buffer

### Editing large web page

``` elisp
(defun hidden-dos-eol ()
  "Do not show ^M in files containing mixed UNIX and DOS line endings."
  (interactive)
  (setq buffer-display-table (make-display-table))
  (aset buffer-display-table ?\^M []))

(defun remove-dos-eol ()
  "Replace DOS eolns CR LF with Unix eolns CR"
  (interactive)
  (goto-char (point-min))
  (while (search-forward "\r" nil t) (replace-match "")))
```

### Add more useful packages for web development

* web-mode

  ``` elsip
  ;; config for web mode
  (defun lisatiy-web-mode-indent-setup ()
    (setq web-mode-markup-indent-offset 2) ; web-mode, html tag in html file
    (setq web-mode-css-indent-offset 2)    ; web-mode, css in html file
    (setq web-mode-code-indent-offset 2)   ; web-mode, js code in html file
    )
  
  (add-hook 'web-mode-hook 'lisatiy-web-mode-indent-setup)
  
  (defun lisatiy-toggle-web-indent ()
    (interactive)
    ;; web development
    (if (or (eq major-mode 'js-mode) (eq major-mode 'js2-mode))
        (progn
  	(setq js-indent-level (if (= js-indent-level 2) 4 2))
  	(setq js2-basic-offset (if (= js2-basic-offset 2) 4 2))))
  
    (if (eq major-mode 'web-mode)
        (progn (setq web-mode-markup-indent-offset (if (= web-mode-markup-indent-offset 2) 4 2))
  	     (setq web-mode-css-indent-offset (if (= web-mode-css-indent-offset 2) 4 2))
  	     (setq web-mode-code-indent-offset (if (= web-mode-code-indent-offset 2) 4 2))))
    (if (eq major-mode 'css-mode)
        (setq css-indent-offset (if (= css-indent-offset 2) 4 2)))
  
    (setq indent-tabs-mode nil))
  (global-set-key (kbd "C-c t i") 'lisatiy-toggle-web-indent)
  ```

  `C-c t i` TAB4个空格和两个空格切换  `M-;` 注释 	`C-space` 标记

* js2-refactor

  ``` elisp
  ;; config for js2-refactor
  (add-hook 'js2-mode-hook #'js2-refactor-mode)
  ```

### occur and imenu

1. improve occur

   ``` elsip
   ;; dwin = do what i mean.
   (defun occur-dwim ()
     "Call `occur' with a sane default."
     (interactive)
     (push (if (region-active-p)
   	    (buffer-substring-no-properties
   	     (region-beginning)
   	     (region-end))
   	  (let ((sym (thing-at-point 'symbol)))
   	    (when (stringp sym)
   	      (regexp-quote sym))))
   	regexp-history)
     (call-interactively 'occur))
   (global-set-key (kbd "C-c C-o") 'occur-dwim)
   ```

   光标放在字符上, `C-c C-o` 直接**提取搜索**

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200429002538.png)

   tips: `C-x o`窗口跳转    `M-x occur-edit-mode` or `e`直接编辑  `C-c C-c` 退出编辑

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200429003515.png)

2. improve imenu

   ``` elisp
   (defun js2-imenu-make-index ()
     (interactive)
     (save-excursion
       ;; (setq imenu-generic-expression '((nil "describe\\(\"\\(.+\\)\"" 1)))
       (imenu--generic-function '(("describe" "\\s-*describe\\s-*(\\s-*[\"']\\(.+\\)[\"']\\s-*,.*" 1)
   			       ("it" "\\s-*it\\s-*(\\s-*[\"']\\(.+\\)[\"']\\s-*,.*" 1)
   			       ("test" "\\s-*test\\s-*(\\s-*[\"']\\(.+\\)[\"']\\s-*,.*" 1)
   			       ("before" "\\s-*before\\s-*(\\s-*[\"']\\(.+\\)[\"']\\s-*,.*" 1)
   			       ("after" "\\s-*after\\s-*(\\s-*[\"']\\(.+\\)[\"']\\s-*,.*" 1)
   			       ("Function" "function[ \t]+\\([a-zA-Z0-9_$.]+\\)[ \t]*(" 1)
   			       ("Function" "^[ \t]*\\([a-zA-Z0-9_$.]+\\)[ \t]*=[ \t]*function[ \t]*(" 1)
   			       ("Function" "^var[ \t]*\\([a-zA-Z0-9_$.]+\\)[ \t]*=[ \t]*function[ \t]*(" 1)
   			       ("Function" "^[ \t]*\\([a-zA-Z0-9_$.]+\\)[ \t]*()[ \t]*{" 1)
   			       ("Function" "^[ \t]*\\([a-zA-Z0-9_$.]+\\)[ \t]*:[ \t]*function[ \t]*(" 1)
   			       ("Task" "[. \t]task([ \t]*['\"]\\([^'\"]+\\)" 1)))))
   (add-hook 'js2-mode-hook
   	  (lambda ()
   	    (setq imenu-create-index-function 'js2-imenu-make-index)))
   (global-set-key (kbd "C-c C-i") 'counsel-imenu)
   ```

   `C-c C-i` 显示函数名, 函数outline

###  expand-region, and iedit mode

1. expand-region

   ``` elisp
   (global-set-key (kbd "C-=") 'er/expand-region)
   ```

   `C-=` 选中

2. iedit

   ``` elisp
   (global-set-key (kbd "C-c C-e") 'iedit-mode)
   ```

   `C-c C-e` 进入iedit-mode   再按`C-c C-e` 退出iedit-mode

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200429005932.png)

   tips: 1. `C-c C-o`提取搜索  2. `e` 进入编辑模式 3. `C-c C-e` 匹配编辑 4. 同时编辑匹配项目 5. `C-c C-c` 退出编辑模式

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200429011019.png)

### Bonus Time. Org export

`C-c C-e` export to html, you could also export to pdf  

### Exercise

1. Learn how to use emmet-mode to do [zen coding](https://github.com/smihica/emmet-mode)
2. configure your system to export org file to pdf file
3. install multiple cursor mode and compare it with iedit mode