# auto-capitalize.el

Capitalize char automatically on Emacs.
This package was forked from [emacswiki](http://www.emacswiki.org/emacs/auto-capitalize.el) to use [skk(ddskk)](http://openlab.ring.gr.jp/skk/ddskk.html).

### Installation

If you use el-get you can add recipe to el-get-source following code:

    (push '(:name auto-capitalize
            :type github
            :pkgname "yuutayamada/auto-capitalize-el")
           el-get-sources)

And then load this package after execute *M-x el-get-install RET auto-capitalize*

    (require 'auto-capitalize)

### Configuration Examples


```lisp
(setq auto-capitalize-words `("I" "English"))
(add-hook 'after-change-major-mode-hook 'auto-capitalize-mode)
```

or


```
;; This configuration adds capitalized words of .aspell.en.pws
;; (aspell's user dictionary)
(require 'auto-capitalize)
(setq auto-capitalize-words `("I" "English"))
(setq auto-capitalize-aspell-file "path/to/.aspell.en.pws")
(auto-capitalize-setup)

```

