+++
title = """
  A Note on X where X = "LSP + flycheck + lsp-pyright"
  """
author = ["Anak Wannaphaschaiyong"]
tags = ["lsp", "blog", "pyright", "flycheck", "note"]
draft = false
+++

History of edit

-   Last edit is <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-11-28 Mon&gt;</span></span>.

There are 3 components to pay attention to including: `conda.el`, `lsp-pyright`, and `flycheck`.

First, `conda.el` allows user to activate conda env from within Emacs.
Users can check `conda.el` by checking `conda-env-home-directory`, `conda-env-current-name`, and `conda-env-current-path`.

Second, LSP is language server a general concept outside of Emacs and python. LSP may have type checking as its feature. `lsp-pyright` is python language server (called "pyright"). It is implemented in Elisp. It is lsp that have type checking feature.

Third, `Flycheck` is an emacs package whose goal is to perform on-the-fly syntax checking. The package is meant to be used for multiple languages.

Given what we know above, the main task for configuration is to

1.  have lsp-pyright to correctly set conda env path to lsp-pyright
    set `lsp-pyright-python-executable-cmd` to `python3` (note that env of python3 is determined by `conda-env-current-path`)
2.  have flycheck use lsp-pyright as lsp for python.

That's it.

Peace.

~milfex-lostex
