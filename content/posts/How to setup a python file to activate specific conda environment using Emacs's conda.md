+++
title = "How to setup a python file to activate specific conda environment using Emacs's conda.el?"
author = ["Anak Wannaphaschaiyong"]
tags = ["conda", "emacs"]
draft = false
+++

I found that default setup for `conda.el` to be annoying and not robust. Firstly, setting `(conda-env-autoactivate-mode t)` will output error everytime file. Apparently, from inspecting the code, this is how it is implemented! see below.

```emacs-lisp
(if conda-env-autoactivate-mode ;; already on, now switching off
      (advice-add 'switch-to-buffer :after #'conda--switch-buffer-auto-activate)
    (advice-remove 'switch-to-buffer #'conda--switch-buffer-auto-activate))
```

The error is `(error "No such conda environment: %s" name)` because input argument `name` has nil value when a file that is switched to don't have `environment.yml` setup. What an assumption to make! --- I think the author is being lazy. (which is reasonable given that he doesn't need to share. I still thank him for sharing!)

The default configuration works fine for me, but it gets annoying whenever I run `toggle-debug-on-error`!.

The solution to this annoying problem is for you to use conda like how it is implemented --- not what it says in the Readme.md! (a very common and understandable documentation bug). I purpose my solution below.

First, you must put the following code in config.el

```emacs-lisp
(use-package! conda
  :config (setq-default mode-line-format (cons '(:exec conda-env-current-name) mode-line-format))
  :after python-mode
  :hook (add-hook 'python-mode-hook 'conda-env-activate-for-buffer))
```

Then, you must place `environment.yml` in base directory (or in any level of parent directories of a python file) then put the following code in the yaml file.

```yaml
name: test
```

That's it.

Peace.

milfex-lostex
