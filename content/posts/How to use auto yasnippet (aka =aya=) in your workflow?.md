+++
title = "How to use auto yasnippet (aka aya) in your workflow?"
author = ["Anak Wannaphaschaiyong"]
tags = ["aya", "blog"]
draft = false
+++

All of the content I presented below can be found at [Auto-YASnippet Github repo](https://github.com/abo-abo/auto-yasnippet).

Auto-Yasnippet (aka aya) provides the following interactive commands: `aya-create`, `aya-expand`, `aya-persiste-snippet`, and `aya-open-line`:

I don't quite understand `aya-open-line` yet, so I will not be explaining it here.

This snippet package support ad-hoc style of editing workflow where you can create useful snippet to be reused as you editing.

Without `aya`, one would have do the following

1.  go to `yassnippet` directory.
2.  implement snippet template which may required multiple reload of the `yassnippet` directory via `yas-reload-all`.
3.  switch back to the to buffer you wish to apply the template.
4.  insert template and edit it.

`aya` simply skip the above step and automatically create `yasnippet` template base on context which may be one line or multiple line.

Here is how one can use `aya`. imagine you have function `count_of_red(color)` and you want to count three colors: red, blue, and green.

You can start by writing template on the line in the same buffer you are editing.

```python
count_of_~red = get_total("~red");
```

note: `~` is a `aya-marker` which will mark word to be replaced.

Then, you will call `aya-create` with point (cursor) on the same line. Note, `~` should now gone, and you should get the following.

```python
count_of_red = get_total("red");
```

To reused the template, you just created with `aya-create`. Just run `aya-expand` on the line you want to insert the new template.

Done! Blazing fast!

Oh, I heard you want to save the template to a snippet? run `aya-persist-snippet`. Save.

That's it.

Peace.
