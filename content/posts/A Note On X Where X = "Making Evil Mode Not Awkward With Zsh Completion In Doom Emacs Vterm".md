+++
title = """
  A Note On X Where X = "Making Evil Mode Not Awkward With Zsh Completion In Doom Emacs Vterm"
  """
author = ["Anak Wannaphaschaiyong"]
tags = ["vterm", "emacs", "blog", "note", "zsh", "doom", "evil-mode"]
draft = false
+++

Set pt value to pos fix awkward completion behavior in vterm.

```emacs-lisp
(defun vterm-goto-char (pos)
  "Set point to POSITION for vterm.

The return value is `t' when point moved successfully.
It will reset to original position if it can't move there."
  (when (and vterm--term
             (vterm-cursor-in-command-buffer-p)
             (vterm-cursor-in-command-buffer-p pos))
    (let ((moved t)
          (origin-point (point))
          pt cursor-pos succ)
      (vterm-reset-cursor-point)        ;; Anak: this line cause weird behavior with auto completion
      (setq cursor-pos (point))
      ;; (setq pt cursor-pos) ;; Anak commented out this line
      (setq pt pos)                     ;; Anak added this line and completion in vterm works better.
      (while (and (> pos pt) moved)
        (vterm-send-key "<right>" nil nil nil t)
        (setq moved (not (= pt (point))))
        (setq pt (point)))
      (setq pt (point))
      (setq moved t)
      (while (and (< pos pt) moved)
        (vterm-send-key "<left>" nil nil nil t)
        (setq moved (not (= pt (point))))
        (setq pt (point)))
      (setq succ (= pos (point)))
      (unless succ
        (vterm-goto-char cursor-pos)
        (goto-char origin-point))
      succ)))
```

If you `(vterm-reset-cursor-point)` position in normal mode will not be preserved when you call `(evil-collection-vterm-insert)`

That's it.

Peace.

~milfex-lostex
