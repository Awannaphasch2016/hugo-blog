+++
title = """
  A Note On X Where X = "adding jump state to command."
  """
author = ["Anak Wannaphaschaiyong"]
tags = ["evilmode", "blog", "note"]
draft = false
+++

"Adding jump state to command." implies that position (`(point)`) that the added command is evaluated is added to jump state. In the other word, you can get back to `(point)` that you executed the command by using `(better-jumper-jump-forward)`.

I was trying to add "jump state" to `(+spell/previous-error)` and `+spell/next-error`.

Note that `+spell` prefix means this command is provided by a Doom's module. From a quick glance into the code, it is clear that --- just like other Doom's module --- it implements branching condition to allow fallback behavior based on context such as current mode or available packages.

As of <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-11-22 Tue&gt;</span></span>, I understand that `better jumper` is an Emacs's package whose job is to provide "jumping back and forward functionality". Vanilla Emacs has its own implementation, but, in my opinion, vim's implementation is better -- it is provided by `evil-mode`.

Trying to add "evil's jump state to command" in Doom Emacs is confusing to me because `better-jumper` doesn't provide function that allow command to remember where it "jumped" from -- lets call this behavior "adding jump state to command." Still, I found that I can simulate this behavior by evaluating <2258328192>.

<a id="code-snippet--2258328192"></a>
```emacs-lisp
(progn
  (better-jumper--push)
  (+spell/previous-error))
```

This finding was a deadline. I expected it because it was expecting such obvious usage to be provided by the package itself. I was right. Since I use `evil-mode`, the package that provides this support function is `evil-mode`. This fact was not clear until after I found the solution.

I wasn't familiar with macro and structure in Elisp, so I didn't know what information to focus on when reading code in evil package. By searching for keys words like `jump` and tinkering with functions that have "jump state". I was able to figure out that "jump state" is provided by keyword `:jump t`. Copied and Pasted code from functions with desired behavior, I added `:jump t` to `(evil-next-flyspell-error)`, see <2519460702>. Still, this didn't work. I stuck again.

<a id="code-snippet--2519460702"></a>
```emacs-lisp
(evil-define-motion evil-next-flyspell-error (count)
  "Go to the COUNT'th spelling mistake after point."
  :jump t
  (interactive "p")
  (dotimes (_ count)
    (evil--next-flyspell-error t)))
```

Now, since I learned about keywords and have a metal framework of how `evil-mode` works, I was able to find this Reddit's thread titled "[evil-mode - jump back to last position.](https://www.reddit.com/r/emacs/comments/cdwmua/evilmode_jump_back_to_last_position/)", and found the correct answer by `RuleAndLine`. He commented that

> Like others are saying, you want C-o. For commands that don't set a jump by default, you want to add something like this to your init file:
>
> (evil-add-command-properties #'foo :jump t)
>
> Edit: this works for any emacs command, not just the ones defined by evil. So, like, I use (evil-add-command-properties #'org-goto :jump t) so I can go to a random org heading then jump back to where I was before.

Hence, the correct answer is

```emacs-lisp
(evil-add-command-properties #'+spell/next-error :jump t)
(evil-add-command-properties #'+spell/previous-error :jump t)
```

As of <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-11-22 Tue&gt;</span></span>, I still don't know how evil use properties to selectively produce behavior based on keyword, but, at this point, this seems like a trivial work, so I omitted it here.

That's it.

Peace.

~milfex-lostex
