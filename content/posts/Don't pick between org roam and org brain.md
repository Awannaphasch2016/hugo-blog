+++
title = "Don't pick between org roam and org brain. Use them together!!"
author = ["Anak Wannaphaschaiyong"]
draft = false
+++

-   ref
    -   list of dicussion about using org roam and org brain together
        -   [Reddit post: org brain and org roam](https://www.reddit.com/r/emacs/comments/gz4lk8/org_brain_and_org_roam/)
        -   [Org brain issue: (Idea) Org roam brain mode](https://github.com/Kungsgeten/org-brain/issues/340)

I personally use org roam to add notes. It is a great tools for connecting ideas and notes.

But if i am being honest, graph visualization is disspointingly useless. I am not I am not the only one.

For the past 3-4 years also, I have seen attempt to make grpah visualization useful.
Some even use machine learning to power up the graph features, [Nodus Labs](https://www.youtube.com/channel/UCK2IvRB36OUwXwMRD1iDmvg) tried running machine learning on top of roam research graph&nbsp;[^fn:1].

In summary, None of them really work. No one adopt it. Those features are bummer.

Then, I found `org brain`. Well, I know about it for a while, but I never tried it out.

Abit of back story, `org brain` is a rip off of `The Brain` app. (This is why free software is amazing.)

As a evil mode user, `org brain` was really awkward to adopt. This is because it doesn't have built to support evil mode.

Given it more time and looking pass the awkwardness, I started to understand that `org brain` main benefit is from explicitly linking things together.

Now, you may thing "explicitly linking things? bummer. Next." Not so far, unlike other explicit link that come before it such as heirarchical structure (like putting things in folder) and tagging system. (incluing grouping tags, inheritance tags, etc. Org brain allows one to link any two "entry" together.

There are two types of link in org brain.

1.  parent-child
2.  friend-friend

Furthermore, a link can hold attribute. (e.g. Dad -love-&gt; son).

To sum it up, org brain can add explicity linking capability to org roam, which make the graph features of org roam useful, finally.

This form of implicit and explicity linking/group are everywhere. (I should be a standard practice really if you ask me.)

I use it all the time. The one that I recall right away is having notes in a folder (Implicit heirarchical structure). To group notes in a more meaning full ways, I use bookmark.
For example, on the left is bookmark entr and on the right is where file is located.

```nil
books/books to read           ~/org/notes/books/books-to-read.org
books/collection of books     ~/Documents/Books/
config/doom emacs/snippet     ~/.emacs.d/.local/straight/repos/snippets/
config/doom emacs/snippet/ma  ~/.doom.d/snippets/org-mode/
config/doom emacs/snippets/o  ~/.doom.d/snippets/org-mode/attr-latex
contacts                      ~/org/contacts.org
emacs regex                   ~/org/notes/regex-notes.org
evaluation.py                 /mnt/c/Users/terng/OneDrive/Documents/Working/tgn/evaluation/evaluation.py
examples/emacs/packages/org   ~/Scratches/Examples/Emacs/Packages/org-drill/spanish.org
examples/emacs/packages/org   ~/Scratches/Examples/Emacs/Packages/org-ref/example.org
glossaries/blockchain         ~/org/glossaries/blockchain.org
glossaries/docker             ~/org/glossaries/docker.org
```

Org roam and org brain though are not meant to be used together. Its features compliment each other perfectly.

That's it.

Peace.

[^fn:1]: [Visualize your roam research notes to generate new nodes](https://www.youtube.com/watch?v=ePLNXN_cg-w)
