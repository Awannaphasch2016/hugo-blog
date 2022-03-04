+++
title = "How to solve hanging tramps?"
author = ["Anak Wannaphaschaiyong"]
tags = ["tramp", "emacs", "garun"]
draft = false
+++

Note that information I describe here can be found at FAQ page of TRAMP user manual, see [here](https://www.gnu.org/software/emacs/manual/html_node/tramp/Frequently-Asked-Questions.html).

From an hour of digging, I discovered that tramp is really specific in term of how it read terminal prompt (aka PS1 environment variable.). It also limited in types of terminal, specified by TERM environment variables. TERM must match tramp terminal default setting (`tramp-terminal-type`).

I am using zsh shell in my remote compute. (I learn now that being minimalist and stick with bash may have more advantage than I would happily admit few weeks back.)

In my case, I need to set `TERM=dumb` and set `PS1='$ '`.

After assigning new value to environment variables and restart emacs, Tramp no longer hangs.

This fix my problem. If this doesn't fix your problem. please read TRAMP user manual on Tramp hangs section. There are few more things that I haven't get to tried.

and.. just like that I completed my first technical blog writing.
