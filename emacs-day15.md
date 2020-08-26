## [day15](https://emacs-china.org/t/21-emacs-15/745) - [outline](https://github.com/emacs-china/Spacemacs-rocks/tree/master/Season2/day15)

Topic: **Window**, **project** and **layout** operations

### Layout related operations 

(有点类似于工作区间来区分不同的项目的状态) 

1. What’s layout in spacemacs? How to use layout in spacemacs?
   在dotspacemacs-configuration-layers里面添加

   ``` elisp
   (spacemacs-layouts :variables layouts-enable-autosave nil                       		layouts-autosave-delay 300) 
   ```

   `SPC o l l` -> zilongshanren/load-my-layout 加载自己定义的layout
   `SPC l l` 列出自己的layout列表, 点击相应的layout, 进入上次自己hacking时保存的文件

2. `SPC l L` load layout file

3. `SPC l l` 或者 `SPC l 数字` to switch between layouts

4. `SPC l s` to save layout to file

5. `SPC l <tab>` switch between the last layout and the current layout

6. `SPC l o` custom layout
   自己custom了org, Cocos2d-X和Spacemacs三个layout
   以cocos2d-x-lite为例, 自己的定义如下
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588394765832.png)
   则可以这样操作:

   1. `SPC l l` layout->cocos2d 进入该layout
   2. `SPC l o c` 则打开UIWidget.cpp这个文件

7. `SPC l R` rename layout

8. `SPC l ?` to open the help window, learn more operations about laout 再按下`?`退出帮助窗

tips: 添加新的layout, 如添加blog的layout

1. `SPC p l` switch to Project Perspective `~/4gamers.cn`, find file 进入git文件, 创建一个 project layout, 如下
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588394144634.png)
   
   `SPC p l` 就是新打开一个**以目录命名的layout**中的文件，注意这个文件得有git管理
   
2. `SPC l l` 进入 `~/4gamers.cn` 的layout
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588394218452.png)

3. `SPC l R` 进行new name: `blog`
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588393009401.png)

4. `SPC o l s` 把layout信息保存到zilong里面

5. 重新打开emacs, `SPC o l l` **加载之前保存的layout**

6. `SPC l l`  发现有blog了, 如下
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588393210223.png)

7. `SPC p f` find file 可以看到blog对应目录里面的文件了
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588393267239.png)

8. `SPC l l` 切换到engine, 发现是自己之前保存的3个buffer的状态
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588393447583.png)

### Window related operations

1. `SPC w -` split window blew
2. `SPC w /` split window right
3. `SPC w .` window micro state 在下面一个小窗口, 可以依照这些提示对窗口进行操作
   ![](https://cdn.jsdelivr.net/gh/lisatiy/picbed-lisatiy@master/img/2020/1588395308592.png)
4. `SPC w 2/3` use predefined window layout
5. `SPC w =` balance window 均等分
6. `SPC w b` switch to minibuffer
7. `SPC w d` delete the current window
8. `SPC w h/j/k/l` move to window
9. `SPC w m` maximize window
10. `SPC w H/J/K/L` **move** window to position with evil direction key
11. `SPC w u/U` window undo/redo
12. `SPC w o` switch to other frame
13. `SPC w F` make a new frame 双屏幕可以使用, 尽量不要用, 可能有未知bug
14. `SPC w 1/2/3/4` goto window with window number
15. `SPC w w` go to other window one by one
16. `SPC w W` ace window 用字母标识窗口
17. `SPC t g` toggle golden ratio 黄金分割来区分当前窗口
18. `SPC t -` center point 光标上下移动时永远在buffer的正中央

### project related operations

1. `SPC p f` find file    visit files in project
2. `SPC p b` visit buffers in project(已经打开过的git项目)
3. `SPC p p` switch to project 在已经打开的git项目间进行切换 
4. `SPC p l` switch to project and create a new layout
5. `Super f` find-file-in-project is a really handy package (可以看到隐藏文件)

Fore more about the project related operations, dig into it with which-key.