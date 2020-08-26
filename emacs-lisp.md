两种表示，一是表达式parenthesized expressions like `(+ 2 3)`；二是不在括号中的"atoms" that are not parenthesized: strings, numbers, symbols (like `'foo`),

```lisp
(setq foo "bar")	;  set two global variables, x=10 and total=0
(setq x 10
      total 0)  
(foo-bar "flim" "flam")
(% (* 15 (+ 8.2 (ls 7 3))))
```

experimenting Lisp in the "scratch" buffer     C-x C-e echo results into the minibuffer



注释

```lisp
(blah blah blah)   ; I am a comment
```



布尔值

> **t** is **trure**
> **nil** is **null**



List

```lisp
'(1 2 3)  ; produces the list (1 2 3) with no list-element evaluation
          ; apostrophe is shorthand for (quote (...))
`(1 ,(+ 1 1) 3)  ; another (1 2 3) via a template system called "backquote"
```



Pairs

link-list node struct (also known as a `cons` cell)

```lisp
(head-value . tail-value)
```

associative list (known as an `alist`)

```lisp
'( (apple . "red")
   (banana . "yellow")
   (orange . "orange") )
```

