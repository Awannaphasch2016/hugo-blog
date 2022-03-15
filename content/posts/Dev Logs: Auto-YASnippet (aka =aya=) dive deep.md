+++
title = "Dev Logs: Auto-YASnippet (aka aya) dive deep."
author = ["Anak Wannaphaschaiyong"]
tags = ["aya", "blog", "devlogs"]
draft = false
+++

Dev logs is new blog series which dive deep into implementation level. The goal is to understand how things works. I figure this should be an interesting series because I always wanted to know how these program works underneath. Instead of explaining the whole code base, I will only focus on the "magical" part that sparked my interest the most.

Todays I present to you `aya`.

I started of the series with `aya` because, I think, it is a small package with the right portion of magic.

The branch I am working with is `ab930dd` commit from [abo-abo repo](https://github.com/abo-abo/auto-yasnippet).

Question I had about `aya` is the following:

1.  How does it know where to replace content?
2.  How is yassnippet template stored during the `aya-create`?

For those whose doesn't want to bother downloading the code. Here is the code I am dealing with.

```emacs-lisp
(defun aya-create (&optional beg end)
  "Create a snippet from the text between BEG and END.
When the bounds are not given, use either the current region or line.

Remove `aya-marker' prefixes, write the corresponding snippet to
`aya-current', with words prefixed by `aya-marker' as fields, and
mirrors properly set up."
  (interactive)
  (unless (aya-create-one-line)
    (let* ((beg (cond (beg)
                      ((region-active-p)
                       (region-beginning))
                      (t
                       (aya--beginning-of-line))))
           (end (cond (end)
                      ((region-active-p)
                       (region-end))
                      (t
                       (line-end-position))))
           (str (buffer-substring-no-properties beg end))
           (case-fold-search nil)
           (res (aya--parse str)))
      (when (cl-some #'listp res)
        (delete-region beg end)
        (insert (mapconcat
                 (lambda (x) (if (listp x) (aya--alist-get-proper-case-value x) x))
                 res ""))
        (setq aya-current
              (aya--maybe-append-newline
               (mapconcat
                (lambda (x) (if (listp x) (aya--alist-create-value-specifier x res) x))
                res "")))
        ;; try some other useful action if it's defined for current buffer
        (and (functionp aya-default-function)
             (funcall aya-default-function))))))
```

Function I am interested in is `aya-create`.
`aya-create` contains 3 interested functions: `aya--parse`, `aya--alist-get-proper-case-value`, and `aya--alist-create-value-specifier`

"--" in the function names is a convention of elisp which indicates that it is a private function.

from `(cl-some #'listp res)` expression, the condition is non-nil if res is a list.
Now, I know that `aya--parse` must return some kind of list.

Given the selected region, `aya--parse` match the following regex.

```emacs-lisp
(format
    "\\(?:`\\(?1:[^']+\\)'\\|%s\\(?1:\\(?:%s\\)+\\)\\)"
    aya-marker ;; value is ~
    aya-field-regex)
```

Then, `aya--parse` return the following format which contains tuples of string properties.

```emacs-lisp
(list (cons 'idx idx)
                    (cons 'value cased-mirror)
                    (cons 'ucase ucase))
```

If `aya--parse` return appropriate format, selected aread will be delete with `(delete-region beg end)` and

Content of a target region is recreated with

```emacs-lisp
(insert (mapconcat
            (lambda (x) (if (listp x) (aya--alist-get-proper-case-value x) x))
            res ""))
```

where `aya--alist-get-proper-case-value` uses list of tuple properties to recreate orignal string.

aya template is saved to `aya-current` whose templatpe is created with `aya--alist-create-value-specifier` as followed

```emacs-lisp
(setq aya-current
        (aya--maybe-append-newline
        (mapconcat
        (lambda (x) (if (listp x) (aya--alist-create-value-specifier x res) x))
        res "")))
```

I think I have learn more than enough to answer my question, so I am going to stop here.

Lets recap.

Diving into few functions, I am able to answer our questions

1.  "How does `aya` know where to replace content?"
2.  "How is yassnippet template stored during the `aya-create`?"

`aya` uses regex to capture string of interest within a region then it create property list of captured string (mainly, be aware of string capitalization.). Template of the captured string is created accordingly and ready to be reused in the future.

Personally, I have learned a few things.

1.  I have learned how regex is used in emacs style. Other than annoying string escape, I have learned `(?num:)` where num is a explicit numbered group. See [here](https://www.gnu.org/software/emacs/manual/html_node/elisp/Regexp-Backslash.html) for more in formation.
2.  I have learned the basic of matching, see [34.6 The Match Data](https://www.gnu.org/software/emacs/manual/html_node/elisp/Match-Data.html) from emacs manual.
3.  I have learn abo-abo style of coding, especially, how he stored property of matched region property as a list of tuples after processed target string.

That's it.

Peace.
