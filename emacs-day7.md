## [day7](https://github.com/emacs-china/Spacemacs-rocks/issues/77)

### Tweak C-w to delete backward

``` elisp
(global-set-key (kbd "C-w") 'backward-kill-word)
```

### Evil! Turn Emacs into Vim in one second

1. install Evil plugin

   ``` elisp
   ;; Enable Evil
   (require 'evil)
   (evil-mode 1)
   ```

2. tell the different between Evil and Vim, [further detail](https://github.com/emacs-evil/evil) for PDF documents
   `C-d` 向下翻页 `C-u` 向下翻页(customize-group->evil->C U Scroll->Toggle on)

3. Evil state = Vim mode
   evil normal state
   evil insert state
   evil visual state `V`
   evil motion state
   evil emacs state
   evil operator state (dw)

4. configure Evil leader key

   ``` elisp
   (global-evil-leader-mode)
   (evil-leader/set-key
     "ff" 'find-file
     "fr" 'recentf-open-files
     "bb" 'switch-to-buffer
     "bk" 'kill-buffer
     "pf" 'counsel-git
     "ps" 'helm-do-ag-project-root
     "0" 'select-window-0
     "1" 'select-window-1
     "2" 'select-window-2
     "3" 'select-window-3
     "fj" 'dired-jump
     "w/" 'split-window-right
     "w-" 'split-window-below
     ":" 'counsel-M-x
     "wm" 'delete-other-windows
     "qq" 'save-buffers-kill-terminal
     "sj" 'counsel-imenu
     "sp" 'counsel-git-grep
     )
   ```

   `M-x customize-group`->evil-leader->Evil Leader->SPC
   `SPC f f` find file  `:q` 退出

5. press `C-z` to toggle between Normal and Emacs state

6. window-numbering
   `M-1` and `M-2`  分别跳转到1号和2号屏
   `:vsp` 垂直分屏

7. evil-surround
   hello `v i w`选中单词 + `S '` 在选中的单词周围上添加`'`号 'hello'  
   'hello' `c s ' "` 将`'`包围的单词的`'`替换为`"`   "hello"
   "hello"  `c-s " (` 变为 ( hello )     "hello"  `c-s " )` 变为 (hello)   

8. evil-nerd-commenter

   ``` elisp
   (evilnc-default-hotkeys)
   (define-key evil-normal-state-map (kbd ",/") 'evilnc-comment-or-uncomment-lines)
   (define-key evil-visual-state-map (kbd ",/") 'evilnc-comment-or-uncomment-lines)
   ```

   V 进入visual 模式, 选中, `,/` 注释, `g v`选中上一次选中的, `,/` 取消注释

9. Made some modes to use emacs-state
   某些模式不用normal state

   ``` elisp
   (dolist (mode '(ag-mode
   		flycheck-error-list-mode
   		occur-mode
   		git-rebase-mode))
     (add-to-list 'evil-emacs-state-modes mode))
   ```

10. binding `h/j/k/l` key

    ``` elisp
    (add-hook 'occur-mode-hook
    	  (lambda ()
    	    (evil-add-hjkl-bindings occur-mode-map 'emacs
    	      (kbd "/")       'evil-search-forward
    	      (kbd "n")       'evil-search-next
    	      (kbd "N")       'evil-search-previous
    	      (kbd "C-d")     'evil-scroll-down
    	      (kbd "C-u")     'evil-scroll-up
    	      )))
    ```

    `C-c C-o` occur-mode中可以使用evil的快捷键`h/j/k/l`

11. add this to ibuffer mode?

### Which key

``` elisp
(which-key-mode 1)
```

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200429180330.png)

### Design your own bingdings

1. Use SPC as the leader key
2. Use comma as the major leader key
3. Use SPC: to list all avialable commands
4. Use which key to group key bindings
5. Yeah! You got a minimal Spacemacs!

### Bouns Time: Search Org notes

`C-c a t` list to do  `C-c a s` 搜索

### Reference

[Evil](https://www.emacswiki.org/emacs/Evil)

### Exercises

Install hydra and begin to add your own hydras!