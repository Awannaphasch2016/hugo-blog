+++
title = "Original OOP is fundamentally different to Modern OOP."
author = ["Anak Wannaphaschaiyong"]
tags = ["oop", "blog", "design", "philosophy"]
draft = false
+++

Modern OOP is misused and misunderstood. Modern OOP create an object to abstract over the object internal state. Originally, OOP is intended to be used to abstract objects over the most important processes that take place within environment in which objects exit. This is done by exposing interfaces that are capable of interacting with the outside world&nbsp;[^fn:1]. In the other word, an object should be built to be resurgence, to protect itself from dynamic environment. This should be done not by shielding itself from outside world, but by allowing itself to be adaptable to the world in which its in.

Alan Kay argues that smallest unit of program should be objects not data structure and procedure. Data structure is static and procedure don't remember its state. On the other hand, objects can dynamically update its state.

Reflecting on the philosophy of OOP, I find more similarity to functional programming (FP) than to modern OOP. FP can be implemented to be recursive, to remember its state. FP is built on pure functions which is a function with no side effects. This property of having no side effect encapsulates pure functions by "exposing interface that capable of interacting with the outside world" -- I quote the exact same description used to describe OOP.

I argue that the reason that Alan Kay don't see functional programming as a type of OOP because he focuses too much on implementing programmable objects to be equivalent of physical objects which are fatal flaw in his believe because programmable objects live in world of bit while physical objects live in world of atom. However, his idea of having programmable objects as smallest unit of exchange may still be largely valid as one user named mpweiher from Hacker News explains Alan Kay view on FP. He put it nicely as followed&nbsp;[^fn:2]

> I obviously can't tell you what he's thinking, but I can make an educated guess:
> In the video (and almost anywhere else you look) you'll note he talks about recursion on the concept of "computer" as a way to scale, because that way the parts are as powerful as the whole.
>
> If you split that concept into the sub-notions of "procedures" and "data", you no longer have that recursive principle, and "functions" in this context are sufficiently equivalent to procedures.
>
> Going the other way, functions don't really scale up, many if not most things in computing are not functions to be computed. One could argue that computers and "computer science" are misnamed, as computation is more the exception than the rule. "Data-around-shufflers" would be more appropriate.
>
> I didn't see the exact monad references, but they look like ways of working around the fact that the "function" primitive is inappropriate. It is really nice, mind you, and has wonderful properties. Kind of like circles as the basis for astronomical orbits: they are "perfect", but the world isn't perfect in the same way, so trying to model the imperfect world with these perfect primitives leads to having to introduce epicycles/monads.

In summary, mpweiher argues that a "pure function" in FP is not equivalent of an "object" in OOP because pure function is too "perfect" and is not capable of describing the real world. His premise lead to a conclusion that monad is needed to patch "imperfection" caused by flawed assumption built on "pure function." If there exists such an "OOP object" claimed by Alan Kay, we may not need "monad-like tool" after all.

[^fn:1]: <https://youtu.be/NTRLK2F_THY?t=633>
[^fn:2]: <https://news.ycombinator.com/item?id=13035577>
