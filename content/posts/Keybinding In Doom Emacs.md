+++
title = "Keybinding In Doom Emacs"
author = ["Anak Wannaphaschaiyong"]
tags = ["blog", "doom", "keybinding"]
draft = false
+++

Doom Emacs has its own keybinding system. A more accurate access would be Doom Emacs keybinding system is a wrapper over evil mode such that it is smoothly compatible with Emacs.

If you use Evil mode without Emacs configuration framework such as Spacemacs or Doom Emacs, it is frustrating to  know if your keybinding is setup properly and will always work as expected at any circumstances. The usually point of failure is when your keybinding is overwritten by other packages. Most of the time, creators of those packages don't use evil-mode, so their implementation don't respect evil-mode, rightfully so.

This is annoying because there is no peace of mind. You can't assume that it will always works in all cases. It always a process of "lets try it here, there, what about that, ...". Because of this, sometimes if I don't need the binding that BADLY, I don't even try it.

Another annoying point is it is one of those problem that you think it should be fixed long along. Also, its one of those that is not that hard to try to solve, but it isn't that interesting enough. You also have to expect iterative process of re-implementing things whenever edge cases came up. tedious process of boringness. And because it is solvable, you can't even blame others, but yourself to not solve it.

Thanks God.

Dooms Emacs solves this problem for us. I am not sure how much Doom Emacs fixed this problem. To my knowledge, I have no problem YET using Doom Emacs keybinding configuration system.

About how to use it. I think its pretty obvious from provided examples in documentation.
I will just explains how to think about it before setup your own key.

Assuming that you use evil-mode,

1.  which map you will to use the key? (`:map`)
2.  which "evil state" or "emacs state" you expect to use the key?
3.  is there any condition you want to be true to enable the key? (:when)
4.  Do you use any prefix? if yes, is it `:leader`, `:localleader`, or `:prefix` (your customize prefix).

That's it really.

That's it.
Peace.
