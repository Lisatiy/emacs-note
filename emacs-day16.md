## [day16](https://emacs-china.org/t/topic/784) - [outline](https://github.com/emacs-china/Spacemacs-rocks/tree/master/Season2/day16)

Topic: Ctags and company mode for auto completion

### Why use Ctags for auto completion?

1. Some dynamic languages don’t support syntax-aware auto completion.

For exampel:

Javascript (though tern-mode could do some sort of auto completion, but the configuration is complex and it’s not always reliable) && Lua

I also use Ctags for C/C++, I usually use Emacs for **writing and navigating** C/C++ code, but use IDE to debug and profiling. **emacs 用来浏览代码**

1. Ctags is very fast and reliable.

### How to configure ctags and auto completion?

ctags -eR . company-etags (company-etags can’t used for every major mode)

How to use Ctags effectively?

1. project wide configurations for auto generating the Tags file.
2. Configure the ctags rules for generate more tags
3. use etags-select to quickly navigate a large code base

首先新建一个 testJs-ctags 目录, 然后在该目录下新建 a.js 以及 b.js 两个文件:

```cmd
mkdir testJs-ctags
cd testJs-ctags
touch a.js
touch b.js
```

然后编辑 a.js 的内容如下:

```js
var func1 = function () {
    console.log("func1");
};

var func2 = function () {
};
```

然后在 b.js 中的补全中可以显示处 func1 和 func2 的补全提示的. 为了更方便的讲解之后的内容, 我们可以查看使用的补全的后端: 输入 `M-x, diminish-undo`, 选择 `company-mode`, 这样在 modeline 就可以看到 company-mode 的具体信息.

再次输入 `fun` 等待弹出补全提示, 在补全选项中上下移动, 可以看到使用的补全后端包括 dabbrev-code 和 etags 等, 如果我们`SPC b k b.js`关闭 a.js 的 buffer, 再次输入 `fun` , 可以看到使用的补全后端为company-keywords, 而输入 `func1` 和 `func2` , 则不会出现补全选项.

在之前的操作中, 我们并没有生成 ctags, 为什么也能使用 ctags 补全呢? 我们可以使用 `SPC h d v`, 然后输出 tags-table-list 来查看该变量的值, 当前的值是指向作者 cocos目录下的 TAGS 文件. 使用以下代码清空该值:

```
(setq-default tags-table-list nil)
```

然后再次尝试输入 `fun` 补全, 这时就不会使用 ctags 补全了, 使用的补全后端为company-keywords, 

那么如何生成 ctags 补全的文件呢? 使用以下命令即可:

```cmd
cd testJs-ctags
ctags -e a.js		# -e 是生成Emacs能够识别的ctags
# 针对目录生产ctages
# ctags -eR foldername
```

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588403175257.png)

`company-etags` 在进行补全的时候, 会从变量 tags-table-list 值的文件列表中去查找 tags, 而且 tags 是不区分语言的.

如果需要手动加载 TAGS 文件, 那么可以调用 `M-x visit-tags-table` 命令. 而在打开一个文件时, ctags 会从文件所在的目录进行查找, 一直到根目录, 加载所找到的 TAGS 文件, 如下 `SPC h d v describe variable: tags-table-list`.

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588403405173.png)

### 如何高效的使用 ctags

#### 自动重新生成 TAGS 文件

在使用 ctags 的过程中, 如果文件的内容被改变, 那么需要重新生成 TAGS 文件, 以便 ctags 的补全结果更精确. 作者实现了一个函数来自动加载必须的 TAGS 文件:

```emacs lisp
(add-hook 'js2-mode-hook 'my-setup-develop-environment) ;; 在js2-mode下面添加一个hook
(defun my-setup-develop-environment ()
  (interactive)
  (when (my-project-name-contains-substring "guanghui") ;; 当前buffer的路径里面包含guanghui, 说明在我的home目录下面
    (cond
     ((my-project-name-contains-substring "cocos2d-x")
      ;; 如果文件路径里面包含cocos2d-x, 自动把tags-table-list设置为~/cocos2d-x/cocos目录下面的tags文件. 解决了第一个步骤, 自动生成tags文件 C++ project don't need html tags
      (setq tags-table-list (list (my-create-tags-if-needed "~/cocos2d-x/cocos"))))
     ((my-project-name-contains-substring "Github/fireball")
      (message "load tags for fireball engine repo...")
      ;; html project donot need C++ tags
      (setq tags-table-list (list (my-create-tags-if-needed "~/Github/fireball/engine/cocos2d")))))))
```

另一个步骤是绑定快捷键, 当文件更改太多tags不满足自己的要求了时的重新生成 TAGS: `SPC o c` . 避免自动保存时生成tags, 因为生成tags是一个耗时的操作, 只有自己想重新生成时才生成. 

```elisp
(defun my-auto-update-tags-when-save (prefix)
  (interactive "P")
  (cond
   ((not my-tags-updated-time)
    (setq my-tags-updated-time (current-time)))

   ((and (not prefix)
	 (< (- (float-time (current-time)) (float-time my-tags-updated-time)) 300))
    ;; < 300 seconds
    (message "no need to update the tags")
    )
   (t
    (setq my-tags-updated-time (current-time))
    (my-update-tags)
    (message "updated tags after %d seconds." (- (float-time (current-time)) (float-time my-tags-updated-time))))))
```

#### 配置规则来生成更多的 TAGS

ctags 自身也有一个配置文件, `SPC f f` find files or url: `/User/guanghui/.vim/.ctags`(作者的路径, 是一个符号链接, 会链接到home目录的.ctags文件) 可以在该文件中定义规则来更好的生成 TAGS, 一个配置文件的示例如下:

```elisp
;; 忽略掉一些路径
--exclude=*.svn*
--exclude=*.git*
--exclude=*tmp*
--exclude=.#*
--tag-relative=yes
--recurse=yes ;; 是否需要递归

;; 那些文件属于js文件
--langdef=js
--langmap=js.js
--langmap=js:+.jsx

;; 定义匹配规则: 什么时候生成ctags  自己的提取规则
;; \1 第一个capture group
;; /[ \t.]([A-Z][A-Z0-9._$]+)[ \t]*[=:][ \t]*([0-9"'\[\{]|null)/ 匹配规则
--regex-js=/[ \t.]([A-Z][A-Z0-9._$]+)[ \t]*[=:][ \t]*([0-9"'\[\{]|null)/\1/n,constant/

--langdef=css
--langmap=css:.css
--regex-css=/^[ \t]*\.([A-Za-z0-9_-]+)/.\1/c,class,classes/
```

在配置文件中可以使用 –exclude 来忽略文件或路径, 使用 –langdef 来定义哪些文件属于 js 文件, 使用 –regex-js 来定义 TAGS 生成时的匹配规则. 这些匹配规则中可以使用正则表达式来提取内容生成 TAGS.

#### 使用 etags-select 来浏览项目

在有 TAGS 之后, 可以使用 ctags 来方便的浏览文件内容.  例如在某个函数名上点击 `, g`, 然后选择 `d etags-select-find-tag-at-point`, 这时会把所有相关的内容列出到 buffer 中, 然后可以按数字选择想要跳转的位置跳转过去.

![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588404977845.png)

## Final thoughts

When syntax-aware auto completion is not available, consider to use Ctags instead.

在org-mode中, 使用`M-x hippie-expand`而不是 `M-x company-etags`