+++
title = "Working with D-Bus in Linux's systemd."
author = ["Anak Wannaphaschaiyong"]
tags = ["linux", "blog", "systemd", "dbud", "middleware"]
draft = false
+++

Quoting "D-Bus integration in Emacs"&nbsp;[^fn:1], D-Bus is defined as followed

> D-Bus is an inter-process communication mechanism for applications residing on the same host. The communication is based on messages. Data in the messages is carried in a structured way, it is not just a byte stream.

According to&nbsp;[^fn:1], name of client application is "a series of identifiers separated by dots", but an application can install multiple objects under its name which are represents as path like syntax -- separated by `/`. Communications to these applications are either "methods" (requests/responds) or "signals" (pub/sub). These form of communication is called "interface" of the application. Name of Interfaces is append to application's name.

To be honest, I still don't know what is the different between object and application. According to&nbsp;[^fn:1], I see "object" (represented as path) as a way to create arbitrary name to refers to a specific application.&nbsp;[^fn:2]

Say I want to add new client D-Bus application to add `org-clock` notification functionality in Emacs, I have to put add systemd service file at `/usr/share/dbus-1/services/`. Note that I am using Ubuntu distro on Wsl2 on Window 10. Example of the file name is `org.freedesktop.Notifications.service`. I speculate that the file is an "interface" to application named `org.freedesktop.Notifications`

In `org.freedesktop.Notifications.service`, I wrote

```md
[D-BUS Service]
Name=org.freedesktop.Notifications
Exec=/usr/lib/notification-daemon/notification-daemon
```

That's it.

Peace.

~milfex-lostex

[^fn:1]: <https://www.gnu.org/software/emacs/manual/html_mono/dbus.html#Overview>
[^fn:2]: this works like `wire` in Urbit's Gall application.
