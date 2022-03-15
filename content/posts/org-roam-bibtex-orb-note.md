+++
title = "Org Roam Bibtex Orb Note"
author = ["Anak Wannaphaschaiyong"]
draft = false
+++

## Blog {#blog}


### Connection between org roam bibtex (orb) and org ref. {#connection-between-org-roam-bibtex--orb--and-org-ref-dot}

Org-ref manage citation entry, referenced citation, PDF, and note just fine. But the problem arise when trying to link notes created org-ref as a node in org roam. This is the problem that orb solve to allow PDF notes to be inserted as a org roam node. To summarize, the problem that orb solve to integrate org-ref functionalities into org-roam ecosystem.

All org roam does is the following:

1.  create name of a note file using org roam file name convertion.
2.  add `:ROAM_REFS:` as a note property whose value is an org-ref citation.

That's it.

Peace.


## keybinding {#keybinding}

| commands             | key | doom keys | custom keys | descriptions |
|----------------------|-----|-----------|-------------|--------------|
| org-roam-bibtex-mode |     |           |             |              |
| orb-note-actions     |     |           |             |              |
|                      |     |           |             |              |
