+++
title = "Iteration and Recursion in Hoon."
author = ["Anak Wannaphaschaiyong"]
tags = ["urbit", "blog", "hoon", "functionalprogramming"]
draft = false
+++

Code below is a part of `Exercise: A Playing Card Library`&nbsp;[^fn:1] section in `Hoon School 7. Libraries`.

```hoon
++  shuffle-deck
  |=  [unshuffled=deck entropy=@]
  ^-  deck
  =/  shuffled  *deck
  =/  random  ~(. og entropy)
  =/  remaining  (lent unshuffled)
  |-
  ?:  =(remaining 1)
    :_  shuffled
    (snag 0 unshuffled)
  =^  index  random  (rads:random remaining)
  %=  $
    shuffled      [(snag index unshuffled) shuffled]
    remaining     (dec remaining)
    unshuffled    (oust [index 1] unshuffled)
  ==
```

Notice that random card is selected from the following 2 lines.

```hoon
shuffled      [(snag index unshuffled) shuffled]
unshuffled    (oust [index 1] unshuffled)
```

`unshuffled` remove random card.
`shuffled` select the same random card that is removed by `unshuffled`.

[^fn:1]: <https://developers.urbit.org/guides/core/hoon-school/H-libraries#exercise-a-playing-card-library>
