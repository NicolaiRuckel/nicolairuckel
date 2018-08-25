---
title: "Minimal Desktop Notifications"
date: 2018-05-12T21:23:56+02:00
draft: false
---

When I started my computer science[^1] studies in 2010, I used to get
notifications for a lot of events.
Even non-events like information on the song that was currently playing
resulted in a pop-up notification.
At some point I got really annoyed by all those pop-up notifications and
replaced all of them with badges on the dock icon or in the status bar.
This also had the advantage that I could leave my laptop for while, come back
and did not miss anything important since all notifications persisted the whole
time.

Since I switched from macOS to Linux as my main operating system, I used
[i3](https://i3wm.org/) as my window manager.
By default, it doesn't support notifications, but programs could set the
[urgency hint](https://tronche.com/gui/x/icccm/sec-4.html#s-4.1.2.4) which
resulted in a highlighted workspace and therefore was similar to what I was used
to from my Mac.
This was fine as long as I used programs that could set the urgent hint but
there were more and more programs that did not have such an option.
Sometimes, I had to choose older applications with less features or worse UI
simply because they could set the urgency hint and newer ones couldn't.

At some point this got very unsatisfying and I switched to the Gnome desktop,
which allows to just show a little circle in the status bar when new
notifications occurred.
This very minimal option for showing notifications was supported by all my
programs.
While I was in heaven notification-wise, I struggled with the window manager.
Finally, I decided that non-tiling window manager are to inconvenient to use and
started again to find a solution for minimal notifications with i3 that did not
restrict me too much in the choice of my programs.
I started researching and asked on
[Reddit](https://www.reddit.com/r/i3wm/comments/7egp8x/minimal_notifications/)
but I could not find a solution and no one could help me.
My compromise (as recommended by someone on Reddit) was using
[Dunst](https://github.com/dunst-project/dunst) which at least had the option to
make notifications small, non-animated and persistent so I did not have to pay
attention to them all the time.
Of course this wasn't a good solution and from time to time I would search for
better solutions.
The I found something very interesting today in the man page
of Dunst:

```plaintext
Within rules you can specify a script to be run every time the rule is
matched by assigning the 'script' option to the name of the script to be
run.
When the script is called details of the notification that triggered it will
be passed via command line parameters in the following order: appname,
summary, body, icon, urgency.
[...]
If the notification is suppressed, the script will not be run unless
always_run_scripts is set to true.
```

So I figured I could filter *all* messages, suppress the notification and run a
script instead, which gets passed the application name as the first parameter
with this rule:

```plaintext
[urgent_hints]
        summary = "*"
        script = ~/dotfiles/scripts/set_urgent_hint.sh
        format = ""
```

The script just takes it's first argument (the application name) and sets the
urgency hint with `wmctrl`.

```sh
#!/bin/sh

wmctrl -r $1 -b add,demands_attention
```

You can find all the configuration and script files in my [dotfiles
repository](https://github.com/NicolaiRuckel/dotfiles).

[^1]: Actually, the programme is called *Computer Science and Media*.
