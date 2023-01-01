+++
title = """
  Note of X where X = "I cannot set custom-variable of org-agenda using either setq or custom-set-variables"
  """
author = ["Anak Wannaphaschaiyong"]
tags = ["org-agenda", "blog", "note", "org-refile", "customization"]
draft = false
+++

I couldn't use `setq` and `custom-set-variables` to have `org-refile` shows list of newly set `org-agenda-files`.

Started to solve, first suspect I found was when I learned about `custom.el` file. Custom variable set by `defcustom` will set custom value in `custom.el`. I reset all `custom.el` to `nil` to make sure that it doesn't set custom variables under weird condition that I am not aware of.

I reloaded Doom Emacs. Changed variables didn't reflect in `helpful-variable`, and `org-agenda-files` was not set to nil --- value shown in `custom.el` --- when I commented out  `(org-agenda-files nil)`. Note that I set `org-agenda-files` to nil using `customize` previous to commenting it out.

I also found that reloaded Doom Emacs seems to load `custom.el` after `init.el`. I tested this hypothesis of this behavior a couple time.

Still, It was too soon to say with confident what side effect of using `setq` in place of `custom-set-variable` is.

Next, I tried changing `setq` to `custom-set-variables`. Then I reloaded. Both `setq` or `custom-set-variables` changed value of `org-agenda-file` in `helpful-variable` accordingly. However, `org-refile` still showed old `org-agenda-file` list.

Next attempt is to look at the code, skimmed through `~/.emacs.d/.local/straight/repos/org/lisp/org-refile.el`, I found that `org-refile-get-targets` retrieve list of files from `org-agenda-files`. This is interesting because value of `org-agenda-files` I saw in `helpful-variables` hold newly changed value --- value that was not reflected in list showed in `org-refile`. Saw this, I immediately think about cached value -- similar situation related to projectile value not updating. Then, I searched for "reload" and "cache" keyword in `helpful-functions` and found `org-reload`. Running `org-reload` solved the problem. Now, org agenda files values reflected the change.

Note I didn't try that hard to find cache file because `org-reload` turned out to solve the problem. I also didn't spend time figure out how refile related cache function works.

That's it.

Peace.

~milfex-lostex
