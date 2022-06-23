+++
title = "A Note On Straight.el's Transaction"
author = ["Anak Wannaphaschaiyong"]
tags = ["straight", "package-manager", "blog"]
draft = false
+++

This article is based on [staright.el README](https://github.com/radian-software/straight.el#comparison-to-el-get) which at the moment doesn't have written document on how transaction works. So This is a work in progress until I either read `straight.el` codebase or summarize its documentation.

Conceptually, `stright.el` clones Git repo and them symlinking files into Emacs's load path. A packages in `straight.el` is defined as `recipe` as a files which was symlinked together. I have an article on recipe.

`straight.el` runs `straight-use-package` during the Emacs initialization to check for package to be updated.
Now, straight has information of what package to be downloaded. user can choose to install whatever packages after Emacs has been launched.

`straight.el` introduce `transaction` concept which provide a way to keep track of things that happens when an operation is executed.

Packages in your emacs configuration (`config.el`?) are passed to `straight-use-package` to be managed. This process is done during loading of your init-file (`init.el`).

Note that there are two ways to load package into `straight.el`. First, `straight.el` is passed packages upon the loading `init.el`. The second way is when one want to try a package, so one decided to manually evaluate `straight-use-package` after emacs has been launched.

How can `straight.el` distinguish between the two?

`straight.el` determines whether packages is part of your `init.el` by reload `init.el`. This implies that `straight.el` should know when the file is evaluated. As of <span class="timestamp-wrapper"><span class="timestamp">[2022-06-22 Wed]</span></span>, I think knowing when file is done evaluated is important because the following: imagine a scenario where package is loaded while init.el is evaluated, one can't tell the name of packages that has been loaded after emacs initialized. One can take the approach of `package.el` by storing mutable state outside of `config.el` inside `jk:package.el` (which is loaded as part of emacs initialization), however, the main selling point of `straight.el` is be passed packages directly to `staright-use-package` while init.el is loaded.

`straight.el` has `transaction system` which can determine when init-file is finished loading by using `post-command-hook` which only execute code after `interactive operation` has finished. More abstractly, `straight.el` introduces transaction concept to keep track of an operation as a unit where, in this case, an `operation` is defined as `evaluating a file`.

`staright.el` will determine which and how to packages whenever `straight-use-package` is invoked. This is because internal state of `straight.el` is managed by `straight-use-package` and internal state can always be change when `staright-use-package` is invoked.
