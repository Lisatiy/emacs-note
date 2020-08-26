## [day18](https://emacs-china.org/t/21-emacs-18/946) - [outline](https://github.com/emacs-china/Spacemacs-rocks/tree/master/Season2/day18)

Topic: How to survive in Spacemacs

### I want a feature from other editors, How could I implement it in Emacs?

<https://emacs-china.org/t/spacemacs-sublime-ctrl-d/902>

`S-d S-d S-d S-r S-f` 编辑多处内容  **Super是command键** `C-h C-f` 跳转到函数

### Emacs don’t behavior like the other editors I used before

<https://emacs-china.org/t/emacs/905>

1. Some defaults are worth learning, but some are not
2. Vim的normal模式时候浏览代码和进行小的代码修改, 大量的文字编辑在insert模式下

Ask in emacs-china.org

1. Stick to the defaults will help in the long run
   比较常用的文字编辑的快捷键定义到insert模式下面, 浏览代码和不经常用的定义到 `SPC o` 快捷键上

I think Mac is the best platform. You could easily adapt yourself to Emacs (CMD A/C/X)

### I have a full time job, I can’t bear the efficiency lose when editing with Emacs/Spacemacs

I want to setup a IDE to do the job for me.

Suggestions:

1. **C/C++/Java/C# IDE is not worth the time**
2. Javascript/HTML/CSS don’t need a IDE
3. **Python**/Ruby/Go/PHP/Clojure/Erlang could have **some IDE feature(补全, 不能调试)** in Emacs

In the first beginning, try to use the right tool for the right job.

Now: I’m using XCode for C++/OC programming, Android Studio for Java programming. (No plugin, no keybindings change)

I also use iTerm2/**tmux** for the shell stuff, the shell in Emacs is slow…

### Don’t try to make the perfect GTD tool with Org-mode

It’s very hard for beginners, I also spent too much time to configure the workflow I’m using now.

Learn Org-mode feature step by step, **don’t try to become the master in the first day**.

### Some tips for beginners to avoid common issues

1. my emacs is frozen, how?

Because Emacs is a single thread app, sometimes you just trigger some time consuming task.

命令行中输入

```cmd
pkill -SIGUSR2 -i emacs
```

出现调用推栈, 可以看出问题出在哪了![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588420568419.png)

然后 `M-x toggle-debug-on-quit` 取消这个堆栈的影响, 后续操作(如`C-g C-g`)不会被打断

2. My Emacs is very slow

Use the following two commands to profile the CPU

```elisp
M-x profiler-start ;; 查看CPU的消耗
```

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588420895735.png)

1. My Emacs start-up time is long…

   命令行中输入

```cmd
/Applications/Emacs.app/Contents/MacOS/Emacs --timed-requires --profile
```

可以看到启动的消耗主要在哪里

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588421041450.png)

`SPC b b load-times` 查看时间消耗, 根据这些可以优化自己的emacs

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588421180427.png)

### I have lots unknown of Emacs..

1. Take it easy and don’t panic, Emacs is a lifelong text editor
2. Learning Emacs one piece a time everyday.
3. Visit reddit/emacs-china.org regularly for keeping update with the community
4. Keep using Emacs daily and reshaping your **secret weapon** gradually.