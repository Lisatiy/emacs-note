## [day10](https://github.com/emacs-china/Spacemacs-rocks/issues/87)

### How company-mode works?

1. backend for the completion sources and front end to display the condidates
2. `C-h v` company-backens
3. try company-file and company-ispell, M-x
4. C-h C-f to view the backend implementation

### Why my company suck?

1. Python anaconda-mode not works
2. some backend require build with a server-client architecture: company-anaconda, company-jedi, company-ycmd, company-tern etc
3. At first, you should make sure the server side is working properly and then you want to make sure you use the right backend
4. how to fix anaconda on Mac

### Group backend

1. if you use want to use etags for completion and you should generate tags first and use company-etags backend.
2. group company-dabbrev-code and company-etags, and another company-dabbrev backend?
3. company-keywords for lua
4. sort by statistics

### Write a Simple company backend

[detail](http://sixty-north.com/blog/writing-the-simplest-emacs-company-mode-backend)

### reference

[ref1](http://sixty-north.com/blog/series/how-to-write-company-mode-backends)

[ref2](https://www.emacswiki.org/emacs/CompanyMode)