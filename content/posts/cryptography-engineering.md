+++
title = "Cryptography Engineering"
author = ["Anak Wannaphaschaiyong"]
tags = ["cryptography"]
draft = false
+++

## Blog <span class="tag"><span class="blog">blog</span></span> {#blog}


### Explaining X where X = Montgomery form for efficient multiprecision multiplication arithmetic. <span class="tag"><span class="modular_arithmetic">modular-arithmetic</span></span> {#explaining-x-where-x-montgomery-form-for-efficient-multiprecision-multiplication-arithmetic-dot}

Prerequisites are the following

-   Residue class of modulo N is all \\(a\\) that satisfy \\(a + kN\\) where N is a constant and \\(k \in \mathbb{Z}\\).

Montgomery multiplication is a method for performing fast modular multiplication.

The algorithm uses the Montgomery forms of \\(a\\) and \\(b\\) to efficiently compute the Montgomery form of \\(ab \mod N\\). The efficiency comes from avoiding expensive division operation.

Montgomery form depends on a constant \\(R > N\\) which is coprime to \\(N\\). The constant R can be chosen so that division by R is easy. In practice, \\(R\\) is always a power of two, since division by powers of two can be implemented by bit shifting.

Computation speed of Montgomery multiplication is beneficial when many multiplication are performed in a row e.g. exponential. This is because convert number \\(a\\) and number \\(b\\) into Montgomery form and their product out of Montgomery form means that computing a single product by Montgomery multiplication is slower than the conventional or `Barett reduction` algorithms.

Addition and subtraction in Montgomery form are the same as ordinary modular addition.
\\((a \mod R) + (b \mod R) = (a+b) \mod R\\)
\\((a \mod R) - (b \mod R) = (a-b) \mod R\\)

On the other hand, multiplication in Montgomery form are the different to ordinary modular multiplication
\\((aR \mod N)(bR \mod N) \mod N = (abR)R \mod N\\)

We know that R and N are coprime. Using to `Bezout's identity`, we get \\(RR'-NN'=1\\) where \\(0 < R' < N \text{ and } 0 < N' < R\\) (I am not sure why \\(0 < R' < N \text{ and } 0 < N' < R\\) has to be true. I am only aware of a condition that \\(R > N\\). Intuitively, the condition holds when \\(R >> N\\), but I am not sure for the all cases where \\(R > N\\))

Since \\(R'\\) is always exists, we get \\(ab \mod N = abR' \mod N\\).
