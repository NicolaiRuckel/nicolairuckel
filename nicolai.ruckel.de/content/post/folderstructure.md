---
title: "Reorganizing my Home Directory Structure"
date: 2018-03-11T18:41:46+01:00
draft: true
---

## Introduction
As I searched for a scan of my bachelor degree certificate and fought my way
through my messed up folder structure I realized two things:

1. I never scanned my bachelor certificate (which is very insignificant for this
   post)
2. I really have to clean up my file system.

The biggest problem was that for a lot of files there were multiple possible
locations. For example tablatures of original music was sometimes in
`~/Documents/music/tabs/$PROJECTNAME` and sometimes in
`~/Documents/projects/music/$PROJECTNAME` or in subfolders of that.
In addition to that `~/Documents` contained a lot of files that weren't
documents.  The same was true for programming-related projects which could be in
either `~/dev` or `~/Documents/projects/$PROJECTNAME`.  Since I am a computer
science student and hobby ~~musician~~ bassist, these were my most important
files.

While this structure doesn't necessarily can be applied in the same way for
other people since they have different needs, this maybe gives some helpful
ideas.

## Overview
All of those directories are lower case because I don't see the point of upper
case names.  Also this gives me the possibility to create uppercase folders that
are listed on top on Linux systems.

```
.
├── bin
├── desktop
├── documents
|   ├── banking
|   ├── invoices
|   ├── scans
|   └── work
├── dotfiles
├── downloads
├── dropbox
├── media
|   ├── apps
|   ├── audio
|   |   ├── audiobooks
|   |   ├── music
|   |   ├── samples
|   |   └── tones
|   ├── pictures
|   |   └── photos
|   ├── text
|   |   ├── sheet music
|   |   └── books
|   ├── video
|   |   ├── movies
|   |   ├── tv-shows
|   |   └── anime
|   |       ├── movies
|   |       └── tv-shows
|   └── games
├── projects
|   ├── dev
|   |   ├── configs
|   |   ├── games
|   |   ├── latex
|   |   ├── programming
|   |   └── web
|   ├── audio
|   |   ├── music
|   |   └── other
|   ├── pictures
|   └── video
└── uni
```

## Thoughts On My Structure

The folders `desktop`, `downloads` and `dropbox` just have to be
*somewhere else* than the rest of my files they get separate folders on the top
level of my home directory and we can ignore those from now on.

Then there are my `dotfiles` for which it doesn't make much sense to move them
deeper in the directory structure.  Theoretically those could be in
`~/projects/dev/configs` but they get used in a very different way then the
configuration files in `~/projects/dev/configs`.  I want to copy my dotfiles on
machines I work, run the deploy script and start to work.  I don't want the
deploy script to care about any directory structure.

Finally there is the `bin` directory which is in my `PATH` and mostly calls
scripts from my dotfiles with machine specific parameters.  It's a bit redundant
but I don't want all my scripts to be in the `PATH`.  Maybe this will be moved
in the dotfiles some day.  It contains no compiled binaries and therefore would
well with git.

If we ignore all those folders and all third-level folders we get a more cleaned
up structure:

```
.
├── documents
|   ├── banking
|   ├── invoices
|   ├── scans
|   └── work
├── media
|   ├── apps
|   ├── audio
|   ├── pictures
|   ├── text
|   ├── video
|   └── games
├── projects
|   ├── dev
|   ├── audio
|   ├── pictures
|   └── video
└── uni
```

My first classification was between original content that I work on (in
`projects`) and `media` content from other people.  The subfolders are mostly
the same with a few a exceptions which I'll discuss later.

You'll notice that there are two remaining folders.  The first one is
`documents` which contains documents that are relevant to me as a person or
created by myself.  This differs a bit from `projects` which are always original
content which is one reason why this is a separate folder.  Another reason is
that I (and most other people) am used to a documents folder on the top level in
my home directory.  Finally I want to synchronize `documents` differently than
`projects`.  While `projects` is a very large folder which contains about
300 GB, `documents`'s size is only 3.5 GB.  This means I can synchronize them
between my desktop and my laptop without running out of space on my laptop which
only contains one small SSD.  In addition to that the files in `documents` are
needed more often when I'm travelling.

