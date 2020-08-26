## day3

### Split your configs into multiple files

1. use Git to management your init file

   * 初学者可以同步init.el和elpa, 防止elpa更新而出错

   * `git st` 和 `git d` 显示修改的内容

   * git throw放弃修改的内容 `M-x global-auto-composition-mode` emacs重新加载文件 

     ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428151050.png)

   * 去掉[auto-save-list](https://emacsredux.com/blog/2013/05/09/keep-backup-and-auto-save-files-out-of-the-way/)

     ``` elisp
     (setq auto-save-default nil)
     ```

     `rm -rf auto-save-list/` 删除auto-save-list文件

   * 修改.gitignore

     * `git add .gitignore`
     * `git ci -m 'add gitignore'`

2. help window is anoyying

   ```elisp
   (require 'popwin)
   (popwin-mode 1)
   ```

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428153458.png)

   对比company-mode不需要require，原因是 `C-h C-f`跳转到global-company-mode定义函数，有魔法注释(;;;###autoload)

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428155118.png)

3. load-file, load-path and load

4. features, provide and require, autoload
   看[Xah Lee](http://ergoemacs.org/emacs/elisp_library_system.html)的教程

5. naming conventions 
   all of names should be a prefix, such that the naming conflicts could be minimal.

   ```emacs
   #自定义变量可以使用自己的名字作为命名方式（可以是变量名或者函数名）
   my/XXXX
   #模式命名规则
   ModeName-mode
   #模式内的变量则可以使用
   ModeName-VariableName
   ```

6. define your abbrevs

   ``` elisp
   (define-abbrev-table 'global-abbrev-table '(
   					    ;; signature
   					    ("8lsf" "lisatiy")
   					    ;; Winsoft
   					    ("8ws" "winsoft")
   					    ))
   ```

   输入`8lsf`, 按空格, 补全`lisatiy`; 输入`8lsf`, 按`/`, 补全`lisatiy/`; 输入`8lsf`, 遇到非字母就好补全

7. how to organize your configs

   * init-packages.el
   * init-ui.el
   * init-better-defaults.el
   * init-keybindings.el
   * custom.el

8. use 'counsel-git' to find file in git managed project.

   ``` elisp
   (global-set-key (kbd "C-c p f") 'counsel-git)
   ```

   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/20200428173324.png)

### Major mode and minor mode in details

1. conventions
   text-mode/special-mode/prog-mode
   naming: xxx-mode, xxx-mode-key-map(快捷键), xxx-mode-hook
2. mode key map and mode hook
3. let's take a look at a package in elpa (company)

### Better defaults

1. disable audio bell

   ``` elisp
   (setq ring-bell-function 'ignore)
   ```