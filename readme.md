# auto-capitalize.el

Capitalize char automatically on Emacs.
This package was forked from [emacswiki](http://www.emacswiki.org/emacs/auto-capitalize.el) to use [skk(ddskk)](http://openlab.ring.gr.jp/skk/ddskk.html).

### INSTALLATION

If you use el-get you can add recipe to el-get-source following code:

    (push '(:name auto-capitalize
            :type git
            :url "https://github.com/yuutayamada/auto-capitalize-el.git"
            :load-path "./")
           el-get-sources)

And then load this package after execute *M-x el-get-install RET auto-capitalize* 

    (require 'auto-capitalize)

### CONFIGURATION EXAMPLE

You can use by M-x turn-on-auto-capitalize-mode or auto-capitalize-mode.
Although to motivate you, put my configuration.

    (eval-when-compile (require 'cl))
    (defvar programing-hooks
      ;; Add your preference programming mode hook like ruby-mode-hook
      '(emacs-lisp-mode-hook)) 

    (defvar my/programming-mode nil
      "Use this variable to know whether current major-mode is mode
      for programming. If it is non-nil mean the mode is mode for programming.")

    ;; Add hook to set t(rue) to my/programming-mode as a buffer local valuable
    ;; to prevent a turn on auto-capitalize-mode.
    (loop for hook in programing-hooks
          do (add-hook hook
                       '(lambda ()
                          (setq-local my/programming-mode t))))

    (defun my/switch-auto-capitalize-mode ()
      "turn on auto-capitalize-mode if it was comment line on 
      specific programming mode."
      (if my/programming-mode
          (if (equal font-lock-comment-face
                     (nth 1 (text-properties-at (point))))
              (turn-on-auto-capitalize-mode)
            (turn-off-auto-capitalize-mode))))

    (defadvice self-insert-command
      "turn on auto-capitalize-mode on specified programming mode"
      (around ad-turn-on-auto-capitalize activate)
      (unless (minibufferp)
        (my/switch-auto-capitalize-mode))
      ad-do-it)

    ;; Enable auto-capitalize-mode
    (add-hook 'text-mode-hook
              '(lambda ()
                 (turn-on-auto-capitalize-mode)))
