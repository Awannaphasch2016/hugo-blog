+++
title = "Install LaTeX on Ubuntu is not as simple as you think."
author = ["Anak Wannaphaschaiyong"]
date = 2022-03-03T00:00:00-05:00
draft = false
creator = "Emacs 25.3.1 (Org mode 8.2.10)"
+++

First of all, I am no expert in LaTeX. I am just a dude who has (a lot) of trouble installing LaTeX and was trying to solve it.

From this experience, I learn important lesson is always start digging from the official documentation of the target packages/libraries. This is because there are many two types of solution in general: `general solution` and `environment specific solution`.

In this case, its clearly a environment specific problem which required environemnt speicific solution.

Before jump in to the solution, lets me explain diganosis of a broken LaTeX state and what I wanted to achieve.

First of all, I wanted to write research paper with LaTeX in org-mode Emacs and sync it to Overleaf, so my advisor can review it and see my progress.

I first encountered the problem when I tried to update LaTex packages with `tlmgr`. it shows the following error message.

```txt
erros-tlmgr: unexpected return value from verify_checksum: -5
```

What is that? you asked. If you have know abit about security, you know that fail to verify checksum means key or content of the package is corrupted. Apprently, the maintainer of (CTAN? LaTeX?) this have his key to expire every year. What should you do now? I don't know how to solve the solution from this clue either, so I tried approaching it from another perspective.

Gathering more information, I found that `apt-get` install `texlive` (`apt-get install texlive-latex-extra.`) into different directory than "general solution" that I found. After a bit more digging, I realised that LaTeX depedencies installed in Ubuntu is outdated, and it is more generally accepted to install LaTeX with this thing call `install-tl.sh` script.

`install-tl.sh` script itself has distro specific version either `window` or `Unix` (distro is put as a suffix in the name). Nonetheless, you can just install `install-tl.sh` which will support all distro. In my case, I use `install-tl-ubuntu.sh`

Apparently, by running `./install-tl.sh` script, your problem should disapear. Of course, there is a catch, it only solved your problem if this is the first approach you used to install LaTeX. If you installed it with Ubuntu `apt-get`, some weird dependencies conflict may still persist.

To make sure that you only have 1 version of LaTeX which is managed by `install-tl.sh`, you need to remove all packages of LaTeX and its depenencies! by running `sudo apt-get purge texlive-base`. Then you still have to manually check if there are another dependencies of TeX. (maybe installed by other apt-get packagkes.) by running `dpkg -l | grep texlive` and manually remove leftover dependencies with `apt purge texlive-XXX`

Also, you need to restart computer and then add `/usr/local/texlive/2021/bin/x86_64-linux` (or something similar) to PATH environment variable.

And that's it, hence, the title.

peace.
