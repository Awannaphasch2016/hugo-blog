+++
title = "X implementation where X = executing org babel block in Doom Emacs."
author = ["Anak Wannaphaschaiyong"]
tags = ["org-babel", "notes", "blog", "implementation", "doom", "org-babel"]
draft = false
+++

-   Editing History
    -   <span class="timestamp-wrapper"><span class="timestamp">[2022-07-06 Wed]</span></span>
    -   Last edit is on <span class="timestamp-wrapper"><span class="timestamp">[2022-07-07 Thu]</span></span>

This article investigates what is executed when one presses `enter` to execute org babel source block in Doom Emacs.

Pressing `enter` in org-babel block will execute `+org/dwim-at-point`, see code below for reference.
First, it checks if `point` is on a button. Then, it proceeds to assign evaluated output of `org-element-context` and `org-element-type`.

```emacs-lisp
(+org/dwim-at-point *optional ARG)
  ...
  (if (button-at (point))
      (call-interactively #'push-button)
    (let* ((context (org-element-context))
           (type (org-element-type context)))
      ;; skip over unimportant contexts
      (while (and context (memq type '(verbatim code bold italic underline strike-through subscript superscript)))
        (setq context (org-element-property :parent context)
              type (org-element-type context)))
      (pcase type
        ...
        ((or `src-block `inline-src-block)
         (org-babel-execute-src-block arg))
```

`org-element-context` returns smallest element or object around point as `(TYPE PROPS)`. Possible types are defined in `org-element-all-elements` and `org-element-all-objects`.

PROPS, short for properties, depends on element or object type, but always have information about surrounded context and location of the element including `:begin`, `:end`, `:parent` and `:post-blank`. It is important to note here that Emacs is designed to assign set of properties to every characters in a buffer. `org-element-context` makes use of this concept. Information of `org-element-all-objects` and `org-element-all-elements` are provided below.

```emacs-lisp
(print org-element-all-objects)
```

|      |          |                    |      |        |                |                    |                   |                  |        |            |                |      |       |              |                   |                |           |             |            |        |           |           |          |
|------|----------|--------------------|------|--------|----------------|--------------------|-------------------|------------------|--------|------------|----------------|------|-------|--------------|-------------------|----------------|-----------|-------------|------------|--------|-----------|-----------|----------|
| bold | citation | citation-reference | code | entity | export-snippet | footnote-reference | inline-babel-call | inline-src-block | italic | line-break | latex-fragment | link | macro | radio-target | statistics-cookie | strike-through | subscript | superscript | table-cell | target | timestamp | underline | verbatim |

```emacs-lisp
(print org-element-all-elements)
```

|            |              |       |         |               |            |        |               |               |              |             |                     |          |                 |            |      |         |                   |               |           |            |          |                 |             |         |               |           |       |           |             |
|------------|--------------|-------|---------|---------------|------------|--------|---------------|---------------|--------------|-------------|---------------------|----------|-----------------|------------|------|---------|-------------------|---------------|-----------|------------|----------|-----------------|-------------|---------|---------------|-----------|-------|-----------|-------------|
| babel-call | center-block | clock | comment | comment-block | diary-sexp | drawer | dynamic-block | example-block | export-block | fixed-width | footnote-definition | headline | horizontal-rule | inlinetask | item | keyword | latex-environment | node-property | paragraph | plain-list | planning | property-drawer | quote-block | section | special-block | src-block | table | table-row | verse-block |

`org-element-context` simply tries to get `element`, its type, and its position, then process elements based on its type and position and output `(TYPE PROPS)`. One can think of `org-element-context` as a function that "repackage" information of org-element into certain format.

```emacs-lisp
...
     (let* ((pos (point))
	    (element (or element (org-element-at-point)))
	    (type (org-element-type element))
	    (post (org-element-property :post-affiliated element)))
      (cond
       ;; posscess element based on its type and position.
       ... ))
..
```

Running `org-element-context` inside org-babel block, I get the following.

