+++
title = "How to write latex using org mode? Minmum things you need to know."
author = ["Anak Wannaphaschaiyong"]
draft = false
+++

What you need to know to start writing latex in org mode is to understand how `org-export-dispatch` include/exclude/map org mode component to latex equivalent. You can learn all about these info by reading org manual on the topic, [here](https://orgmode.org/manual/Exporting.html).

You should know a little bit about org mode header arguments and LaTeX to fully follow the blog.

In this blog, I will just present minimal info for you to start writing latex in org mode.

This is the org header for a minimum use.

```org
#+TITLE: Ensemble Approaches for Streaming Networking Classification
#+DATE: <2022-03-03 Thu>
#+AUTHOR: Anak Wannaphaschaiyong
#+EMAIL: awannaphasch2016@fau.edu
#+OPTIONS: toc:nil
#+LATEX_CLASS: IEEE
```

From above code, you need to define things to be used in `#+LATEX_CLASS`. LaTeX class's variable avaible in the header argument is defined in `org-latex-class`. From above you see that I define LaTeX class variable with `org-latex-class`.

```emacs-lisp
(add-to-list 'org-latex-classes
             '("IEEE" "\\documentclass{IEEEtran}"
  ("\\section{%s}" . "\\section*{%s}")
  ("\\subsection{%s}" . "\\subsection*{%s}")
  ("\\subsubsection{%s}" . "\\subsubsection*{%s}")
  ("\\paragraph{%s}" . "\\paragraph*{%s}")
  ("\\subparagraph{%s}" . "\\subparagraph*{%s}")))
```

From the doc you see that

```org
  (class-name
    header-string
    (numbered-section . unnumbered-section)
    ...)
```

so, we get
"IEEE" is a class name.

`\\documentclass{IEEEtran}` is `header-string`

and

```emacs-lisp
("\\section{%s}" . "\\section*{%s}")
  ("\\subsection{%s}" . "\\subsection*{%s}")
  ("\\subsubsection{%s}" . "\\subsubsection*{%s}")
  ("\\paragraph{%s}" . "\\paragraph*{%s}")
  ("\\subparagraph{%s}" . "\\subparagraph*{%s}"
```

is list of `(number-section . unnumbered-section)`

Out of these components, its worth to understand that `(number-section . unnumbered-section)` directly mapped to how `org-export-dispatch` map org header to latex equivalent.

Using the above `(number-section . unnumbered-section)`, If you have content of org file as followed.

```org
* first header
** second header
*** third header
```

First header will be map to section, second header will be mapped to subsection, and so on.

Without these defined, `org-export-dispatch` will map first header to enumerate and whatever that is equivalent of subenumerate, and so on. (I don't recall the name percisely.)

I provide example of minimum content below

```org
#+TITLE: Ensemble Approaches for Streaming Networking Classification
#+DATE: <2022-03-03 Thu>
#+AUTHOR: Anak Wannaphaschaiyong
#+EMAIL: awannaphasch2016@fau.edu
#+OPTIONS: toc:nil
#+LATEX_CLASS: IEEE

* First Header

Lorem $1+1$ ipsum dolor sit amet, consectetur adipiscing elit. Cras lorem
nisi, tincidunt tempus sem nec, elementum feugiat ipsum. Nulla in
diam libero. nunc tristique ex a nibh egestas sollicitudin.

\begin{equation}
1+ 1
\end{equation}

- 1
- 2
- 3
- 4

** sub header :noexport:
Mauris efficitur vitae ex id egestas. Vestibulum ligula felis,
pulvinar a posuere id, luctus vitae leo. Sed ac imperdiet orci, non
elementum leo. Nullam molestie congue placerat. Phasellus tempor et
libero maximus commodo.
* Second header
something bruh
```

That's it.

Peace.
