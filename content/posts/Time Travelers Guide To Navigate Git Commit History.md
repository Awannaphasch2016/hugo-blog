+++
title = "Time Travelers Guide To Navigate Git Commit History."
author = ["Anak Wannaphaschaiyong"]
tags = ["git", "autodidact"]
draft = false
+++

One of principle I follow is

> never rely on others' people goodwill.
> and
> always expect other to be evil when it is possible.

In quote <qoute>, type of `evil` falls into incompetent evil and irresponsible evil. Putting this principle into practice, one must understand structures that govern behavior of people given a particular pursuit of goal.

In this scenario, I refers `structure` as `git log`  and `a particular pursuite of goal` as `learning and understanding a piece of code such as open source code.`

A common practice to understand open source is to "read readme.md", "read documentation", or "look at examples." All of these violate the principle since it expects other to have readme, documentation, and examples or you to look at.

What is the alternative? you asked. One alternative would be to look at git history and go back into git commit history and inspect the bare minimum that make the very thing you want to learn work at all. This approach remove boiler plate of dependencies that make the feature you wanted to learn work with other components (which, often than not, you don't care about it).

Before you commit to learn from a particular piece of code, you have to skim through. Given that you found the code on github, the quickest way is to go to `users/git-repo/commits/branch?before=most-recent-comment+total-number-of-commits`. For example, on <span class="timestamp-wrapper"><span class="timestamp">[2022-06-15 Wed] </span></span> at 6.35 PM GMT-4 `torvalds/linux` repo on github as `1105072` commits  `https://github.com/torvalds/linux/commits/master?before=afe9eb14ea1cbac5d91ca04eb64810d2d9fa22b0+1105072` shows commit page where the most bottom commit is the first commit of Linux ever committed using git version control.

When using `before` argument (alternatively, you can use `after` argument), commit timeline can be visualized as followed.

<a id="code-snippet--git-commit-timeline"></a>
```org
                 [--------github-commit-page-------]
(-inf)-(-2)-(-1)-(target-commit)-(+1)-(+2)-...-(+35)-...-(+inf)
```

where left commit is older and `github commit page` can contain at most 35 commits.
Note: math to show commits on `commit page` may be abit off, but you get the idea.
