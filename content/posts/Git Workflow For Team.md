+++
title = "Git Workflow For Team"
author = ["Anak Wannaphaschaiyong"]
tags = ["git", "collaboration"]
draft = false
+++

I intend to make this blog be a work-in-progress where I will keep adding useful git workflow when working with a team.


## Pull Requests {#pull-requests}

To do a pull-requests, you need to do the following

1.  fork original repo.
2.  create new local branch and checkout to the new branch.
3.  commit new changes.
4.  send pull requests from `new local branch` from `forked repo (origin)` to `original repo (upstream)`.

Alternative to the pull-request workflow I mention above, it is possible to do pull-requests by using `git forge`&nbsp;[^fn:1], adding commit to new branch&nbsp;[^fn:2], and then do a pull requests to the target branch in remote. The new branch is automatically created


## Pull new updates from upstream repo {#pull-new-updates-from-upstream-repo}

To get new updates from upstream, you need to do the following

1.  `git fetch upstream`
    check if git fetch correctly by running `git branch -v -a`
2.  git merge `remote/upstream` to local branch.
3.  git push changes to from local branch to `remote/origin`

[^fn:1]: As of <span class="timestamp-wrapper"><span class="timestamp">[2022-07-03 Sun]</span></span>, I still don't know for sure what `git forge` does or what it is
[^fn:2]: As of <span class="timestamp-wrapper"><span class="timestamp">[2022-07-03 Sun]</span></span>, I believe that the new branch is on the orignal repo instead of fork repo. I haven't tried it first hand, I watched this [magit forge video](https://www.youtube.com/watch?v=wgI8r3Nx_BI&ab_channel=MikeZamansky).
