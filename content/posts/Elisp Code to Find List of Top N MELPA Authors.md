+++
title = "Elisp Code to Find List of Top N MELPA Authors"
author = ["Anak Wannaphaschaiyong"]
tags = ["elisp", "blog", "implementation"]
draft = false
+++

```emacs-lisp
;; https://www.reddit.com/r/emacs/comments/t9qs6h/need_help_listing_all_emacs_super_developers/
(require 'url)
(require 'cl-lib)
(defvar url-http-end-of-headers)
(defvar smelpa-json nil "Melpa recipe JSON data.")

(defun smelpa-json ()
  "Return an alist of MELPA recipe metadata."
  (or smelpa-json
      (setq smelpa-json
            (with-current-buffer (url-retrieve-synchronously "https://melpa.org/archive.json")
              (goto-char url-http-end-of-headers)
              (json-read)))))
(defun smelpa-packages-by-author ()
  "Return alist of form: ((author . (package-url...)))."
  (let (authors)
    (cl-loop for (_ . data) in (smelpa-json)
             do (when-let ((props     (alist-get 'props data))
                           (url       (alist-get 'url props))
                           (parsed    (url-generic-parse-url url))
                           (filename  (url-filename parsed))
                           (tokens    (split-string filename "/" 'omit-nulls))
                           (author    (intern (car tokens))))
                  (if (alist-get author authors)
                      (push url (alist-get author authors))
                    (push (cons author (list url)) authors))))
    authors))
(defun smelpa-most-published-authors (n)
  "Return alist of form ((author . (url...))) for top N published MELPA authors."
  (let ((authors (smelpa-packages-by-author)))
    (cl-subseq
     (cl-sort authors #'>
              :key (lambda (cell) (length (cdr cell))))
     0 (min n (length authors)))))
```
