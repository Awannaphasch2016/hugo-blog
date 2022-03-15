+++
title = "Connection between org-roam-bibtex (orb), org-roam and org-ref."
author = ["Anak Wannaphaschaiyong"]
draft = false
+++

Org-ref manage citation entry, referenced citation, PDF, and note just fine. But the problem arise when trying to link notes created org-ref as a node in org roam. This is the problem that orb solve to allow PDF notes to be inserted as a org roam node. To summarize, the problem that orb solve to integrate org-ref functionalities into org-roam ecosystem.

All org roam does is the following:

1.  create name of a note file using org roam file name convention.
2.  add `:ROAM_REFS:` as a note property whose value is an org-ref citation.

`orb-insert-link` creates new node (from citation entry shown in citation completion mechanism like helm-bibtex) if the node of that entry hasn't yet existed.

That's it.

Peace.
