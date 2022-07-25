+++
title = "X Implementation Where X = Doom Emacs's +lookup/ Command."
author = ["Anak Wannaphaschaiyong"]
tags = ["blog", "lookup", "doom"]
draft = false
+++

I was trying to figure out `+lookup/definition` that open in other window. In one of the issue, Henrik&nbsp;[^fn:1] mention that some `lookup` backend (As an example, `xref` is a built in backend for lookup) are asynchronous and there is no standardized mechanism to talk to them to see whether the command runs successfully&nbsp;[^fn:2].

lets call this new command `+lookup/definition-other-window`
Current possible solutions are

1.  ignore validation step to make sure that the command runs succesfully.
2.  when the command is called, switch to other window then run `+lookup/definition` command.
    It can be implemented as followed
    ```emacs-lisp
       (dolist (fn '(definition references))
         (fset (intern (format "+lookup/%s-other-window" fn))
               (lambda (identifier &optional arg)
                 "TODO"
                 (interactive (list (doom-thing-at-point-or-region)
                                    current-prefix-arg))
                 (let ((pt (point)))
                   (switch-to-buffer-other-window (current-buffer))
                   (goto-char pt)
                   (funcall (intern (format "+lookup/%s" fn)) identifier arg)))))
    ```

I just thinks its interesting, so I figure I write something about it.

That's it.
Peace.

[^fn:1]: Henrik is a creator of Doom Emacs.
[^fn:2]: <https://github.com/doomemacs/doomemacs/issues/3397#issuecomment-649124705>
