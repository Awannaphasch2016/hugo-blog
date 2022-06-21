+++
title = "Most Efficient Workflow To \"Lookup\" Documentations On Programming Language."
author = ["Anak Wannaphaschaiyong"]
tags = ["documentation", "blog", "doom-emacs", "emacs"]
draft = false
+++

The normal workflow of lookup documentation would be to search google, stack-overflow, etc. Alternatively, if you are using IDE, IDE will lookup documentation for you, for example `goto-definition` etc. Very  convenience. What else do you need?

Although, searching online directly is not the best approach, it is everyone last line of defense. On the other hands, IDE is as good as it gets. However, the problem with IDE is that it is context specific. Each IDE is created for one or few language. The advantage of this is workflow can be implemented specially for a language, so theoretically, nothing should be able to beat it.

So, to be fair, the title claim of "most efficient workflow" apply mainly to text editor. Still, I use the word "theoretically" because, in practice, "lookup" documentation for any language is more or less the same.

Lets get into the meat of the blog.

Using Doom Emacs, looking up documentation can be online or offline. For online documentation, I use `devdocs.io`. For offline documentation, I use `docset` from Dash.app. Both contains lots of languages. I can't tell which has more. (You can check by yourself.)

To look up online, I use command `+lookup/documentation`.
To look up offline, I use `+lookup/in-all-docsets`.
To look up vocabulary definition (dictionary must be downloaded locally), I use `+lookup/dictionary-definition`.
To make a correct to misspelling word, I use `flyspell-correct-wrapper`.
To lookup reference. I use `+lookup/references`. What is reference? you asked. Whatever you implemented to be a reference. For example, in org file, reference is implemented as synonym. Sky is the limit.

Not to mention that these features are provided on top of the doom completion module which provide list of string completion based on what I type.

A side note on Doom Emacs. Doom's convention is to add prefix `+` to commands and functions that are implemented by Doom. Doom provides `module` which combine many underlying emacs packages that do the same things to take advantages of good features and eliminate bad features. This `+` is a convention used in Doom module.