The last folder is `uni`, which contains everything related to my studies.  I
need those files on my laptop since I can't take my desktop to the university
for obvious reasons.

Maybe I will buy a bigger SSD for my laptop to have enough space for all of
those folders (except for `media`) but I'm not sure if I would change my
structure then.  On my desktop some of these are links to my HDD, some are on my
SSD (for space reasons) but this isn't really relevant here.

In `media` I first differentiate the different kinds of media.  For the
non-interactive ones (`audio`, `pictures`, `text` and `video`) this is pretty
straightforward I think.  The interactive ones are separated in `games` and
`apps`.  Theoretically I could divided everything first in interactive and
non-interactive but this didn't seem very practically to me.  If I had less
games (not that I have that many) I probably would put them all into `apps`.
`games` is also the place for my Steam library.

All of those folders contain various subdirectories. I didn't list all of them
because most of them won't matter to anyone else and I just want to give an idea
of what I did.

The `projects` folder also contains a `dev` directory (which is a difference
from `media`) which contains projects which have to to with code.

## Descriptions of the Folders
This is a bit more detailed description of what I put into which folder.  Some
of those informations are already mentioned and are just repeated for
completion's sake.

### ~/bin
This is a place for binaries that are in my `PATH`.  Most of them are little
shell scripts.  All of them are very specific to the machine.  For example there
is a script that turns the second display of my desktop machine off, starts Kodi
and after Kodi gets closed turns the second display on again.

### ~/desktop
I don't even know why this folder exists.

### ~/documents
Text-based files like bank statements, invoices or scans of documents that are
related to me.

### ~/dotfiles
My [dotfiles](https://github.com/RanaExMachina/dotfiles).

### ~/downloads
This is a huge mess of files that should be sorted elsewhere.

### ~/dropbox
I'm not a huge fan of Dropbox but I need this for some projects.

### ~/media
Everything media related that is done by other people.

#### ~/media/apps
Installer and binaries of various applications that I backuped but probably
never use again.  This excludes games.

#### ~/media/audio
Audio files such as music or audio books.

#### ~/media/pictures
Photos, screenshots, logos, etc.

#### ~/media/text
Non-personal text files like books or sheet music.  Sheet music may seem a bit
weird here but it fits nowhere else.

#### ~/media/video
Movies and TV shows.  Also a separate folder for anime.

#### ~/media/games
Game binaries that don't have a place in `/opt` (e.g. exe files of old RPG
Maker games) and my Steam library.

### ~/projects
This is everything I worked on.  This mostly copies `~/media` with the addition
of some folders and some simplifications.

#### ~/projects/dev
All projects that have to do with code. Most of them are just git repositories
or include git repositories.

##### ~/projects/dev/configs
Configuration files that are not in `~/dotfiles` either because they have weird
locations or are for other machines (e.g. gitolite configs).

##### ~/projects/dev/games
Various attempts to program a game.  Maybe someday I finish something.

##### ~/projects/dev/latex
Also known as the macro hell.  Here are my LaTeX templates.

##### ~/projects/dev/programming
Programming that isn't a game (i.e. will get finished someday).

##### ~/projects/dev/web
Web pages.

#### ~/projects/audio
All audio-related projects. `~/projects/audio/music` contains a folder for each
band I worked with.

#### ~/projects/video
There was a time I wanted to make movies.  This is also the reason why I need
big HDDs.

### ~/uni
All study-related stuff with a folder for each (of the way too many) semesters.
This could be inside `~/projects` but I decided to give it its own folder since
there is a lot of stuff I didn't really do by myself (lecture scripts etc.).

## Open Questions
Sometimes I have to use a virtual machine to check if my software works on other
systems but I have no idea where to put the virtual machine files.  Currently
they are on the top level in `HOME` which I don't really like but I don't know a
better place yet.
