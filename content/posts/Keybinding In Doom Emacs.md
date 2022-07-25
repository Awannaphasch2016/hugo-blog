+++
title = "Keybinding In Doom Emacs"
author = ["Anak Wannaphaschaiyong"]
tags = ["blog", "doom", "keybinding"]
draft = false
+++

Doom Emacs has its own keybinding system. A more accurate explaination is

> Doom Emacs keybinding system is a wrapper over evil mode such that it is smoothly compatible with Emacs.

If you use Evil mode without Emacs configuration framework such as Spacemacs or Doom Emacs, it is frustrating to  know if your keybinding is setup properly and whether it will always work as expected in any circumstances. A common point of failure is when your keybinding is overwritten by some packages. Most of the time, creators of those packages don't use evil-mode, so their implementations don't respect evil-mode, rightfully so.

This is annoying because there is no peace of mind. You can't assume that it will always works in all cases. It always a process of "lets try it here, there, what about that, ...". Because of this, if I don't need the binding that BADLY, I don't even try it.

Another annoying point is it is one of those problem that you think it should be fixed long along. Also, its one of those that is not that hard to try to solve, but it isn't interesting enough. On top of that, you also have to expect iterative process of re-implementing things whenever edge cases came up. tedious process of boringness. And because it is solvable, you can't even blame others, but yourself.

Thanks God. Dooms Emacs solves this problem for us. I am not sure how much Doom Emacs fixed this problem. To my knowledge, I have no problem YET using Doom Emacs keybinding configuration system.

Assuming that you use evil-mode and use `map!` to modify your key&nbsp;[^fn:1], you have to answer the following question.

1.  What is the keymap you will use? (`:map`)
2.  Do you expect to use your keymap in "evil state" or "emacs state"?
3.  Is there any condition you want to be true to enable the key? (`:when`)
4.  Which prefix option do you choose, if any? is it `:leader`, `:localleader`, or `:prefix` (your customize prefix).
5.  What is the mode you want to enable your keymap? (`:after`)

As an example, I have `org-cdlatex-mode` enable when I open org mode file and `` ` `` (uptick key) is map to `cdlatex-math-symbol` command when I am in `evil-insert-state`. I eval the following expression to assign `` ` `` to nil to allow me to type `` ` `` in `evil-insert-state`.

```emacs-lisp
(map! :after org-cdlatex-mode
  (:map org-cdlatex-mode-map
    "`" nil))
```

Without `map!`, you will have to write hook to run after `org-cdlatex-mode` is enable as followed.

<a id="code-snippet--rebind-uptick-in-org-cdlatex-mode-map"></a>
```emacs-lisp
(defun org-cdlatex-mode-map-hook ()
  (define-key org-cdlatex-mode-map (kbd "`") nil))
(eval-after-load 'org-cdltex-mode
  (add-hook ''org-cdllatex-mode-hook 'org-cdlatex-mode-map-hook))
```

As of <span class="timestamp-wrapper"><span class="timestamp">[2022-07-11 Mon]</span></span>, I am not sure what is the difference usage between `with-eval-after-load` vs `eval-after-load`.

That's it.
Peace.

[^fn:1]: `!` suffix indicate Doom Emacs implementation.
