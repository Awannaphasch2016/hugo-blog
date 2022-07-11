+++
title = "A Note of X where X = AWS IAM services."
author = ["Anak Wannaphaschaiyong"]
tags = ["aws", "blog", "iam"]
draft = false
+++

In `AWS IAM`, a `policy` is the smallest entity of permission. There are types of policies: `resources-based policy`, `identity-based policy`, and `session-based policy`.

<a id="figure--aws-policies"></a>

{{< figure src="/ox-hugo/screenshot_20220711_154129.png" caption="<span class=\"figure-number\">Figure 1: </span>aws policies" width="500px" >}}

Policies can be attached to the following "identity": `user` (1 account can have more than 1 users), `role`, and `group` (a group has many `user`)&nbsp;[^fn:1]. `user`, `role`, and `group` are called `identity`. In AWS identity is called `IAM identity` and `user`, `role`, and `group` are called `IAM user`, `IAM role`, and `IAM user group`, respectively.

Roles are used for "task-oriented policy." Imagine the following scenario where you want to create policies to allow `AWS lambda` to read from `AWS S3` storage and store data to `AWS dynamoDB` database. You don't care who will do this task. You only care about the task. More specifically, collection of policies that make the task possible.

[^fn:1]: [IAM Identities (users, user groups, and roles)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html)
