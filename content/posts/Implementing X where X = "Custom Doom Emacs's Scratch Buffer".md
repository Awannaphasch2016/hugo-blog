+++
title = """
  Implementing X where X = "Custom Doom Emacs's Scratch Buffer"
  """
author = ["Anak Wannaphaschaiyong"]
tags = ["doom", "blog", "implementation", "scratch", "module"]
draft = false
+++

I was trying to implement my own scratch buffer.I learned alot about Emacs's way of programming. I gained a new mental debugging tool.

The main function I started to modify is  `doom/open-scratch-buffer`. The functions deals with opening scratch buffer when current-buffer is inside and outside of a projectile's project.

`doom/open-scratch-buffer` does the following

-   check if scratch will open in the same buffer or as pop up buffer
-   Then, it passes arguments to `(doom-scratch-buffer &optional DONT-RESTORE-P MODE DIRECTORY PROJECT-NAME)`.

`doom-scratch-buffer` does the following

-   create buffer if the name doesn't already exist
-   restore existing buffer if buffer already opened by running `(doom--load-persistent-scratch-buffer project-name)`
-   add the scratch buffer to `doom-scratch-buffers`
-   add related hooks. then open the buffer.

I ended up copied code from `scratch.el` and modified it. Modification was pretty straight forward. First, I simplified arguments to pass as a way to poke the system to match my prediction of its behavior to its actual behavior.

I learned about how scratch page persist content. Content of doom scratch buffer is saved to `~/.emacs.d/.local/etc/scratch/__default.el` whenever its closed. To persist my scratch buffer content, I created `~/.emacs.d/.local/etc/scratch/__now-n-next.el` to use inplace of `~/.emacs.d/.local/etc/scratch/__default.el`.

After this step, I get the following code.

```emacs-lisp
(defun anak/open-scratch-buffer (&optional arg)
  "Pop up a persistent scratch buffer.

If passed the prefix ARG, do not restore the last scratch buffer.
If PROJECT-P is non-nil, open a persistent scratch buffer associated with the
  current project."
  (interactive "P")
  (let (projectile-enable-caching)
    (funcall
     #'pop-to-buffer
     ;; #'switch-to-buffer
     (anak/scratch-buffer
      arg
      'org-mode
      default-directory
      nil))))

(defun anak/scratch-buffer (&optional dont-restore-p mode directory project-name)
  "Return a scratchpad buffer in major MODE."
  (let* ((buffer-name "*anak:now-n-next*")
         (buffer (get-buffer buffer-name)))
    (with-current-buffer
        (or buffer (get-buffer-create buffer-name))
      (setq default-directory directory)
      (setq-local so-long--inhibited t)
      (if dont-restore-p
          (erase-buffer)
        (unless buffer
          (anak/load-persistent-scratch-buffer project-name)
          (when (and (eq major-mode 'fundamental-mode)
                     (functionp mode))
            (funcall mode))))
      (cl-pushnew (current-buffer) doom-scratch-buffers)
      (add-transient-hook! 'doom-switch-buffer-hook (anak/persist-scratch-buffers-h))
      (add-transient-hook! 'doom-switch-window-hook (anak/persist-scratch-buffers-h))
      (add-hook 'kill-buffer-hook #'anak/persist-scratch-buffer-h nil 'local)
      (run-hooks 'doom-scratch-buffer-created-hook)
      (current-buffer))))

(defvar anak/scratch-default-file "__now-n-next"
  "The default file name for a project-less scratch buffer.

Will be saved in `doom-scratch-dir'.")

(defun anak/persist-scratch-buffer-h ()
  "Save the current buffer to `doom-scratch-dir'."
  (let ((content (buffer-substring-no-properties (point-min) (point-max)))
        (point (point))
        (mode major-mode))
    (with-temp-file
        (expand-file-name (concat anak/scratch-default-file
                                  ".el")
                          doom-scratch-dir)
      (prin1 (list content
                   point
                   mode)
             (current-buffer)))))

(defun anak/load-persistent-scratch-buffer (project-name)
  (setq-local doom-scratch-current-project
              (or project-name
                  anak/scratch-default-file))
  (let ((smart-scratch-file
         (expand-file-name (concat doom-scratch-current-project ".el")
                           doom-scratch-dir)))
    (make-directory doom-scratch-dir t)
    (when (file-readable-p smart-scratch-file)
      (message "Reading %s" smart-scratch-file)
      (cl-destructuring-bind (content point mode)
          (with-temp-buffer
            (save-excursion (insert-file-contents smart-scratch-file))
            (read (current-buffer)))
        (erase-buffer)
        (funcall mode)
        (insert content)
        (goto-char point)
        t))))

(defun anak/persist-scratch-buffers-h ()
  "Save all scratch buffers to `doom-scratch-dir'."
  (setq doom-scratch-buffers
        (cl-delete-if-not #'buffer-live-p doom-scratch-buffers))
  (dolist (buffer doom-scratch-buffers)
    (with-current-buffer buffer
      (anak/persist-scratch-buffer-h))))
```

The code wasn't totally correct. When I opened my scratch buffer (`*anak:now-n-next*`), the buffer replaced the current buffer (where my cursor is in). I found that `pop-to-buffer` caused this behavior, shown below.

```emacs-lisp
...
(funcall
     #'pop-to-buffer
     ;; #'switch-to-buffer
     (anak/scratch-buffer
      arg
      'org-mode
      default-directory
      nil))
...
```

I dig into it further by carefully inspect `*Messages*` output using edebug. I found that `display-buffer` applies functions based on file's name. That's it. I changed `(buffer-name "*anak:now-n-next*")` to `(buffer-name "*doom:now-n-next*")`. Now, `*doom:now-n-next*` and `*doom:scratch*` opens buffer the same way.

A Note on `display-buffer`, `display-buffer` collects list of functions to be applied based on class of `display-buffer-*-action` and `*-action` where `(cdr functions)` is buffer name.

```emacs-lisp
...
(while (and functions (not window))
	  (setq window (funcall (car functions) buffer alist)
	  	functions (cdr functions)))
...
```

Below is a message output by `display-buffer`'s code section, shown below.

messages are, in order,

1.  function name to be applied
2.  buffer name
3.  list of actions to apply based.

Below is output when `doom/open-scratch-buffer` is evalulated.

```nil
Result: +popup-buffer

Result: #<buffer *doom:scratch*>

Result: ((actions) (side . bottom) (size . 0.35) (window-width . 40) (window-height . 0.35) (slot) (vslot . -4) (window-parameters (ttl . t) (quit) (select . t) (modeline . t) (autosave . t) (transient . t) (no-other-window . t)))

Result: #<window 115 on *doom:scratch*>
```

Below is output when `anak/open-scratch-buffer` is evalulated.

```nil
Result: display-buffer-use-some-window

Result: #<buffer *anak:now-n-next*>

Result: nil

Result: #<window 67 on *anak:now-n-next*>
```

That's it.

Peace.

~milfex-lostex
