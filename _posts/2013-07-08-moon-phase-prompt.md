---
layout: post
title: Moon phase prompt
date: 2013-07-08
categories: [bash]
tags:
- osx
- bash
---
There was a popular post on boingboing a while back that showed how to turn your [OS X shell-prompt into a hamburger](http://boingboing.net/2013/04/03/howto-turn-your-shell-prompt-i.html).  The gist of it is that you use a built-in emoji font, which happens to have a hamburger.


To look at the fonts yourself, check [here](http://reviews.cnet.com/8301-13727_7-57353404-263/how-to-use-the-os-x-character-viewer/) to see how to open the character viewer.  There are lots of symbols there, but a few caught my eye:

![Emoji moons](/assets/moons.png "Emoji Moons")


The hamburger is cool, but phases of the moon would be even cooler.  After a bit of googling, I found [this gist](https://gist.github.com/matthewmcvickar/5299479), which came very close to solving the problem, but didn't quite get there. 


However, it didn't take too long to get things fixed up:


{% gist 5312617 current_moon_phase.sh %}


There are two functions, the first returns the current phase day, using the simple calculation from [here](http://www.ben-daglish.net/moon.shtml).  Basically, we know that 1970-01-07T20:35 (592500 in unix epoch time) was a new moon, so we find the difference between right now and that time and mod it by the lunar period, 2551443 seconds.  The second function uses this phase day to return the correct icon, which probably won't appear correctly in your browser.


To use this, simply put this script as current_moon_phase.sh somewhere in your path and make sure it is executable (chmod u+x current_moon_phase.sh).  Then, in your .bashrc file, you can change your prompt by doing something like this:

    export PS1="\w $(current_moon_phase.sh) "

I've been using this for a few months now and, while a bit frivolous, it's informative and not too obtrusive.  The only minor issue I have found is that the background of the font only seems to work with pure white or black backgrounds.  If your terminal is somewhat transparent or not quite black or (eww) white, you will notice the background of the font.

Here is what mine looks like currently:

![moon phase prompt](/assets/prompt.png "Moon Phase Prompt")

Unfortunately, it's a new moon, so you can't see too much at the moment.
