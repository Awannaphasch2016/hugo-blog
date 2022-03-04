+++
title = "how to set recurring todo tasks with org mode in emacs?"
author = ["Anak Wannaphaschaiyong"]
draft = false
+++

First thing is to understand that behavior of a header block in org mode is dictated by properties.

I want to set repeating task to have the following functions

-   when I change from TODO state to DONE state, a header block will log "state changes" with time stamp.

That is all the requirement I need for recurring tasks.

This can be done by setting the following

-   set `:REPEAT_TO_STATE:` property under the header with `org-set-property`
-   set either `DEADLINE` (`org-deadline`) or `SCHEDULE` (`org-schedule`) with recurring syntax&nbsp;[^fn:1] , for example, adding `.+1d/+3d` to timestamp represent recurring every 1 day or 3 day. (it will be randomly assigned by org mode.).

first you must set header as followed

```org
* TODO work on quiz 3
DEADLINE: <2022-03-03 Thu  .+1w>
:PROPERTIES:
:REPEAT_TO_STATE: TODO
:LAST_REPEAT: [2022-03-02 Wed 16:26]
:END:
```

Then when you change from TODO to DONE state, header will log "state change" in a `:LOGBOOK:` property, and DONE state will automatically change to TODO. (so you will not see DONE state appears.). Deadline is then reset to the next date and time.

```org
* TODO work on quiz 3
DEADLINE: <2022-03-03 Thu .+1w>
:PROPERTIES:
:REPEAT_TO_STATE: TODO
:LAST_REPEAT: [2022-03-02 Wed 16:26]
:END:
:LOGBOOK:
- State "DONE"       from "TODO"       [2022-03-02 Wed 16:26]
:END:
```

[^fn:1]: [8.3.2 repeated tasks](https://orgmode.org/manual/Repeated-tasks.html)
