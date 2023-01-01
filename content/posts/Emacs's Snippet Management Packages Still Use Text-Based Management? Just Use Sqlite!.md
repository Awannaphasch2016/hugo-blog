+++
title = "Emacs's Snippet Management Packages Still Use Text-Based Management? Just Use Sqlite!"
author = ["Anak Wannaphaschaiyong"]
tags = ["snippet", "pkm", "blog", "sqlite", "emacs"]
draft = false
+++

By now, in <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-12-08 Thu&gt;</span></span>, it should be conclusive that any type of contents are best organized/managed using database. Responsibilities of database includes retrieve/store data. That's it.

However, emacs manages data as text. Advantages of this is simplicity, but, this argument doesn't even work anymore. why? Emacs supports SQLite as built-in!

I like Emacs because of level of compatibility that it provides, but it frustrates me to realized that open source community is not as collaborative, as a result, Emacs slow to adopts.

Yassnippet, CodeLibrary, and Yankpad are all snippet managements packages. All of them use text to manage snippets. Yassnipeet and Codelibrary manage snippet using directory and filename. Directory where snippets are stored. Yassnippet detects mode by searching for directory name that match mode name, and each directory contains files containing "snippet template." CodeLibrary is similar to Yassnippet in that it does text searches on mode name, but instead of directory's name, it uses filename.

Yankpad takes slightly different approach. Yankpad only look for file content, specified by `yankpad-file`. Depends on "category", heading hierarchy, heading's tags, and heading's properties, different set of rules will be triggered. These rules include "content of other files to be appended to `yankpad-file`," "which heading to include?" and "what part of heading to include?" Yankpad has these rules which allows yankpad to be organized in a more flexible way. Still, it can be done with SQLite as database. Just use that.

That's it.

Peace.

~milfex-lostex
