+++
title = "how to publish hugo blog with org mode subtree?"
author = ["Anak Wannaphaschaiyong"]
tags = ["hugo"]
draft = false
+++

Prerequisite of this blog assumes that you already setup hugo blog by going through hugo [quick start](https://gohugo.io/getting-started/quick-start/) documentation.

This blog is published via approaches presented in this blog.

Org mode subtree is just one of the bullet point (aka. header) within org mode.
As the title suggested, this article publication workflow allows one to publish subsection of a content within one of org mode header as a full page article. Main advantage of this method is that user doesn't need to move content from the original location. Not even move to a separate file!

There are few moving components you have to configure to have a seamless workflow for

1.  converting org mode to org markdown.
2.  place converted markdown down file to content directory of your hugo site. (e.g. `path-to-hugo-site/hugo/quickstart/content/posts/`)

The goal of these configurations is to let hugo file converter knows base directory of your hugo site directory, and name of the article.

You can set base directory of your hugo site by setting `:hugo_base_dir:` property at the top of your file. It should look like the following, for example,

```org
#+hugo_base_dir: /home/awannaphasch2016/org/projects/sideprojects/website/my-website/hugo/quickstart=
```

Next, you have to set name of your article by setting `:EXPORT_FILE_NAME:` property under header that contain content of your.

Now, you are ready to publish your content. You can publish with `org-export-dispatch` command and select `Export to hugo-compatible markdown` option.

Your article is added to `hugo-repo/content/posts` as a post with .md extension. This is a local update. If you run `hugo server -D` (this runs hugo server locally at `localhost` port `1313`: `localhost:1313`), you can see that new article has been updated.

To update to online (At <span class="timestamp-wrapper"><span class="timestamp">[2022-06-15 Wed]</span></span>, I personally use github free hosting ending in `.github.io`), you have to run `hugo` command at the project root directory. The changes will be generated to `hugo-repo/public/posts`. This directory contains articles that are ready to be hosted online for the world to see.

Note that using hugo with github, online `hugo-repo/public` needs to be manage. Not the whole `hugo-repo`.
It is also important to emphasize that local update can be viewed immediately, however, you must wait for a few mins (&lt; 5 mins) for online update. (like any other content update for online site ever.)

One minor inconvenient I want to point out is using this workflow one cannot identify location of the org file from converted markdown files shown in content directory of your hugo site. Because of the first point, every times you published the same content, new markdown is created. You have to delete the previous one manually.

Slight inconvenient, but miles away from other publication workflow I have tried.

Peace out.
