+++
title = """
  A Note On X Where X = "Emac's Combobulate Package"
  """
author = ["Anak Wannaphaschaiyong"]
tags = ["combulate", "blog", "emacs", "note"]
draft = false
+++

Lets inspect `combobulate-navigate-previous` by step into the function.

The following functions are called in order:

1.  `combobulate-navigate-previous`
2.  `combobulate--move-point-to-node`
    responsible for display and move node.
3.  `(combobulate--navigate 'previous)`
    pass `previuos` to `combobulate--navigate`
4.  `combobulate--nav-get-prev-sibling`
    get sibling node by query its parents node and get all of its nodes.
    sibling nodes are arrange in order, so getting previous or next siblings nodes is easy.
5.  `combobulate--nav-get-sibling-nodes`
    outputs list of nodes
6.  `seq filter`
    check for matched node.

Note that getting a node is done by using tree-sitter query. Tree-sitter API provides such query functions.

That's it.

Peace.

~milfex-lostex.
