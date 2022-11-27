+++
title = "Markdown Note"
author = ["Anak Wannaphaschaiyong"]
tags = ["markdown", "emacs"]
draft = false
+++

## Blog <span class="tag"><span class="blog">blog</span></span> {#blog}


### X implementation where X = "markdown-preview" in Emacs <span class="tag"><span class="implementation">implementation</span></span> {#x-implementation-where-x-markdown-preview-in-emacs}

`markdown-preview` pass HTML file to `browse-url`
`browse-url` has the following algorithm

1.  prepare argument to use with specify url
2.  check for "url handle" (which is prefix to url e.g. `file:`)
3.  expand file name according to "url handle"
4.  find suitable function to browse url
5.  setup environment variable for display e.g. `DISPLAY` and `WAYLAND_DISPLAY`
6.  apply function with argument
