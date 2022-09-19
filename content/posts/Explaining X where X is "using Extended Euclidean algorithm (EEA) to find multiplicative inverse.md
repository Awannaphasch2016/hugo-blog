+++
title = """
  Explaining X where X is "using Extended Euclidean algorithm (EEA) to find multiplicative inverse."
  """
author = ["Anak Wannaphaschaiyong"]
tags = ["number-theory", "crypto-engineering", "abstract-algebra", "blog", "ea", "euclidean-algorithm", "bezourt-theorem", "extended-euclidean-algorithm", "eea"]
draft = false
+++

I always get lost in the detail when learning or working on math, and I find that new math concept introduced only a few important concepts. The rest are filling in details by connecting new and old concepts in the right order using math notation.

Think of new math concepts as tools that are reusable for tasks in which tools are specialized for.

In this series of "Explaining X" where X is any mathematical concept, I will try to avoid mathematical details and will try my best to capture the newly introduced concept.

In these series, prerequisite of knowledge will be required to fully understand the blog. Keep that in mind.

I suggest reader to watch video on the topic first. The blog is served as a narrated story that designed to fit how human learn and think of things. That's it. Human thinks in narrative.

Lets start.

Euclidean algorithm (EA) is a tool that is used to find greatest command denominator (gcd). EA is interesting in that it has a recursive behavior.

One important thing to note here is that recursive behavior is attractive to algorithms implemented using computer because it allows algorithm to be efficient. Recursion is easy to optimized for maximum computer performance. A field whose focus is on computer performance naturally recursive pattern, such as cryptography engineering.

Next up, we have Bezout theorem. Bezout theorem observes a pattern that involve 2 integers and their gcd.
More precisely, \\(az + bt = d\\) where a, b are integer, and d is a gcd of z and t.

Apparently, recursive algorithm of EA output a result that can be expressed in \\(az + bt = d\\). Expressing EA using Bezout's theorem's equation, called "Bezout's identity," result in a new algorithm called extended euclidean algorithm (EEA).

Some people may argue that jumping from EA to EEA  is to trivial to give it a name, but, just like a function, when sequence of operations are used often enough, programmer will eventually convert it to a function and give it a name.

Where is EEA often used?
EEA is often used to find multiplicative inverse of a (\\(a^{-1}\\)) given a mod b.

Thinking of EEA as a function, we need to put condition on the input such that output EEA guarantees certain rules.

We know that EEA is EA expressed as Bezout's identity. We also know that gcd of relative prime number is 1. This implies that applying EEA on relative prime number will get \\(az + bt = 1\\).

To use EEA to find multiplicative inverse, we need to change EEA'a input conditions as followed

1.  the 2 integers must be relative primes.
2.  one of the integer must be a prime.
3.  the two input, s and t, must be of form (s mod t) where t is prime.

Given the input condition above, applying EEA on s and t where t is prime. we know that output EEA on the 2 input can be expressed as

\\[as + bt = 1 \text{ (mod t)}\\]

then
\\[as + 0 = 1 \\]

Using multiplicative inverse property, \\(x \* x^{-1} = 1\\), we get \\(a = s^{-1}\\).

This shows condition of when to use EEA to get multiplicative inverse.

This is my first blog on math. It is still awkward to write. My writing style is expected to evolve as I get more familiar with writing about math.

That's it.
peace.
