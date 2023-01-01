+++
title = """
  A Note Of X Where X = "Debugging Org's Overwritten Variables"
  """
author = ["Anak Wannaphaschaiyong"]
tags = ["blog", "note", "debug"]
draft = false
+++

To debug org related bug, org-reload reloads all lisp files in `~/.emacs.d/.local/straight/repos/org/`. Reloading `config.el` files should inform you what information has been overwritten. If you use `Doom Emacs` and modify either `package.el` or `init.el`, you must run `doom sync` in your terminal (outside of emacs), then consequently run `doom/reload` inside `Doom Emacs` for modification to correctly take effect.

It is important to note that you should always make sure to set `custom-variables`  --- variables declared by `defcustom` --- using `custom-set-variables`. These values are saved in `custom.el`. If, after applying `org-reload`, configuration still not fully refresh, you need to check `custom.el`. For more information about what information is cached, see `~/.emacs.d/.local/cache`. More information about recorded history is at `~/.emacs.d/.local/cache/savehist`. I don't recall chaining value here help much.
