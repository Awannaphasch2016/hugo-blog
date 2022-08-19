+++
title = "Using jq command tools to filter JSON."
author = ["Anak Wannaphaschaiyong"]
tags = ["jg", "cmd", "blog", "json"]
draft = false
+++

This blog summarizes `jq` documentation's tutorial&nbsp;[^fn:1].

If you can fully understand what the following command do, you don't need read the rest of the blog. That's pretty much sum up all `jq` can do.

```sh
curl 'https://api.github.com/repos/stedolan/jq/commits?per_page=5' | jq '[.[] | {message: .commit.message, name: .commit.committer.name, parents: [.parents[].html_url]}]'
```

If you are still confused, read on.

There are only 4 concepts in `jq` shown below.

```sh

# pipelining
jq '.[] | {name: [.key[].childkey]} '

# only apply to list
jq '.[0]' # select first json from a list
jq '.[]' # pass each json in a list one at a time.

# apply to non-list
jq '[[[[{name: .key.childkey},{name: .otherkey.childotherkey}]]]]' # only accept 1. nested lists of json 2. json
```

[^fn:1]: <https://stedolan.github.io/jq/tutorial/>
