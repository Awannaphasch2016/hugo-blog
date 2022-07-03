+++
title = "Implementation of X where X = Emac's auth-source."
author = ["Anak Wannaphaschaiyong"]
tags = ["auth-source", "blog"]
draft = false
+++

As an example, I will use `api.github.com` as a API endpoint.

If I use `~/.authinfo.gpg` as an auth-sources file. (variable name is `auth-sources`), I need to add the following to the file where I need to sub value into `user-username` and `user-password`.

```org
machine api.github.com login user-name password user-password
```

`auth-source-search` is a function that retrieve password from your specify auth-sources file. You can use it as followed. This will output list of property where `:secret` key has your password as its value.

```emacs-lisp
(apply #'auth-source-search
       (append '(:host "api.github.com" :user "awannaphasch2016^forge") (list :max 1)))
```
