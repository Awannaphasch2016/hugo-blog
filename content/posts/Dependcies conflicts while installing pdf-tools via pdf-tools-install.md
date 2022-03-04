+++
title = "Error log: Error in private config: config.el, (error pdf-info-epdfinfo-program is not executable) and Dependcies conflicts while installing pdf-tools via pdf-tools-install."
author = ["Anak Wannaphaschaiyong"]
tags = ["emacs", "pdf-tools", "garun", "error"]
draft = false
+++

## Current Solution as of <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-03-02 Wed&gt;</span></span>. {#current-solution-as-of-dot}

The solution only works on doom emacs only, I found that `pdf-tools` must be install with `init.el`.

I had `(package! pdf-tools)` and `:tools pdf`. Dependencies conflict is caused by endable pdf-tools two different ways as shown.

I solved the problem by remove `(package! pdf-tools)` from packages.el and only keep `:tools pdf`.

Abit of backstory, I first encounter the problem at a very early stage of using doom emacs (first 2 weeks.), so I didn't know how to properly install things. (This problem is recognized by doom emacs maintainer that installing packages in doom style are beginner mistake.)


## actions log {#actions-log}


### Gathering information {#gathering-information}

When I encountered this error, I can still open doom with `doom run`, but it is clear from the error message when doom is open that config.el is not loaded all the ways.

```md
Warning: due to a long standing Gtk+ bug
https://gitlab.gnome.org/GNOME/gtk/issues/221
Emacs might crash when run in daemon mode and the X11 connection is unexpectedly lost.
Using an Emacs configured with --with-x-toolkit=lucid does not have this problem.
Warning (initialization): An error occurred while loading ‘/home/awannaphasch2016/.emacs.d/init.el’:

Error in private config: config.el, (error pdf-info-epdfinfo-program is not executable)

To ensure normal operation, you should investigate and remove the
cause of the error in your initialization file.  Start Emacs with
the ‘--debug-init’ option to view a complete error backtrace.
```

It is important to note that doom does recognize pdf mode. (It open pdf file with pdfview mode)

As the main error message suggests `pdf-info-epdfinfo-program` can't not be executed because it doesn't exist.

