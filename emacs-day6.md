## [day6](https://emacs-china.org/t/topic/74)

### Bonus Time

1. Use org-capture to take notes
2. gtd

```elisp
;; 在mac上抓取当前网页的URL
(defun zilongshanren/insert-chrome-current-tab-url()
  "Get the URL of the active tab of the first window"
  (interactive)
  (insert (zilongshanren/retrieve-chrome-current-tab-url)))

(defun zilongshanren/retrieve-chrome-current-tab-url()
  "Get the URL of the active tab of the first window"
  (interactive)
  (let ((result (do-applescript
		 (concat
		  "set frontmostApplication to path to frontmost application\n"
		  "tell application \"Google Chrome\"\n"
		  "	set theUrl to get URL of active tab of first window\n"
		  "	set theResult to (get theUrl) \n"
		  "end tell\n"
		  "activate application (frontmostApplication as text)\n"
		  "set links to {}\n"
		  "copy theResult to the end of links\n"
		  "return links as string\n"))))
    (format "%s" (s-chop-suffix "\"" (s-chop-prefix "\"" result)))))
(setq org-capture-templates
      '(("t" "Todo" entry (file+headline "~/.emacs.d/gtd.org" "工作安排")
	 "* TODO [#B] %?\n  %i\n"
	 :empty-lines 1)
	("c" "Chrome" entry (file+headline "~/.emacs.d/gtd.org" "Quick notes")
               "* TODO [#C] %?\n %(lisatiy/retrieve-chrome-current-tab-url)\n %i\n %U"
               :empty-lines 1)
	))
;; r aka remember
(global-set-key (kbd "C-c r") 'org-capture)
```

* `C-c r t` 编辑工作安排todo事项 `C-c r c` 编辑带链接的todo事项 `C-c C-c` finish `C-c C-k` 退出 [Further reading](https://orgmode.org/manual/Capture.html)
  [中文输入编码](http://ergoemacs.org/emacs/emacs_encoding_decoding_faq.html)

  ```elsip
  ;; UTF-8 as default encoding
  (set-language-environment "UTF-8")
  ```

* Install Org pomodoro to track my time
  `C-c a a` 启动gtd  `M-x org-pomodoro`  开启番茄时间

### Clean up configs

1. move keybindings into one place

2. make c-n and c-p to select company condicate

   ``` elisp
   (with-eval-after-load 'company
     (define-key company-active-map (kbd "M-n") nil)
     (define-key company-active-map (kbd "M-p") nil)
     (define-key company-active-map (kbd "C-n") #'company-select-next)
     (define-key company-active-map (kbd "C-p") #'company-select-previous))
   ```

### Batch rename files

1. `C-x C-j` 跳转到dired mode目录 `Shift-6` 跳转到上一级目录
2. press `C-x C-q` in dired mode
3. use expand-region(`C-=`) and iedit(`C-c C-e`) to batch change files
4. finish `C-c C-c`

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200429090544.png)

### Search and replace

* install helm-ag 

  at first, you should install [ag for win10](https://github.com/JFLarvoire/the_silver_searcher/releases)
  search speed: ag > pt > ack > grep

  ``` elisp
  ;; 添加自己的ag路径
  (let ((lisatiy-path "c:/Program Files/ag_win64/"))
  (setenv "PATH" (concat lisatiy-path ":" (getenv "PATH"))) ; Assume ":" is the separator
    (add-to-list 'exec-path lisatiy-path))
;; 让ag支持中文
  (defun lisatiy/helm-ag-gbk (&rest args)
  (set-terminal-coding-system nil)
    (set-keyboard-coding-system nil)
  (set-language-environment 'chinese-gbk))
  (advice-add 'helm-do-ag :before #'lisatiy/helm-ag-gbk)
(global-set-key (kbd "C-c p s") 'helm-do-ag-project-root)
  ```

  `C-c p s`  项目中搜索 
  
  ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200429113046.png)
  
  结合 **org** 和 **gtd** 搜素, 排除有 **setq** 的选项
  
  ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200429114121.png)
  
  `C-c C-e` 打开buffer, 可以直接编辑搜素的结果 C-= 选择region `C-c C-e` iedit匹配编辑 `C-c C-c` finish
  
  ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200429102008.png)

### Show javascript errors with flycheck

1. flycheck-checkers

   ``` elisp
   (add-hook 'js2-mode-hook 'flycheck-mode)
   ```

2. eslint

   ``` cmder
   npm install -g eslint
   ```

### Snippets and auto snippet

``` elisp
(require 'yasnippet)
(yas-reload-all)
(add-hook 'prog-mode-hook #'yas-minor-mode)
```

TAB 在js文件中补全

* auto-yasnippet
  1. (add-to-list~AA 'path~AA 'xxx~AA)
  2. `M-x aya-create`
  3. `M-x aya-expand` 
  4. (add-to-list**BB** 'path**BB** 'xxx**BB**) 自己定义~后的内容

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200429110023.png)

### Exercises

1. give [helm-swoop](https://github.com/emacsorphanage/helm-swoop) package a try
2. give [org-mac-link](https://melpa.org/#/org-mac-link) package a try