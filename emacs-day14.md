## [day14](https://emacs-china.org/t/21-emacs-14/738) - [outline](https://github.com/emacs-china/Spacemacs-rocks/tree/master/Season2/day14)

Topic: File and Buffer operations

### Talk the difference between the configs of mine and spacemacs

1. 自己打造的mode-line
2. 排除了大量的package

### File related operations

1. `SPC p f` (find a file in current project, it looks like the Ctrl-p plugin in Vim)

I also do some hacks to enhance the `SPC p f`

```elisp
(defun zilongshanren/open-file-with-projectile-or-counsel-git ()
  (interactive)
  (if (zilongshanren/vcs-project-root)
      (counsel-git)		;; 如果在git项目里面使用counsel-git查找文件
    (if (projectile-project-p)
        (projectile-find-file)
      (ido-find-file)))) 
```

If it is in a Git repository, I use `counsel-git` to find file. Why not projectile? Becuase I think ivy-mode is much faster. If it is in a proctile project, say it has a `.projectile` file in your project’s root. Otherwise, you `ido-find-file`

1. `SPC f f` to find a file start from the current directory    `C-h` 返回上级目录
2. `SPC f L` find the file across the **whole Mac system**
3. `SPC f l` find file literally(I also enhance this func with ffap)
   使用literally方式打开不会附加任何编码信息
   `SPC : ffap` 使用utf-8格式打开
4. `SPC f h` find file in hex mode(使用十六进制格式打开) (I also enhance this func with ffap)
   `C-c C-c` 回到之前的模式, 若返回到了`fundamental`模式打开的文件,  `M-x org-mode` 使用org-mode模式打开文件, `M-x set-buffer-coding-system -> utf-8` 设置utf-8格式
5. `SPC f o` open with external program 使用外部程序打开文件
6. `SPC f E` sudo edit
7. `SPC f D` delete current file and buffer
8. `SPC f j` open the current file’s dired mode 
9. `SPC f r` find the recent file with ivy
10. `SPC f R` rename the current file
11. `SPC f v` **add local variables**
    在项目目录下添加一个.dir-locals.el的文件, 可以对项目做一些特殊的设置. 执行该项目下的buffer时都会执行该.dir-locals.el里面的命令
12. `SPC f y` yank current buffer’s full path
    `p` 粘贴得到的文件的全路径
13. `SPC f a d` find the current visited directory with **fasd**(chenbin).
    访问最近常用的目录
14. `SPC f C d/u` convert file encoding between unix and dos 转换文件编码
15. `SPC f e d` find the .spacemacs/.spacemacs.d/init.el file
16. `SPC f e i` find the .emacs/.emacs.d/init.el init file
17. `SPC f e l` helm locate library file 打开系统上安装的.el文件
18. `SPC f c` copy file
19. `SPC f b` show bookmarks
20. `SPC f s/S` save buffers

### buffer related operations

1. `SPC b .` buffer micro state (**hydra**) 切换next或previousbuffer, 按`J K` micro state会退出

2. `SPC b b` switch buffers(启动后打开的所有buffer), i rebind it to `ivy-switch-buffer`, because I could see recent use file in buffer

3. `SPC b d` kill a buffer

4. `SPC b f` find buffer file in finder (只能在Mac使用)

5. `SPC b B/i` I bind it to ibuffer

   类似于dired-mode, 可以进行与dired-mode类似的操作
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588388166408.png)

6. `SPC b h` go to home

7. `SPC b k` kill matching buffers 如输入helm, 则所有有关helm的buffer被kill

8. `SPC b N` new empty buffer 新建buffer

9. `SPC b m` kill others buffer

10. `SPC b R` safe revert buffer 意外退出后, 从自动备份的文件中还原文件

11. `SPC b s` switch to scratch buffer

12. `SPC b w` toggle buffer read-only

13. `SPC b Y` **copy the whole buffer to clipboard**, the content could be used in other programs

14. `SPC b P` paste to the whole buffer

15. `SPC <tab>` **switch between the current buffer and the last opened buffer**

### Sometimes I also use the `Dired` mode to do all the files operations

I think I have talked about it in the previous videos.

### Happy hacking!

`SPC 2` 分两个窗口