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
|   └── video
└── uni
```

Some of these are links to my HDD, some are on my SSD but this isn't relevant
here.

## Descriptions

### ~/bin
This is a place for binaries that are in my `PATH`.  Most of them are little
shell scripts.


### ~/desktop
I don't even know why this folder exists.

### ~/documents
Text-based files like ebooks, invoices or decklists for MtG and Scrolls.

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
Audio files such as music or audiobooks.

#### ~/media/pictures
Photos, screenshots, logos, etc.

#### ~/media/video
Movies and TV shows.  Also a separate folder for anime.

#### ~/media/games
Game binaries and my Steam library.

### ~/projects
This is everything I worked on.  This mostly copies `~/media` with the addition
of some folders and some simplifications.

#### ~/projects/dev
All projects that are done in text editors. Most of them are just git
repositories or include git repositories.

##### ~/projects/dev/configs
Configuration files that are not in `~/dotfiles` either because they have weird
locations or are for other machines.

##### ~/projects/dev/games
Various attempts to program a game.  Maybe someday I finish something.

##### ~/projects/dev/latex
Also known as the macro hell.  Here are my LaTeX templates.

##### ~/projects/dev/programming
Programming that isn't a game (i.e. will get finished someday).

##### ~/projects/dev/web
Web pages.

#### ~/projects/audio
All audio-related projects.

##### ~/projects/audio/music
This contains my original music and folders for bands I worked with.

##### ~/projects/audio/other
Old podcast-like audio projects.

#### ~/projects/video
There was a time I thought I should make movies.

### ~/uni
All study-related stuff with a folder for each (of the way too many) semesters.
This could be inside `~/projects` but I decided to give it its own folder since
there is a lot of stuff I didn't really do by myself (lecture scripts etc.).

## Open Questions

### Documents
I'm not sure whether `documents` should be on the top level or inside `media`
since some of those files are consumable media by other people (e.g. ebooks) and
others are my own work (e.g. letters or invoices).  Maybe those should be
separated in `~/media/text` and `~/documents`.

### Virtual Machines
Sometimes I have to use a virtual machine to check if my software works on other
systems but I have no idea where to put the virtual machine files.  Currently
they are on the top level in `HOME` which I don't really like but I don't know a
better place yet.
