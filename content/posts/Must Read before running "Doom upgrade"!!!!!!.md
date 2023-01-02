+++
title = """
  Must Read before running "Doom upgrade"!!!!!!
  """
author = ["Anak Wannaphaschaiyong"]
tags = ["doom", "blog", "upgrade"]
draft = false
+++

Doom discord announces important update and fixes. This is where you should take a look first before attempting to pull remote commits that are ahead of your local commits.

Doom emacs has only 1 branch. It used to have 2 main branch master and develop branch, but Henrik give up on develop branch because, I assume, its too much work to make develop branch stable before merging to master. For this reason, instead of merging develop branch to master branch. all the development is done in master branch. One can find new release by searching for `release(modules)` commit headline in `git log --all`.

More than often apply `git checkout` to new Doom release will result in error and, large about of those time, you can't event launch your Emacs. When you encounter this scenario, use `git bisect` to pin point earliest commit that cost the problem and work your way up from there.
