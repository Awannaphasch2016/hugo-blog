+++
title = "Comprehensive review of snippets management tools in emacs. The best way to manage code snippets in emacs."
author = ["Anak Wannaphaschaiyong"]
tags = ["snippet", "blog"]
draft = false
+++

Personally, I think snippets is under untilize. Same as notes. The fact is people just don't do neither snippets or notes.

I defined code snippet as followed

> A collection of either small/large code which may store in single/multiple files that you will revisit against in the future.

Focusing on manging code snippets in emacs, few packages come to mind including: [yassnipet](https://github.com/joaotavora/yasnippet), [auto-yasnippet](https://github.com/abo-abo/auto-yasnippet/blob/master/auto-yasnippet.el), [yankpad](https://github.com/Kungsgeten/yankpad), and [code library](https://github.com/lujun9972/code-library).

In my workflow, to share code snippet with others, gists is needed.

What are list gists packages in emacs? I found [gist.el](https://github.com/defunkt/gist.el), [jist.el](https://github.com/defunkt/gist.el), and [yagist.el](https://github.com/mhayashi1120/yagist.el).

Comparing `gist.el` and `yagist.el`, both are pretty much the same in all aspects including list all gists, create new gists, etc. One major different is that `gist.el` open content of snippet in a new buffer when one pree enter in `*Github gists*` buffer, containing list of all code in your gists.

I just didn't bother with `jist.el`. I skipped it.

lets come back to code snippets. Out of all candidates `yassnipet`, `auto-yassnipet`, `yankpad`, and `code library`, `code library` allow automatic sync to gists when new snippet is added. That's a win for `code-library`.

I also want to point out that `yassnipet` doesn't really follow by definition of code snippets, instead, `yassnipet` provide template for code to be reuse. So, I need to remove `yasnnipet` and `auto-yasnippet` from the equation of "code snippet managements." Just to be clear, `yassnipet` is amazing. I use it. Everyone uses it. If they don't, I will recommend them to use it. Again, it provide code templates.

Now, we left with `yankpad` and `code library`.

On a side note, `yankpad` also support `yasnippet` template and work semalessly with `auto-yasnippet`.

The main selling point of `yankpad` is to manage code snippets within one org file. This allows one to utilize search/filtering capability provided by org mode. With `yankpad`, one can insert, create, and search code snippets. What about `code library`? it only allow you to store it to seapate file with the following `(mode . file-name)` mapping, but, as mentioned above, automatically sync to gist is an amazing feature it provides.

Now you may ask. "Do I even need `code library`? Sure, it save snippet locally but `gist.el` (the winner of gists mangement category.) can create and sync newly added snippet?" The answer is no.

Here is the best workflow I follow.

-   use `yasnippet` for code template, of course.
-   use `yankpad` to store code snippet locally.
-   use `gist.el` to manage code snippet between local and remote. Mostly, for sharing code.

Ultimately, `yankpad` can simply include gists automatically sync feature to make saving code snippet workflow to be seamless, but that doesn't bother me. This is as good as its gonna get if you ask me.

That's it.

Peace.
