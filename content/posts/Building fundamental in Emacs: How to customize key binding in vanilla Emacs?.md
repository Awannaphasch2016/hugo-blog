+++
title = "Building fundamental in Emacs: How to customize key binding in vanilla Emacs?"
author = ["Anak Wannaphaschaiyong"]
tags = ["emacs", "blog"]
draft = false
+++

When I first get into Emacs, I was a vim user before, so I picked up Doom Emacs without experience with vanilla Emacs. Transition has been smooth so far, but because I never has experience with Vanilla Emacs before when I encounter a bug in Doom Emacs. I always have to first figure out if it is Doom Emacs problem or Emacs problems. Because of this, I put out a new blog series to help me build a stronger foundation of Vanilla Emacs.

I started of the series with a topic that irritate me quite often, key binding.

My goal of this blog is as followed

1.  Understand priority of keymaps
2.  Understand stand enough to distinguish vanilla Emacs problem from Doom problem.

This is a summarize of `Emacs Internal Manual under Emacs topic on chapter 49.3 Key Binding Chapter`.


## Keymaps {#keymaps}

Most modes have their own key binding which can overwrite your custom keybinding. For this reasons Emacs has reserve small number of keys to create a "safe space" for custom or build-in key binding example of these are 'C-c &lt;a char&gt;'', 'F5' - 'F9' keys.

Key sequence and its command function are recorded in Emacs as a data structure called "keymaps".

Keymap's value consist of `sequence of key binding` and `command` where `sequence of key binding` can either be a key or a `chain of keymaps`, more in "Visualize how a chain of keymaps works" section. In the other word, a keymap is a map between presentation of `key sequence` to a command.

Note that since `keymaps` is simply just a data structure. A mode can define its own `keymaps` such as `org-mode-map` etc.

To inspect current keymaps availble in a buffer, you can use `C-h b`.

Keymaps accepts values from variety of keys including '&lt;Home&gt;' and mouse.


## Prefix {#prefix}

Emacs interprets one keymap at a time, however, a "chain" of keymap commands is also accepted. A "chain" of keymap  contains "prefix". "prefix" is a keymap that map to other keymaps.

Some keymap (not all) have symbols representation, for example, symbol of 'C-x' is 'Control-X-prefix'.


## Local Keymaps {#local-keymaps}

local keymaps can have their own prefix key.

It is important to note that global prefix is ALWAYS vulnerable to be overwritten by higher priority keys. Still, there are keys that are reserved for the user. (From what I have read, it is unclear which keys are reserved.)

When local keymap is defined, global keymaps and local keymaps are chain together.
To clarify, given that we have "C-x C-z h", "C-x" is global prefix and "C-z" is local prefix. instead of one "C-x C-z" prefix.


## Visualize how a chain of keymaps works? {#visualize-how-a-chain-of-keymaps-works}

This is how I think of it visually. It maybe incorrect or imprecise, but, at least, it helps me visualize in my head.

Says, we have a keymap `a,b,...,n` that map to `foo-command`.
Recall that a keymap is a map between presentation of `key sequence` to a command.
When sequence of key is pressed, a chain of keymap will be evaluated as followed.

```nil
(key a, keymap b)-> (key b, keymap c) -> ... -> (key n, foo-commands)
```


## Key precedence (keymap lookup order) {#key-precedence--keymap-lookup-order}

local keymaps can be defined in 3 different places.

1.  Major mode
2.  Minor mode
3.  area of text within a buffer.

To be more precise, in term of commands, key precedence (keymap lookup order) is as followed. Emacs look up keymap from top to bottom of the list.

1.  `overriding-terminal-local-map` for terminal-specific key bind
2.  `overriding-local-map`
3.  `keymap char property at point` keymaps for the current character. Yasnippet keymaps are in this category.
4.  `emulation-mode-map-alists`. Apparently, its more multi-mode keymap management. I am not sure what this means, but if i have to guess it is used in modes that have its known key precedence or other complexity that its key binding system brings. Evil mode keymap falls into this category.
5.  `minor-mode-overriding-map-alise`
6.  `minor-mode-map-alist`
7.  `keymap text property at point`
8.  `current-local-map`
9.  `current-global-map`


## Modifying Keybinding {#modifying-keybinding}

