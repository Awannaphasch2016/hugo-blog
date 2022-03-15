+++
title = "Emacs Package Explained: How to customize key binding in evil modes?"
author = ["Anak Wannaphaschaiyong"]
tags = ["evilmode", "blog"]
draft = false
+++

This is my summary of a more thoroughly explained evil guide, see [here](https://github.com/noctuid/evil-guide#why-dont-keys-defined-with-evil-define-key-work-immediately).


## Keymap Precendence in vanilla emacs {#keymap-precendence-in-vanilla-emacs}

-   `overriding-terminal-local-map` for terminal-specific key bind
-   `overriding-local-map`
-   `keymap char property at point` keymaps for the current character. Yasnippet keymaps are in this category.
-   `emulation-mode-map-alists`. Apparently, its more multi-mode keymap management. I am not sure what this means, but if i have to guess it is used in modes that have its known key precedence or other complexity that its key binding system brings. Evil mode keymap falls into this category.
-   `minor-mode-overriding-map-alise`
-   `minor-mode-map-alist`
-   `keymap text property at point`
-   `current-local-map`
-   `current-global-map`


## Keymap Precendence in `evil mode` {#keymap-precendence-in-evil-mode}

Emacs will look up keymaps in order of top to bottom:

-   `evil-make-intercept-map`
-   `evil-local-set-key`
-   `evil-define-minor-mode-key`
-   `evil-define-key` (auxiliary keymaps)
-   `evil-make-overriding-map`
-   `evil-global-set-map`


## Evil keymaps states {#evil-keymaps-states}

-   `evil-insert-state-map`
-   `evil-emacs-state-map`
-   `evil-normal-state-map`
-   `evil-visual-state-map`
-   `evil-motion-state-map`
-   `evil-operator-state-map`
-   `evil-outer-text-objects-map`
-   `evil-inner-text-objects-map`
-   `evil-replace-state-map`

Note: there is a non-intuitive behavior of evil motion state which I don't quit understand yet. see [here](https://github.com/noctuid/evil-guide#global-keybindings-and-evil-states).


## Defining evil keymaps {#defining-evil-keymaps}

one can define evil keymaps with evil function or native emacs function.

In all of the cases, one needs to provide `key`, `command`, `evil state`, and `keymap`.

```emacs-lisp
(define-key 'evil-normal-state-map (kbd "a") 'bar) ;; i am not sure why scope of evil keymap  doesn't need to be provided like 'evil-global-set-map' etc.
(evil-define-key 'normal 'global "a" 'bar)
(evil-global-set-key 'normal "a" 'bar)
```

To define lead key, `make-sparse-keymap` can be used as followed.

```emacs-lisp
(defvar my-leader-map (make-sparse-keymap)
  "keymap for leader key")

;; binding "," to the keymap
(define-key evil-normal-state-map "," my-leader-map)

;; binding ",b"
(define-key my-leader-map "b" 'list-buffers)

;; change the "leader" key to space
(define-key evil-normal-state-map (kbd "-") my-leader-map)
```


## Why doesn't evil mode work properly? {#why-doesn-t-evil-mode-work-properly}

To be clear, there is no magic underneath. If evil keymaps is in the correct state within correct keymaps precedence, every should work according to keymap search rules.

Recall that evil keymaps are in `emulation-mode-map-alists`, hence, it is possible that other keymaps within the same mode-map can over right it. For example, company mode may override evil mode.


## Switching Between Evil and Emacs {#switching-between-evil-and-emacs}

Note that, here, we don't want to override keybinding. We want to switch between evil and emacs state.

there are the following ways to do this.

-   use `evil-set-initial-state`. Set the initial state when a mode is activated.
-   use `evil-make-override-map` or `evil-make-intercept-map`. Reorder key precedence.
-   use `evil-execute-in-emacs-state`. temporary change to emacs state.
-   use `evil-disable-insert-state-bindings`. If this is non-nil, default Emacs bindings are by and large accessible in insert state.

You can also make sure that a keymap is always less than evil keymap using `evil-make-overiding-map` and `evil-make-intercept-map`.

Furthermore, once a key is defined with `evil-intercept-maps`, it cannot be override. Example of this is `edebug-mode-map`. To modifier key in intercept-map, you must undefined it. It can be done as followed

```emacs-lisp
(define-key keymap [intercept-state] nil)
```

On a side note, if you define keybinding with `setq`, it will have no effect if you define keymap after evil is loaded, so you have to make sure that evil is loaded after as followed.

```emacs-lisp
(setq evil-overriding-maps nil
      evil-intercept-maps nil)
;; ...
(require 'evil)
```

You can always prevent evil keymaps from ever being overwritten after evil is loaded. You can use `(advice-add 'evil-make-overriding-map :override #'ignore)` which can be removed with `(advice-remove 'evil-make-overriding-map #'ignore)`.
