## [Oday17](https://emacs-china.org/t/21-emacs-17-lispy/827) - [outline](https://github.com/emacs-china/Spacemacs-rocks/tree/master/Season2/day17)

Topic: How to use [Lispy](https://github.com/abo-abo/lispy/tree/1abfd85f959a2a3cd5c2806b2837990ec671fe7c) to write lisp code (emacs-lisp/clojure/clojurescript/scheme/common lisp etc)

## Introduction to Lispy

1. vim like Paredit: [function reference](http://oremacs.com/lispy/)
2. It even has some IDE features
3. how to install

## Basic usage of Lispy

1. barf and slurp
   把text-mode放到括号里面 `[ d >`   再移出去 `<`
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588405790394.png)
2. raise sexp
   把横线上面的判断去掉 `r`  
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588406043398.png)
3. kill/copy/yank
   `k` 删除内容后会保证括号匹配
   `m` 标记表达式 `Alt w` 拷贝 `DEL` 删除 `C-y` 粘贴  `n` new-copy `C-y` 粘贴 `c` 克隆一个一模一样的表达式出来 
4. ace
   `d` 光标在括号左右跳动 括号出按`a`, 符号高亮显示 `i` 选中 Source Code Pro `i` 光标跳到其内部, 进行操作 
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588406680194.png)
5. swap/w/s
   `w` text-mode 和spacemacs/system-is-mac上下互换 `s` 再互换回去
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588406926342.png)
6. navigation hjkl/[]
   hjkl在表达式之间跳转  []定位不同表达式的括号
   `C 1` 显示当前函数的文档 在按`C 1`文档消失
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588407213224.png)
   `C 2` 显示该函数简单的用法
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588407291301.png)
7. split & splice
   `M j` 把text-mode和company-hook变成两个表达式
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588407445323.png)
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588407512794.png)
   再回去: `>` text-mode进去 `S-z` 取消选中 `S-j` 去掉text-mode的括号 `[` 跳转到括号 `o` 变成一行
8. wrap
   `S (` 直接给文本加上括号
9. 格式化代码 
   O 变成一行
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588407939511.png)
   M 变成多行
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588408015181.png)
10. debug
      `F` 跳转到定义 `i` evil-insert `d` special-lispy-different `x e` edebug  `]` 跳转到括号 `e` eval进入到定义 `n` 执行 再按`n`, 计算结果  再按`n`, 返回
      ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588418206525.png)
   

 