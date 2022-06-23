+++
title = "A Note On Straight's Recipe."
author = ["Anak Wannaphaschaiyong"]
tags = ["package-manager", "blog", "recipe", "straight", "package-manager"]
draft = false
+++

Straight's recipe is similar but not identify to one used by MELPA.&nbsp;[^fn:1]

A `recipe` describes which local repository to link the files from and how to clone that repository, if repo is not found locally. With this definition of recipe, one can think of recipe as a build step (`recipe`) of a package.

Ultimately, a package is defined is a collection of files required for package's build. `striaght.el` views a package in this manner. As a result, `straight.el` tries to get away from definition package as a folder (e.g. Git repo or an entry in MELPA). Note that folder itself is also defined as a collection of file that share same root directory. Some would argue that folder can be composed of symlink. Allowing symlink, folder is a subset of a package because all files in folder may not required for package's build. That's it `straight.el` use symlink internally.

There are 2 types of recipe: fetch recipe and build recipe.

As the name suggested, `build recipe` is `recipe` for build. Using definition of `recipe`, `build recipe` is a recipe that describe local source and local destination of symlink relevant to succesfully build a package. It is composed of 3 properties: `:files`, `:local-repo`, and `:build`. symlink is created from `:files` to point to `:local-repo`. After symlinks are created, the target files are byte-compile and store in `:local-repo`. When local files are missing, `fetch recipe` will be used to fetch files from git repo, hosted online ,such as Github. It is composed of 5 properties: `:repo`, `:host`, `:branch`, `:nonrecursive`, `:fork`, `:protocol`.

See <straight_dir> for visualization straight directory. Note that only `.el` files are symlinked, since only they are relevant to Emacs to build.

<a id="code-snippet--straight-dir"></a>
```md
straight
├── build
│   ├── el-patch
│   │   ├── el-patch-autoloads.el
│   │   ├── el-patch.el -> ~/.emacs.d/straight/repos/el-patch/el-patch.el
│   │   └── el-patch.elc
│   └── straight
│       ├── straight-autoloads.el
│       ├── straight.el -> ~/.emacs.d/straight/repos/straight.el/straight.el
│       └── straight.elc
└── repos
    ├── el-patch
    │   ├── CHANGELOG.md
    │   ├── LICENSE.md
    │   ├── README.md
    │   └── el-patch.el
    └── straight.el
        ├── LICENSE.md
        ├── Makefile
        ├── README.md
        ├── bootstrap.el
        ├── install.el
        └── straight.el
```

Note that collection of recipes are contained in recipe repositories which is implemented as a regular package (collection of dependent files). The recipe repository backends abstract over the formatting differences in different recipe sources to translate recipes into the uniform format used by straight.el. When you run M-x straight-get-recipe, the translated recipe is what is returned.&nbsp;[^fn:1]


## What recipe doesn't get right. {#what-recipe-doesn-t-get-right-dot}

As far as I am concerned, `straight.el` follows informal guideline by package manager developer (<a href="#citeproc_bib_item_1">Boyer 2016</a>) which requires that a package manage dependencies based on information from 4 states including project code, manifest file, lock file, and dependencies. `straight.el` `recipe` is an implementation of manifest like functionality. One thing that `straight.el` doesn't follow is that `lockfile` is written by human to overwrite `fetch recipe`. One downfalls of this is there is no way to confirm that the package manager use dependencies you are intended. Boyer (<a href="#citeproc_bib_item_1">Boyer 2016</a>) states that lockfile should generate by machine as a confirmation of what dependencies it uses. As of <span class="timestamp-wrapper"><span class="timestamp">[2022-06-22 Wed]</span></span>, I can't think of a scenario that require one to edit lockfile to overwrite `recipe`. I need to use it more to have creditable opinion to critique further.

Lastly, `straight.el` should allow for "local recipe" which can be loaded to overwrite "original recipe." Not sure how useful will this be, but it seems to be quit useful for testing different version of packages while using Emacs.


## Conclusion {#conclusion}

Last few word from me before signing off. After reading through, I get this feeling that `straight.el` obviously does what "package manager" should do in general. Whenever I have a feeling of "obviously x", there is an "internal signal" in me that says "its obvious because you don't know what have been done." I will leave this question to be explored in the future. For now, best I can do is to be curious on whether "internal signal" is any good.

That's it.
Peace.

<style>.csl-entry{text-indent: -1.5em; margin-left: 1.5em;}</style><div class="csl-bib-body">
  <div class="csl-entry"><a id="citeproc_bib_item_1"></a>Boyer, Sam. 2016. “So You Want to Write a Package Manager.” <a href="https://medium.com/@sdboyer/so-you-want-to-write-a-package-manager-4ae9c17d9527urldate2022-06-22">https://medium.com/@sdboyer/so-you-want-to-write-a-package-manager-4ae9c17d9527urldate2022-06-22</a>.</div>
</div>

[^fn:1]: [The staright's recipe format](https://github.com/radian-software/straight.el#the-recipe-format)