Note that, Emacs always treats ‘C-A’ as ‘C-a’, ‘C-B’ as ‘C-b’, and so forth. This is because, in non-graphical environment,  'A' is the same as 'a.' To let Emacs know about the difference, we can pass in 'C-S-a' where S is &lt;Shift&gt;.

You have to think in the point of view of how computer compile information.

Emacs also accpets uncommon including &lt;Super&gt;, &lt;Hyper&gt;, and &lt;Alt&gt;, these are represented as 's-', 'H-', and 'A-'. Without these keys on the keyboard, you can still activate the key with 'C-x @ s', 'C-x @ h', and 'C-x @ a', respectively.

There are more valid keys. I only provide few examples.

The goal of modifying a keymap is to either modify `sequence of key binding` or `command` of a keymap.


### Changing Keybinding for current Emacs session. {#changing-keybinding-for-current-emacs-session-dot}

One can change keybinding for CURRENT Emacs session with the following options.

```nil
‘M-x global-set-key <RET> KEY CMD <RET>’
     Define KEY globally to run CMD.
‘M-x local-set-key <RET> KEY CMD <RET>’
     Define KEY locally (in the major mode now in effect) to run CMD.
‘M-x global-unset-key <RET> KEY’
     Make KEY undefined in the global map.
‘M-x local-unset-key <RET> KEY’
     Make KEY undefined locally (in the major mode now in effect).
```


### Changing Keybinding permanently. {#changing-keybinding-permanently-dot}

One can change keybinding permanently using the following commands.

```emacs-lisp
(global-set-key (kbd "C-c y") 'clipboard-yank)
(global-set-key (kbd "C-M-q") 'query-replace)
(global-set-key (kbd "<f5>") 'flyspell-mode)
(global-set-key (kbd "C-<f5>") 'display-line-numbers-mode)
(global-set-key (kbd "C-<right>") 'forward-sentence)
(global-set-key (kbd "<mouse-2>") 'mouse-save-then-kill)
```

One can also delay local keymap to be evaluated by using hook as followed.

```emacs-lisp
(add-hook 'texinfo-mode-hook
    (lambda ()
        (define-key texinfo-mode-map "\C-cp"
                    'backward-paragraph)
        (define-key texinfo-mode-map "\C-cn"
                    'forward-paragraph)))
        (define-key texinfo-mode-map "\C-c\C-xx" nil)
```


### Rebinding with Mouse event {#rebinding-with-mouse-event}

valid key includes

```nil
[mouse-N] where 1 is the leftmost mouse button.
[drag-mouse-N]
[down-mouse-N]
[double-mouse-N]
```

keyboard prefix precedes mouse prefix.

Keybinding for clicking on frame has the following format [frame-type mouse-N]
frame-type includes

```nil
‘mode-line’
     The mouse was in the mode line of a window.
‘vertical-line’
     The mouse was in the vertical line separating side-by-side windows.
     (If you use scroll bars, they appear in place of these vertical
     lines.)
‘vertical-scroll-bar’
     The mouse was in a vertical scroll bar.  (This is the only kind of
     scroll bar Emacs currently supports.)
‘menu-bar’
     The mouse was in the menu bar.
‘tab-bar’
     The mouse was in a tab bar.
‘tab-line’
     The mouse was in a tab line.
‘header-line’
     The mouse was in a header line.
```


### Disabling Commands {#disabling-commands}

disable Commands silently

```emacs-lisp
(put 'delete-region 'disabled
    "It's better to use `kill-region' instead.\n")
```

disable commands with message

```emacs-lisp
(put 'delete-region 'disabled
    "It's better to use `kill-region' instead.\n")
```


### When to define a mode? {#when-to-define-a-mode}

You might imagine to simply have one of these modifier keymap function in your init.el and keymaps will be rebind.

Not so fast.

Sometimes, major mode or minor mode may define their keybinding using mode-hook. In this case, keymaps that are defined later can override your init.el configuration. In the cases as this, you have to dig into thier souce code to understand when you want your new keybinding to be evaluated.


## Conclusion {#conclusion}

This blog summarizes `Emacs Internal Manual under Emacs topic on chapter 49.3 Key Binding Chapter`. We have learn that keymap priority based on context from highest to lowest: region in buffer, minor mode, and major mode.

Lastly, I have learned that vanilla Emacs doesn't exc. I can't say what exactly.