This [page](https://www.reddit.com/r/emacs/comments/aa9yz3/compiling_pdftools/) encounters similar error, and it is suggested to run `pdf-tools-install`.

Running `pdf-tools-install.` output the following error.

```md
-*- mode: compilation; default-directory: "~/.emacs.d/.local/elpa/pdf-tools-20211110.513/build/server/" -*-
Comint started at Thu Nov 18 09:02:31

/home/awannaphasch2016/.emacs.d/.local/elpa/pdf-tools-20211110.513/build/server/autobuild -i /home/awannaphasch2016/.emacs.d/.local/elpa/pdf-tools-20211110.513/
---------------------------
    Installing packages
---------------------------
Skipping package installation (already installed)

---------------------------
 Configuring and compiling
---------------------------
./configure -q --bindir=/home/awannaphasch2016/.emacs.d/.local/elpa/pdf-tools-20211110.513/ && make clean && make -s

Is case-sensitive searching enabled ?     yes
Is modifying text annotations enabled ?   yes
Is modifying markup annotations enabled ? yes

test -z "epdfinfo" || rm -f epdfinfo
test -z "libsynctex.a" || rm -f libsynctex.a
rm -f *.o
epdfinfo.c: In function 'image_write':
epdfinfo.c:566:9: warning: ignoring return value of 'fwrite', declared with attribute warn_unused_result [-Wunused-result]
         fwrite (buffer, 1, width * height * 3, file);
         ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: epdfinfo-epdfinfo.o: in function `mktempfile':
epdfinfo.c:(.text.mktempfile+0x51): warning: the use of `tempnam' is dangerous, better use `mkstemp'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: warning: libXrender.so.1, needed by /home/awannaphasch2016/anaconda3/lib/libcairo.so, not found (try using -rpath or -rpath-link)
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: warning: libX11.so.6, needed by /home/awannaphasch2016/anaconda3/lib/libcairo.so, not found (try using -rpath or -rpath-link)
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: warning: libXext.so.6, needed by /home/awannaphasch2016/anaconda3/lib/libcairo.so, not found (try using -rpath or -rpath-link)
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: warning: libXau.so.6, needed by /home/awannaphasch2016/anaconda3/lib/libxcb-shm.so.0, not found (try using -rpath or -rpath-link)
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderCreateGlyphSet'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libglib-2.0.so: undefined reference to `__fdelt_chk@GLIBC_2.15'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XNextRequest'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XShmAttach'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderCompositeTriStrip'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XCreateWindow'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XShmQueryVersion'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libkrb5.so.3: undefined reference to `__poll_chk@GLIBC_2.16'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libstdc++.so: undefined reference to `aligned_alloc@GLIBC_2.16'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XEventsQueued'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XExtendedMaxRequestSize'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libglib-2.0.so: undefined reference to `memcpy@GLIBC_2.14'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderFreePicture'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderFillRectangles'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `_XReadEvents'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderCompositeTrapezoids'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XCreatePixmap'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XFreePixmap'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderCompositeText16'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libglib-2.0.so: undefined reference to `clock_gettime@GLIBC_2.17'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderQuerySubpixelOrder'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XAddExtension'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XUnlockDisplay'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XSync'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderFindStandardFormat'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderChangePicture'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XAllocColor'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderComposite'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XShmQueryExtension'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XCreateGC'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XShmDetach'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XDestroyWindow'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderCompositeText8'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderFindVisualFormat'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XSetErrorHandler'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libgio-2.0.so.0: undefined reference to `sendmmsg@GLIBC_2.14'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XShmPutImage'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XESetCloseDisplay'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderCreatePicture'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XInitImage'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libxcb.so.1: undefined reference to `XauDisposeAuth'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderSetPictureClipRectangles'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderCompositeText32'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XShmGetImage'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libglib-2.0.so: undefined reference to `getauxval@GLIBC_2.16'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XFillRectangle'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderFreeGlyphSet'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XQueryColors'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderQueryVersion'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderFillRectangle'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XMaxRequestSize'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderSetPictureTransform'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderCreateRadialGradient'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XShmCreatePixmap'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcrypto.so.1.1: undefined reference to `secure_getenv@GLIBC_2.17'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XSendEvent'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XGetDefault'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XScreenNumberOfScreen'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XInitExtension'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XChangeGC'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderFreeGlyphs'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XPutImage'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XGetImage'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XSetClipMask'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderCreateSolidFill'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderCreateLinearGradient'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libxcb.so.1: undefined reference to `XauGetBestAuthByAddr'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XCopyArea'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderFindFormat'
/HOME/AWANNAPHASCH2016/ANACONDA3/BIN/../LIB/GCC/X86_64-CONDA_COS6-LINUX-GNU/7.3.0/../../../../X86_64-CONDA_COS6-LINUX-GNU/BIN/LD: /HOME/AWANNAPHASCH2016/ANACONDA3/LIB/LIBCAIRO.SO: UNDEFINED REFERENCE TO `XRENDERADDGLYPHS'
/HOME/AWANNAPHASCH2016/ANACONDA3/BIN/../LIB/GCC/X86_64-CONDA_COS6-LINUX-GNU/7.3.0/../../../../X86_64-CONDA_COS6-LINUX-GNU/BIN/LD: /HOME/AWANNAPHASCH2016/ANACONDA3/LIB/LIBCAIRO.SO: UNDEFINED REFERENCE TO `XSETCLIPRECTANGLES'
/HOME/AWANNAPHASCH2016/ANACONDA3/BIN/../LIB/GCC/X86_64-CONDA_COS6-LINUX-GNU/7.3.0/../../../../X86_64-CONDA_COS6-LINUX-GNU/BIN/LD: /HOME/AWANNAPHASCH2016/ANACONDA3/LIB/LIBCAIRO.SO: UNDEFINED REFERENCE TO `XLOCKDISPLAY'
/HOME/AWANNAPHASCH2016/ANACONDA3/BIN/../LIB/GCC/X86_64-CONDA_COS6-LINUX-GNU/7.3.0/../../../../X86_64-CONDA_COS6-LINUX-GNU/BIN/LD: /HOME/AWANNAPHASCH2016/ANACONDA3/LIB/LIBCAIRO.SO: UNDEFINED REFERENCE TO `XRENDERSETPICTUREFILTER'
/HOME/AWANNAPHASCH2016/ANACONDA3/BIN/../LIB/GCC/X86_64-CONDA_COS6-LINUX-GNU/7.3.0/../../../../X86_64-CONDA_COS6-LINUX-GNU/BIN/LD: /HOME/AWANNAPHASCH2016/ANACONDA3/LIB/LIBCAIRO.SO: UNDEFINED REFERENCE TO `XFREEGC'
COLLECT2: ERROR: LD RETURNED 1 EXIT STATUS
MAKE[1]: *** [MAKEFILE:473: EPDFINFO] ERROR 1
MAKE: *** [MAKEFILE:368: ALL] ERROR 2
===========================
     BUILD FAILED.  ;O(
===========================
NOTE: MAYBE TRY THE '-D' OPTION.

COMINT EXITED ABNORMALLY WITH CODE 1 AT THU NOV 18 09:02:38
```


### remove `pdf-tools` from package install and uncomment `pdf` module in `init.el` {#remove-pdf-tools-from-package-install-and-uncomment-pdf-module-in-init-dot-el}

I suspected that there could be version or dependencies mismatch that cause the error, so I make sure that `pdf-tools` is removed from `packages.el` page and uncommented `pdf` module in `init.el`. I do this because I figure it is best to install dependencies in doom-like ways.

I observed that pdf-tools was rebuild when I reload doom.
I also observed that when open pdf file, doom doesn't recognise pdf file and open it as fundamental mode. (while previous to install `pdf` module via `init.el`, doom opens pdf with pdf-view mode)

Still, rerun `pdf-tools-install` still output the same error as before.

Validation: How does module loaded into doom? How is it related to loading the packages itself via straight.el or other package manager?


### replace line of code in `pdf-info.el`. Code is found [here](https://github.com/politza/pdf-tools/pull/683/commits/90852ba946c1a798f0b7b4dd412bf9d616c8cecf). {#replace-line-of-code-in-pdf-info-dot-el-dot-code-is-found-here-dot}

After replaced the line, run `pdf-tools-install` still fails.
Note: as of <span class="timestamp-wrapper"><span class="timestamp">&lt;2021-11-18 Thu&gt;</span></span>, the code is not merged into master.


### manually compile pdf-tools at `~/.emacs.d/.local/straight/repos/pdf-tools/` {#manually-compile-pdf-tools-at-dot-emacs-dot-d-dot-local-straight-repos-pdf-tools}

I decided to follow compilation guide from pdf-tools github page, see [here](https://github.com/politza/pdf-tools#compilation).

run `make -d`, I get the following message.

```md
GNU Make 4.2.1
Built for x86_64-pc-linux-gnu
Copyright (C) 1988-2016 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Reading makefiles...
Reading makefile 'Makefile'...
Using Emacs 27.1
Updating makefiles....
Considering target file 'Makefile'.
Looking for an implicit rule for 'Makefile'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.o'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.c'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.cc'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.C'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.cpp'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.p'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.f'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.F'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.m'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.r'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.s'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.S'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.mod'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.sh'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile,v'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'RCS/Makefile,v'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'RCS/Makefile'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 's.Makefile'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'SCCS/s.Makefile'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.o'.
Looking for a rule with intermediate file 'Makefile.o'.
Avoiding implicit rule recursion.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.c'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.cc'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.C'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.cpp'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.p'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.f'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.F'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.m'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.r'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.s'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.S'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.mod'.
Trying pattern rule with stem 'Makefile.o'.
Trying implicit prerequisite 'Makefile.o,v'.
Trying pattern rule with stem 'Makefile.o'.
Trying implicit prerequisite 'RCS/Makefile.o,v'.
Trying pattern rule with stem 'Makefile.o'.
Trying implicit prerequisite 'RCS/Makefile.o'.
Trying pattern rule with stem 'Makefile.o'.
Trying implicit prerequisite 's.Makefile.o'.
Trying pattern rule with stem 'Makefile.o'.
Trying implicit prerequisite 'SCCS/s.Makefile.o'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.c'.
Looking for a rule with intermediate file 'Makefile.c'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.y'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.l'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.w'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.w'.
    Trying pattern rule with stem 'Makefile.c'.
    Trying implicit prerequisite 'Makefile.c,v'.
    Trying pattern rule with stem 'Makefile.c'.
    Trying implicit prerequisite 'RCS/Makefile.c,v'.
    Trying pattern rule with stem 'Makefile.c'.
    Trying implicit prerequisite 'RCS/Makefile.c'.
    Trying pattern rule with stem 'Makefile.c'.
    Trying implicit prerequisite 's.Makefile.c'.
    Trying pattern rule with stem 'Makefile.c'.
    Trying implicit prerequisite 'SCCS/s.Makefile.c'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.y'.
    Looking for a rule with intermediate file 'Makefile.y'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile.y'.
    Trying implicit prerequisite 'Makefile.y,v'.
    Trying pattern rule with stem 'Makefile.y'.
    Trying implicit prerequisite 'RCS/Makefile.y,v'.
    Trying pattern rule with stem 'Makefile.y'.
    Trying implicit prerequisite 'RCS/Makefile.y'.
    Trying pattern rule with stem 'Makefile.y'.
    Trying implicit prerequisite 's.Makefile.y'.
    Trying pattern rule with stem 'Makefile.y'.
    Trying implicit prerequisite 'SCCS/s.Makefile.y'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.l'.
    Looking for a rule with intermediate file 'Makefile.l'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile.l'.
    Trying implicit prerequisite 'Makefile.l,v'.
    Trying pattern rule with stem 'Makefile.l'.
    Trying implicit prerequisite 'RCS/Makefile.l,v'.
    Trying pattern rule with stem 'Makefile.l'.
    Trying implicit prerequisite 'RCS/Makefile.l'.
    Trying pattern rule with stem 'Makefile.l'.
    Trying implicit prerequisite 's.Makefile.l'.
    Trying pattern rule with stem 'Makefile.l'.
    Trying implicit prerequisite 'SCCS/s.Makefile.l'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.w'.
    Looking for a rule with intermediate file 'Makefile.w'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile.w'.
    Trying implicit prerequisite 'Makefile.w,v'.
    Trying pattern rule with stem 'Makefile.w'.
    Trying implicit prerequisite 'RCS/Makefile.w,v'.
    Trying pattern rule with stem 'Makefile.w'.
    Trying implicit prerequisite 'RCS/Makefile.w'.
    Trying pattern rule with stem 'Makefile.w'.
    Trying implicit prerequisite 's.Makefile.w'.
    Trying pattern rule with stem 'Makefile.w'.
    Trying implicit prerequisite 'SCCS/s.Makefile.w'.
    Trying pattern rule with stem 'Makefile'.
    Rejecting impossible implicit prerequisite 'Makefile.w'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.cc'.
Looking for a rule with intermediate file 'Makefile.cc'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile.cc'.
    Trying implicit prerequisite 'Makefile.cc,v'.
    Trying pattern rule with stem 'Makefile.cc'.
    Trying implicit prerequisite 'RCS/Makefile.cc,v'.
    Trying pattern rule with stem 'Makefile.cc'.
    Trying implicit prerequisite 'RCS/Makefile.cc'.
    Trying pattern rule with stem 'Makefile.cc'.
    Trying implicit prerequisite 's.Makefile.cc'.
    Trying pattern rule with stem 'Makefile.cc'.
    Trying implicit prerequisite 'SCCS/s.Makefile.cc'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.C'.
Looking for a rule with intermediate file 'Makefile.C'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile.C'.
    Trying implicit prerequisite 'Makefile.C,v'.
    Trying pattern rule with stem 'Makefile.C'.
    Trying implicit prerequisite 'RCS/Makefile.C,v'.
    Trying pattern rule with stem 'Makefile.C'.
    Trying implicit prerequisite 'RCS/Makefile.C'.
    Trying pattern rule with stem 'Makefile.C'.
    Trying implicit prerequisite 's.Makefile.C'.
    Trying pattern rule with stem 'Makefile.C'.
    Trying implicit prerequisite 'SCCS/s.Makefile.C'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.cpp'.
Looking for a rule with intermediate file 'Makefile.cpp'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile.cpp'.
    Trying implicit prerequisite 'Makefile.cpp,v'.
    Trying pattern rule with stem 'Makefile.cpp'.
    Trying implicit prerequisite 'RCS/Makefile.cpp,v'.
    Trying pattern rule with stem 'Makefile.cpp'.
    Trying implicit prerequisite 'RCS/Makefile.cpp'.
    Trying pattern rule with stem 'Makefile.cpp'.
    Trying implicit prerequisite 's.Makefile.cpp'.
    Trying pattern rule with stem 'Makefile.cpp'.
    Trying implicit prerequisite 'SCCS/s.Makefile.cpp'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.p'.
Looking for a rule with intermediate file 'Makefile.p'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.web'.
    Trying pattern rule with stem 'Makefile.p'.
    Trying implicit prerequisite 'Makefile.p,v'.
    Trying pattern rule with stem 'Makefile.p'.
    Trying implicit prerequisite 'RCS/Makefile.p,v'.
    Trying pattern rule with stem 'Makefile.p'.
    Trying implicit prerequisite 'RCS/Makefile.p'.
    Trying pattern rule with stem 'Makefile.p'.
    Trying implicit prerequisite 's.Makefile.p'.
    Trying pattern rule with stem 'Makefile.p'.
    Trying implicit prerequisite 'SCCS/s.Makefile.p'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.web'.
    Looking for a rule with intermediate file 'Makefile.web'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile.web'.
    Trying implicit prerequisite 'Makefile.web,v'.
    Trying pattern rule with stem 'Makefile.web'.
    Trying implicit prerequisite 'RCS/Makefile.web,v'.
    Trying pattern rule with stem 'Makefile.web'.
    Trying implicit prerequisite 'RCS/Makefile.web'.
    Trying pattern rule with stem 'Makefile.web'.
    Trying implicit prerequisite 's.Makefile.web'.
    Trying pattern rule with stem 'Makefile.web'.
    Trying implicit prerequisite 'SCCS/s.Makefile.web'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.f'.
Looking for a rule with intermediate file 'Makefile.f'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.F'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.r'.
    Trying pattern rule with stem 'Makefile.f'.
    Trying implicit prerequisite 'Makefile.f,v'.
    Trying pattern rule with stem 'Makefile.f'.
    Trying implicit prerequisite 'RCS/Makefile.f,v'.
    Trying pattern rule with stem 'Makefile.f'.
    Trying implicit prerequisite 'RCS/Makefile.f'.
    Trying pattern rule with stem 'Makefile.f'.
    Trying implicit prerequisite 's.Makefile.f'.
    Trying pattern rule with stem 'Makefile.f'.
    Trying implicit prerequisite 'SCCS/s.Makefile.f'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.F'.
    Looking for a rule with intermediate file 'Makefile.F'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile.F'.
    Trying implicit prerequisite 'Makefile.F,v'.
    Trying pattern rule with stem 'Makefile.F'.
    Trying implicit prerequisite 'RCS/Makefile.F,v'.
    Trying pattern rule with stem 'Makefile.F'.
    Trying implicit prerequisite 'RCS/Makefile.F'.
    Trying pattern rule with stem 'Makefile.F'.
    Trying implicit prerequisite 's.Makefile.F'.
    Trying pattern rule with stem 'Makefile.F'.
    Trying implicit prerequisite 'SCCS/s.Makefile.F'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.r'.
    Looking for a rule with intermediate file 'Makefile.r'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile'.
    Rejecting impossible implicit prerequisite 'Makefile.l'.
    Trying pattern rule with stem 'Makefile.r'.
    Trying implicit prerequisite 'Makefile.r,v'.
    Trying pattern rule with stem 'Makefile.r'.
    Trying implicit prerequisite 'RCS/Makefile.r,v'.
    Trying pattern rule with stem 'Makefile.r'.
    Trying implicit prerequisite 'RCS/Makefile.r'.
    Trying pattern rule with stem 'Makefile.r'.
    Trying implicit prerequisite 's.Makefile.r'.
    Trying pattern rule with stem 'Makefile.r'.
    Trying implicit prerequisite 'SCCS/s.Makefile.r'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.F'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.m'.
Looking for a rule with intermediate file 'Makefile.m'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.ym'.
    Trying pattern rule with stem 'Makefile.m'.
    Trying implicit prerequisite 'Makefile.m,v'.
    Trying pattern rule with stem 'Makefile.m'.
    Trying implicit prerequisite 'RCS/Makefile.m,v'.
    Trying pattern rule with stem 'Makefile.m'.
    Trying implicit prerequisite 'RCS/Makefile.m'.
    Trying pattern rule with stem 'Makefile.m'.
    Trying implicit prerequisite 's.Makefile.m'.
    Trying pattern rule with stem 'Makefile.m'.
    Trying implicit prerequisite 'SCCS/s.Makefile.m'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.ym'.
    Looking for a rule with intermediate file 'Makefile.ym'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile.ym'.
    Trying implicit prerequisite 'Makefile.ym,v'.
    Trying pattern rule with stem 'Makefile.ym'.
    Trying implicit prerequisite 'RCS/Makefile.ym,v'.
    Trying pattern rule with stem 'Makefile.ym'.
    Trying implicit prerequisite 'RCS/Makefile.ym'.
    Trying pattern rule with stem 'Makefile.ym'.
    Trying implicit prerequisite 's.Makefile.ym'.
    Trying pattern rule with stem 'Makefile.ym'.
    Trying implicit prerequisite 'SCCS/s.Makefile.ym'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.r'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.s'.
Looking for a rule with intermediate file 'Makefile.s'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.S'.
    Trying pattern rule with stem 'Makefile.s'.
    Trying implicit prerequisite 'Makefile.s,v'.
    Trying pattern rule with stem 'Makefile.s'.
    Trying implicit prerequisite 'RCS/Makefile.s,v'.
    Trying pattern rule with stem 'Makefile.s'.
    Trying implicit prerequisite 'RCS/Makefile.s'.
    Trying pattern rule with stem 'Makefile.s'.
    Trying implicit prerequisite 's.Makefile.s'.
    Trying pattern rule with stem 'Makefile.s'.
    Trying implicit prerequisite 'SCCS/s.Makefile.s'.
    Trying pattern rule with stem 'Makefile'.
    Trying implicit prerequisite 'Makefile.S'.
    Looking for a rule with intermediate file 'Makefile.S'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile.S'.
    Trying implicit prerequisite 'Makefile.S,v'.
    Trying pattern rule with stem 'Makefile.S'.
    Trying implicit prerequisite 'RCS/Makefile.S,v'.
    Trying pattern rule with stem 'Makefile.S'.
    Trying implicit prerequisite 'RCS/Makefile.S'.
    Trying pattern rule with stem 'Makefile.S'.
    Trying implicit prerequisite 's.Makefile.S'.
    Trying pattern rule with stem 'Makefile.S'.
    Trying implicit prerequisite 'SCCS/s.Makefile.S'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.S'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.mod'.
Looking for a rule with intermediate file 'Makefile.mod'.
    Avoiding implicit rule recursion.
    Avoiding implicit rule recursion.
    Trying pattern rule with stem 'Makefile.mod'.
    Trying implicit prerequisite 'Makefile.mod,v'.
    Trying pattern rule with stem 'Makefile.mod'.
    Trying implicit prerequisite 'RCS/Makefile.mod,v'.
    Trying pattern rule with stem 'Makefile.mod'.
    Trying implicit prerequisite 'RCS/Makefile.mod'.
    Trying pattern rule with stem 'Makefile.mod'.
    Trying implicit prerequisite 's.Makefile.mod'.
    Trying pattern rule with stem 'Makefile.mod'.
    Trying implicit prerequisite 'SCCS/s.Makefile.mod'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.c'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.cc'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.C'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.cpp'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.p'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.f'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.F'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.m'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.r'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.s'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.S'.
Trying pattern rule with stem 'Makefile'.
Rejecting impossible implicit prerequisite 'Makefile.mod'.
Trying pattern rule with stem 'Makefile'.
Trying implicit prerequisite 'Makefile.sh'.
Looking for a rule with intermediate file 'Makefile.sh'.
Avoiding implicit rule recursion.
Trying pattern rule with stem 'Makefile.sh'.
Trying implicit prerequisite 'Makefile.sh,v'.
Trying pattern rule with stem 'Makefile.sh'.
Trying implicit prerequisite 'RCS/Makefile.sh,v'.
Trying pattern rule with stem 'Makefile.sh'.
Trying implicit prerequisite 'RCS/Makefile.sh'.
Trying pattern rule with stem 'Makefile.sh'.
Trying implicit prerequisite 's.Makefile.sh'.
Trying pattern rule with stem 'Makefile.sh'.
Trying implicit prerequisite 'SCCS/s.Makefile.sh'.
No implicit rule found for 'Makefile'.
Finished prerequisites of target file 'Makefile'.
No need to remake target 'Makefile'.
Updating goal targets....
Considering target file 'all'.
File 'all' does not exist.
Considering target file 'pdf-tools-1.0.tar'.
File 'pdf-tools-1.0.tar' does not exist.
    Considering target file '.cask/27.1'.
    File '.cask/27.1' does not exist.
    Finished prerequisites of target file '.cask/27.1'.
    Must remake target '.cask/27.1'.
cask install
Putting child 0x55d1fce51170 (.cask/27.1) PID 2737 on the chain.
Live child 0x55d1fce51170 (.cask/27.1) PID 2737
Reaping losing child 0x55d1fce51170 PID 2737
Removing child 0x55d1fce51170 PID 2737 from chain.
```

I searched the error of `make: cask command not found` and, interestingly, I found this [page](https://github.com/politza/pdf-tools/issues/335), which is an issue from pdf-tools github.

I have further check that version of `pdf-tools` from `M-x list-packages` are the latest version, see the commit on github [here](https://github.com/vedang/pdf-tools/tree/a8847b75d3487d60e27762816bdbdd23b6dc1c11).

I confirmed that epdfinfo can't be found by checking the following

1.  `M-x pdf-info-check-epdfinfo RET`
2.  from installing section [here](https://github.com/vedang/pdf-tools/tree/a8847b75d3487d60e27762816bdbdd23b6dc1c11#installing), I checked that no tar file is contained within the direcotry.


### search about `epdfinfo` installabtion problem on the latest git commit, no result found. {#search-about-epdfinfo-installabtion-problem-on-the-latest-git-commit-no-result-found-dot}

I searched for `epdfinfo` related issue on the latest git commit and found nothing.
This confirmed that the problem is more general than version conflict.


### install cask manually, and rerun `make -d` in `~/.emacs.d/.local/straight/repos/pdf-tools/` {#install-cask-manually-and-rerun-make-d-in-dot-emacs-dot-d-dot-local-straight-repos-pdf-tools}

I install cask manually from [here](https://github.com/cask/cask#installation).

when I rerun `make -d`, the same `cask caa't be found` is gone, and get the following message instead.

```md
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libxcb.so.1: undefined reference to `XauGetBestAuthByAddr'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XCopyArea'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderFindFormat'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderAddGlyphs'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XSetClipRectangles'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XLockDisplay'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XRenderSetPictureFilter'
/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld: /home/awannaphasch2016/anaconda3/lib/libcairo.so: undefined reference to `XFreeGC'
collect2: error: ld returned 1 exit status
Reaping losing child 0x55a8532ded80 PID 9340
make[2]: *** [Makefile:473: epdfinfo] Error 1
Removing child 0x55a8532ded80 PID 9340 from chain.
make[2]: Leaving directory '/home/awannaphasch2016/.emacs.d/.local/straight/repos/pdf-tools/server'
Reaping losing child 0x560ffc5badf0 PID 9336
make[1]: *** [Makefile:368: all] Error 2
Removing child 0x560ffc5badf0 PID 9336 from chain.
make[1]: Leaving directory '/home/awannaphasch2016/.emacs.d/.local/straight/repos/pdf-tools/server'
Reaping losing child 0x5577befe74b0 PID 9333
make: *** [Makefile:82: server/epdfinfo] Error 2
Removing child 0x5577befe74b0 PID 9333 from chain.
```

The above error seem to be the same as the one I observed at [Gathering information](#gathering-information).
When I rerun `pdf-tools-install`, I still get the same error as mentioned.


### Found same `collect2: error: ld` error in the latest issue of pdf-tools. {#found-same-collect2-error-ld-error-in-the-latest-issue-of-pdf-tools-dot}

I found the issue [here](https://github.com/vedang/pdf-tools/issues/42).

I stopped here because to I am unable to locate where `/home/awannaphasch2016/anaconda3/bin/../lib/gcc/x86_64-conda_cos6-linux-gnu/7.3.0/../../../../x86_64-conda_cos6-linux-gnu/bin/ld` is.

To dig into it further, I first need to locate the file and knowledge about how C program is built and how ld works may come in handy if I am on the right track on debugging this problem.


### I found solution by keeping `:tools pdf` and remove `(package! pdf-tools)` from packages.el {#i-found-solution-by-keeping-tools-pdf-and-remove--package-pdf-tools--from-packages-dot-el}
