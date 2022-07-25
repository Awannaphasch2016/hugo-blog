+++
title = "Getting source code of distributed binary package in Ubuntu"
author = ["Anak Wannaphaschaiyong"]
tags = ["linux", "blog", "debug", "ubuntu"]
draft = false
+++

[This](https://superuser.com/questions/388890/is-there-a-way-to-extract-the-source-code-from-deb-or-rpm-packages) stack exchange post state the following.

```org
Debian and RPM packages don't contain source code, only the compiled result. However, you can fetch the source packages - SRPMS, or the Debian description, patch, and original tarball.
```

That's it. You can only download file that are provided in url where target deb file is located. Which files will be provided? Only package maintainers can determine that. Therefore, there could be a scenario where no source codes are available for download.

As an example of what could be provided, files contained in <https://releases.hashicorp.com/vagrant/2.2.9/> are shown below.

{{< figure src="/ox-hugo/screenshot_20220703_184738.png" width="300px" >}}

With good knowledge about file extension convention, in this case, best bet to find source code is to look into zip file. Unfortunately, in this case, zip file only contains binary file of `vagrant`. Fortunately, `vagrant` is an open source and one can obtain source code from its github page, [here](https://github.com/hashicorp/vagrant).

Welcome to the world of software. You get what you get, so make the best of it.

Below, I will explain step by step on how to obtain source code of distributed binary package in Ubuntu.

To follow along, I will use `hello` packages in Ubuntu as an example package to download source code locally. However, any other packages available in `apt-get` can be used.

First, you need to uncomment `deb-src` in `source.list`.

```sh
chmod 777 /etc/apt/source.list # change file permission from read-only to editable.
vim /etc/apt/source.list
sed ":%s/# deb-src/deb-src/g" /etc/apt/source.list # replace '# deb-src' with 'deb-src'
```

\#+END_SRC

Then, you can download source code of hello packages.

```sh
sudo apt-get source hello
```

Running the above on `Ubuntu 20.04.4` will result in a known bug&nbsp;[^fn:1]. As of <span class="timestamp-wrapper"><span class="timestamp">[2022-07-03 Sun]</span></span>, I have no clue what `_apt` or  `/var/lib/update-notifier/package-data-downloads/partial/` mean.

```sh
sudo chown _apt /var/lib/update-notifier/package-data-downloads/partial/
```

The command above should download `hello` source code to current directory. Now, you can edit it as you want.

Lastly, make sure to change permission of `/etc/apt/source-list` back to readonly. I don't know about security much, but it seems to logical.

```sh
sudo chmod u=r,g=r,o=r /etc/apt/sources.list # change file permission from editable tto read-only
```

That's it.
Peace.

[^fn:1]: [couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied) [duplicate]​](https://askubuntu.com/questions/954862/couldnt-be-accessed-by-user-apt-pkgacquirerun-13-permission-denied)
