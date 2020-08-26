# spacemacs-win10

## [emojify](https://github.com/iqbalansari/emacs-emojify)

1. `M-x customize-group` -> `emojify` -> emojify emoji set -> emojione-v2.2.6-22
2. 从网上下载[emojione-v2.2.6-22](https://github.com/plexus/.emacs.d) , 放到~/.cache/emojify/emojione-v2.2.6-22

## modeline-待解决

``` elisp
;; '(:eval (lisatiy/modeline-winum-mode))
'(:eval (winum-get-number-string))
```

怎么展示第二格的modeline

``` elisp
'(:eval (lisatiy/modeline--evil-substitute))
'(:eval (lisatiy/update-persp-name))
```

# emacs-win10

## win10下出现中文字体很卡

在 init-ui.el 中设置中文字体

```elisp
(dolist (charset '(kana han cjk-misc bopomofo))
  (set-fontset-font (frame-parameter nil 'font) charset
                    (font-spec :family "微软雅黑" :size 20)))
```

参考:

1. [Spacemacs怎么单独设置中文的字体](https://emacs-china.org/t/spacemacs/1003)
2. [Windows10下Emacs只要有中文就非常卡](https://emacs-china.org/t/topic/992/1)

## mode-line

1. [all-the-icons](https://github.com/domtronn/all-the-icons.el/tree/0b74fc361817e885580c3f3408079f949f5830e1)
   需要将下载的fonts中的ttf字体文件放入c:/windows/fonts文件夹
2. [doom-modeline](https://github.com/seagle0128/doom-modeline)

