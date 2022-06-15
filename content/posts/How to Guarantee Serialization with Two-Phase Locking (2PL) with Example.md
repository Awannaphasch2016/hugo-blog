+++
title = "How to Guarantee Serialization with Two-Phase Locking (2PL) with Example"
author = ["Anak Wannaphaschaiyong"]
tags = ["book", "blog", "database"]
draft = false
+++

This is a summary on Chapter 21.1 Two-Phase Locking Techniques for Concurrency Control from Fundamental of Database system by Pearson 2015.

The goal of this blog is to give a concrete example on how 2PL's schedule is `guaranteed to be serializable`.

<a id="figure--Figure-21.3"></a>

{{< figure src="/ox-hugo/screenshot_20220427_180350.png" caption="<span class=\"figure-number\">Figure 1: </span>Figure 21.3" width="500px" >}}

<a id="figure--Figure-21.4"></a>

{{< figure src="/ox-hugo/screenshot_20220427_180447.png" caption="<span class=\"figure-number\">Figure 2: </span>Figure 21.4" width="500px" >}}

Figure <Figure_21.3> and figure <Figure_21.4> uses the same set of locks which is provided in Shared/Exclusive locks including read_lock, write_lock and unlock. However, figure <Figure_21.4> is considered 2PL while figure <Figure_21.3> is not. Note that 2PL is Shared/Exclusive locks with additional protocol called `two phase locking protocol`. The different between 2PL and shared/exclusive lock is that 2PL guarantee serialization while the other doesn't.

The book also mentioned that while 2PL protocol guarantee sheduling serializability. It doesn't permit all possible serializable schedules.

Serialization is achieved via by converting figure <Figure_21.3> to figure <Figure_21.4> because figure <Figure_21.4> reorders write_lock(X) and write_lock(Y) to be right before unlock(Y) and unlock(X), respectively.

Naturally, two questions arises.

Considering \\(T\_1\\), the first question is "why does order of write_lock(X) and unlock(Y) matter?" To answer this question, one have to think in term of constraint that would results in serialization.  In \\(T\_{1}\\), value of Y is read first. This means Y should be locked until `X = X+Y` is written. This condition is satisfied by placing write_lock(X) above unlock(Y). This can be read as "write X before unlock Y."

To satisfy the above constraints, in \\(T\_1\\), write_lock have to be placed on X until `X = X +Y` is executed. This guarantees that X will not be changed until `X = X+Y` is executed. At the same time, \\(T\_{1}\\) doesn't need to be any constraint on Y except that \\(T\_1\\) needs to be informed of any changes made in Y before `X = X+Y` will be computed.

Secondly, considering \\(T\_1\\), "can write_lock(X) be anywhere else above unlock(Y)?" The answer is yes, but the reason that it is placed right above unlock is for efficiency by reducing queue waiting time. Recall that when write_lock is called, neither read nor write can be called on the same data. `To guarantee this efficiency, distant between write_lock(X) and write_item(X) needs to be minimized`.
