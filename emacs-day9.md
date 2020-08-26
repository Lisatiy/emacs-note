## [day9](https://emacs-china.org/t/21-emacs-macro-use-package/416)

### What is macro?

Code which generate code?
Write macro is almost the same as writing function in elisp.

### What's the different between function and macro?

1. Evaluation: the macro arguments are the actual expression appearing in the macro call.
2. Expansion: the value returned by the macro body is an alternate Lisp expression, also known as the expansion
3. examples

