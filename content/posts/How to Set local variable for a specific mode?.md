+++
title = "How to set local variable for a specific mode?"
author = ["Anak Wannaphaschaiyong"]
draft = false
+++

This type of tutorial/question is best to present with an example.
Given that I want to set `compile-command` variable for LaTex mode which applies to all buffer of this mode.

```emacs-lisp
(defun set-compile-command-default-in-LaTeX-mode ()
  (set (make-local-variable 'compile-command) ;; create local variable specific to a current buffer
       (format "" (buffer-file-name))))

(add-hook 'LaTeX-mode-hook
          'set-compile-command-default-in-LaTeX-mode)
```
