+++
title = "What the f*** is wiki.c2.com? and its potential for mainstream adoption."
author = ["Anak Wannaphaschaiyong"]
tags = ["wiki", "blog"]
draft = false
+++

-   last edit
    -   <span class="timestamp-wrapper"><span class="timestamp">[2022-06-26 Sun]</span></span>

One of my life long projects is to build an `index protocol` using tokenomics for thought sharing. For now, on <span class="timestamp-wrapper"><span class="timestamp">[2022-06-26 Sun]</span></span>, I call it "The Forest."

On <span class="timestamp-wrapper"><span class="timestamp">[2022-06-26 Sun]</span></span>, I stumbled upon `wiki.c2.com`. I was reading about it for a couple hours, and `wiki.c2.com` seems to share lots of philosophy that `The Forest` holds. Two hours in, however, I can't seem to get a grip of some very basic stuff like how to read it? what is it for? Words they use can only be understood by those who already know it. Each page is structured like a blob of discussions. There are no sense of direction. What I mean is. Whenever I attempt to read one of the page, I can't answer "Where do I start reading this?"

I designed The Forest to avoid this type of problem. The Forest is designed such that scope of things to read is narrowed by searching for questions one has before searching for answer.

Studied history of Stack Overflow, I am aware that The Forest attempts to solve the same problem that Stack Overflow solved. Stack Overflow was founded as one of many question-answering platform. However, the differences between Stack Overflow and its competitors are that users can find answer easily on Stack Overflow. It solves this by having superior "answer indexing mechanism." If I am right about comparing The Forest to Stack Overflow, The Forest will be Stack Overflow of "Sharing Ideas as Wiki" platforms where `wiki.c2.com` is an example.

According to comments on a Reddit thread, people regards `wiki.c2.com` as "one gigantic cultural artefact that needs to stay afloat."&nbsp;[^fn:1] One of the user nicely summarized `wiki.c2.com` as followed:

> [Wiki.c2.com is] the first wiki wiki and the model for Wikipedia, the Portland Pattern Repository was a place where many of the principles of Agile software development were hashed out through discussion of the leading members of that movement. It was closer to the discussion pages of Wikipedia, where someone would write on a topic, and another would add more dimension or a counterpoint to what was written. Instead of creating a page of what, say, Extreme Programming was, pages full of discussion of how it was implemented on site or how it could be improved were generated; when it became too large, someone might refactor that page into several different pages, such as XP Principles, XP Practices, XP implementations, and so on.

Another user jokingly make a responds comment as followed:

> Elsewhere on the net, there are two sites that convention mandated a warning flag for fear of clicking the rest of the afternoon following interesting things. TVTropes... and `wiki.c2.com`.

To me, `wiki.c2.com` feels like an open bar for hippie thinkers to engage in any topic on their minds. Its one of those place where anyone can endlessly wander (from page to page) and get lost like a runaway vacation. In a way, it comforts me. I recalled this feeling of comfort. I encountered a place/culture like this before. And it was `emacs`. My first love.

On a serious note, the problem I found related to implementations of Wiki are the followings:

1.  Different wiki has different protocol of how to interact with it.
2.  Wikis lacks credibility as a "source of truth." They functionality and usage resemble platforms that encourage honest, open, and opinionated discussion.
3.  People misuse public wiki as their own back of an envelope's scratch pad.
4.  It is not useable beyond a fun "get away" read.

Point 1 and 2 can be fixed with indexing protocol with tokenomics. An example of indexing protocol is [The Graph](https://thegraph.com/en/) which is described on their main site, as of <span class="timestamp-wrapper"><span class="timestamp">[2022-06-26 Sun]</span></span>, as "an indexing protocol for querying networks like Ethereum and IPFS". In summary, The Graph is indexing protocol for data while The Forest is indexing protocol for thought.

On the last point, point 3, I see that it can be fixed by using version control to "fork" idea of others and "grow it yourself" (Grow as in growing `seeds of thought` into your own `evergreen forest`). Forking process of existing wikis already existed&nbsp;[^fn:1], but the current practice of forking doesn't fully embrace full functionality of version control. This is the point I wanted to make. It is possible to fully replicate version control functionality. To be exact, replicating Git way of doing version control as it is the rightful winner of `version control war`. This includes "staging," "commit," "stashing," "blame," and "cherry picking." Go crazy. Be creative.

Furthermore, on point 4, to enhance usability and embrace The Forest's ideology, using a combination of `language server protocol` (LSP) of server-client like approach and use `resembrance agents` as an API to provide utilities such as providing list of (thought) completion via `(thought) completion framework`.

Ultimately, integrating and using `The Forest` driven by `resembrance` agent capability should feel no different from `thinking.` That's it. A complete extension of your brain's capacity. My goal standard of what `second brain` should be.

That's it.
Peace.

[^fn:1]: [The c2 wiki was down](https://news.ycombinator.com/item?id=12705774)
