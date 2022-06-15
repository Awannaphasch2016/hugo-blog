+++
title = "Enable x11 display in WSL2"
author = ["Anak Wannaphaschaiyong"]
tags = ["blog"]
draft = false
+++

Resources are provided in [my roam research note](https://roamresearch.com/#/app/AdaptiveGraphStucture/page/I1FI0mnUx).

I successfully connect x-apps via x11 protocol by first installing and launching xming server. Xming application provides x11-server. Then, I need to tell the wsl2 "address and port of X11 server to connect wsl2 application to" (my note on x11 can be seen [here](https://roamresearch.com/#/app/AdaptiveGraphStucture/page/f433e8apo)) X11 server is enlisted as WSL2 entrusted DNS which located in resolve.conf. (my note on resolve.conf can be seen [here](https://roamresearch.com/#/app/AdaptiveGraphStucture/page/I1FI0mnUx).) From the image below, x11 server port is `0.0`.

{{< figure src="/ox-hugo/screenshot_20220430_153555.png" width="300px" >}}

In practice, I need to put the following in shell configuration file. In my case, it was `.zshrc`.

```bash
export DISPLAY="`grep nameserver /etc/resolv.conf | sed 's/nameserver //'`:0"
```

My friend gets it working by replacing `:0` with `:0.0`. I couldn't tell you why, but that's something to be careful about.