```emacs-lisp
(src-block
 (:language "python" :switches nil :parameters nil :begin 171 :end 213 :number-lines nil :preserve-indent nil :retain-labels t :use-labels t :label-fmt nil :value "print('hi')
" :post-blank 1 :post-affiliated 171 :mode nil :granularity element :org-element--cache-sync-key
(863 . 171)
:cached t :parent
(section
 (:begin 1 :end 232 :contents-begin 1 :contents-end 231 :robust-begin 1 :robust-end 229 :post-blank 1 :post-affiliated 1 :mode first-section :granularity element :org-element--cache-sync-key
  (863 . 0)
  :cached t :parent
  (org-data
   (:begin 1 :contents-begin 1 :contents-end 2408 :end 2408 :robust-begin 3 :robust-end 2406 :post-blank 0 :post-affiliated 1 :path "/home/awannaphasch2016/Scratches/tmp1.org" :mode org-data :CATEGORY "tmp1" :parent nil :cached t :org-element--cache-sync-key
    (803 . -1152921504606846885)))))))
```

Next, if an element's type is either `src-block` or `inline-src-block`, `org-babel-execute-src-block` is executed.

```emacs-lisp
...
        ((or `src-block `inline-src-block)
         (org-babel-execute-src-block arg))
..
```

Similar to `org-element-context`, `org-babel-execute-src-block` gathers information specific to `org-babel` (e.g `org-babel-get-src-block-info`). More specifically, org-babel related information is source block's location, header, and language. Once information is assigned to variables, the function just compute based on provided information.

<a id="code-snippet--org-babel-execute-src-block-src"></a>
```emacs-lisp
(defun org-babel-execute-src-block (&optional arg info params)
  ...
  (interactive)
  (let* ((org-babel-current-src-block-location
	  (or org-babel-current-src-block-location
	      (nth 5 info)
	      (org-babel-where-is-src-block-head)))
	 (info (if info (copy-tree info) (org-babel-get-src-block-info))))

    (cl-callf org-babel-merge-params (nth 2 info) params)
    (when (org-babel-check-evaluate info)
      (cl-callf org-babel-process-params (nth 2 info))
      (let* ((params (nth 2 info))
	     (cache (let ((c (cdr (assq :cache params))))
		      (and (not arg) c (string= "yes" c))))
	     (new-hash (and cache (org-babel-sha1-hash info :eval)))
	     (old-hash (and cache (org-babel-current-result-hash)))
	     (current-cache (and new-hash (equal new-hash old-hash))))
	(cond
    ...))))
  ...
)
```

`org-babel-current-src-block-location` is assigned value only in `org-babel-exp-results` which is used to prepare result to be export from org file. So, in this case, `org-babel-current-src-block-location` is nil. <org_babel_execute_src_block_src> says if `org-babel-current-src-block-location` is nil, fall back on value of `(nth 5 info)` then fall back to `(org-babel-where-is-src-block-head)`. I think the fallback method is there to increase efficiency because if fallback methods are expected to do the same thing, according to descriptions, and fallback methods involve more computation.

```emacs-lisp
(org-babel-get-src-block-info)
```

|            |                                |                                                                                                                                                                                                                                                                                     |   |     |      |        |
|------------|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---|-----|------|--------|
| emacs-lisp | (org-babel-get-src-block-info) | ((:colname-names) (:rowname-names) (:result-params both) (:result-type . value) (:results . both) (:exports . both) (:lexical . no) (:pandoc . t) (:kernel . python3) (:eval . never-export) (:tangle . no) (:hlines . no) (:noweb . no) (:cache . no) (:session . jupyter-python)) |   | nil | 4959 | (<%s>) |

Command is interned from `org-babel-execute:` prefix followed by lang.

```emacs-lisp
(cmd (intern (concat "org-babel-execute:" lang)))
```

In <org_babel_execute_src_block_src>, I find implementation of caching results interesting in that it uses hash of "info of org babel source" to determined if there is any change to the block since last run. block will be recomputed only if "info of org babel source" has changed. This is done by comparing new hash of old hash as followed.

```emacs-lisp
...
	     (new-hash (and cache (org-babel-sha1-hash info :eval)))
	     (old-hash (and cache (org-babel-current-result-hash)))
	     (current-cache (and new-hash (equal new-hash old-hash)))
...
```

Lastly, it expand noweb body (`org-babel--expand-body`), evaluate body, insert result (`org-babel-insert-result`), and run hook (`(run-hook 'org-babel-after-execute-hook')`).

That's all for code structure of computing source block. The rest is just detail which is better to learn when you really need it.

I haven't explored caching mechanism. This should be an interesting post in itself.

That's it.
Peace.
