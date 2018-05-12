---
title: "Minimal Desktop Notifications"
date: 2018-05-12T21:23:56+02:00
draft: true
---

When I started my computer science (and media) studies in 2010, I used a lot of
notifications: When I got an instant message, when I got an email, when someone
highlighted me on IRC, when the next song started playing and so on.
At some point I got really annoyed by all those popup notifications and only
accepted badges on the dock icon or in the status bar.

Since I switched from macOS to Linux as my main operating system, I used
[i3](https://i3wm.org/) as my window manager.
Instead of popup notifications, my programs set the [urgency
hint](https://tronche.com/gui/x/icccm/sec-4.html#s-4.1.2.4) which was similar to
what I was used to from my Mac.
This was fine as long as I used programs that could set the urgent hint but
there were more and more programs that did not have such an option.
After I looked into Gnome again and had a very minimal option for notifications
with all my programs.
Finally I decided that non-tiling window manager are to inconvenient to use and
did not want to use Gnome anymore and started again to find a solution for
minimal notifications with i3 that did not restrict me too much in the choice of
my programs.
I started researching and asked on
[Reddit](https://www.reddit.com/r/i3wm/comments/7egp8x/minimal_notifications/)
but I could not find a solution.
My compromise was using [Dunst](https://github.com/dunst-project/dunst) which at
least had the option to make notifications small, non-animated and persistent so
I did not have to pay attention to them all the time.
Of course this wasn't a good solution and from time to time I would search for
better solutions until I found something very interesting today in the man page
of Dunst:

    Within rules you can specify a script to be run every time the rule is
    matched by assigning the 'script' option to the name of the script to be
    run.
    When the script is called details of the notification that triggered it will
    be passed via command line parameters in the following order: appname,
    summary, body, icon, urgency.
    [...]
    If the notification is suppressed, the script will not be run unless
    always_run_scripts is set to true.

So I could filter *all* messages, suppress the notification and run a script
instead, which gets passed the application name as the first parameter with this
rule:

    [urgent_hints]
            summary = "*"
            script = ~/dotfiles/scripts/set_urgent_hint.sh
            format = ""

The script just takes it's first argument (the application name) and sets the
urgency hint with `wmctrl`.

```sh
#!/bin/sh

wmctrl -r $1 -b add,demands_attention
```

You can find all the configuration and script files in my [dotfiles
repository](https://github.com/RanaExMachina/dotfiles).
