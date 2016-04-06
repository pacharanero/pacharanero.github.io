---
title: 'Get the Apple MagicMouse &#8216;back&#8217; feature with a Logitech M305 mouse and Ubuntu or Linux Mint'
author: pacharanero
layout: post
categories:
  - Uncategorized
---
I hated my MacBook when I tried one earlier this year. I gave it 6 months near enough, but I couldn&#8217;t get used to the erratic minimise&#8217; behaviour of the Dock, the US keyboard layout, the bloody cost of any decent apps or accessories, and actually I was pretty disappointed by the standard of the built-in apps like Numbers. After that trial period I sold the MacBook, bought a Dell M3800 and learned just what fun it can be to try to install Linux on EFI bootloaders 😉

**But one thing I really liked & missed from the MacBook was the swipe Back and Forward browsing feature of the Magic Mouse.**

I decided to see if I could get the &#8216;left&#8217; and &#8216;right&#8217; switches on the mouse wheel of my Logitech M305 wireless mouse to do the same thing.

Turns out it&#8217;s not hard, I thought I&#8217;d write it down here as there didn&#8217;t seem to be any complete and basic guide out there yet, and also I might forget one day so it&#8217;s here as a &#8216;message in a bottle to future self&#8217; (thanks to <a title="http://graysoftinc.com/" href="http://graysoftinc.com/">James Edward Gray</a> of the <a title="http://rubyrogues.com/" href="http://rubyrogues.com/">@RubyRogues</a> podcast for introducing me to this concept!)

<a title="https://help.ubuntu.com/community/ManyButtonsMouseHowto" href="https://help.ubuntu.com/community/ManyButtonsMouseHowto">This</a> guide on Ubuntu Forums was my main source, but the was a bit weirdly laid out and the imwheelrc entry wasn&#8217;t quite right for me, so I thought it would be worth doing a quick blog post about it.

##Install imwheel

`sudo apt-get install imwheel`

Edit `/etc/X11/imwheel/imwheelrc` in your text editor *du jour*, inserting the below snippet:


    #firefox Back and Forward mapped to mouse wheel Left and Right<br />
    "^Firefox$"<br />
    None,Left,Alt_L|Left<br />
    None,Right,Alt_L|Right<br />


I think I then needed to start imwheel manually (type `imwheel` in a terminal window) to test it was working

It worked almost suspiciously well, making me wonder what it&#8217;s broken&#8230;. But so far nothing&#8217;s borked. Tested on Mint 17 Qiana with M305 mouse, but should work pretty identically on any Ubuntu variant, and quite similarly on non-Ubuntu Linuces (plural of Linux surely). And should also work just as well with any mouse that has mouse wheel left and right switches.

And I put an entry in Startup Applications so it should start automatically when the machine boots up. This also seems to work.

##Update February 2016:

I switched to Google Chrome after 10 years of using Firefox, as recent updates (FF43-45 on Linux) have been REALLY slow. The `imwheel` hack also works on Chrome:


    #chrome Back and Forward mapped to mouse wheel Left and Right
    "^google-chrome$"
    None,Left,Alt_L|Left
    None,Right,Alt_L|Right

And perhaps unsurprisingly, it also works with the Logitech MX Anywhere and Anywhere 2 Mice...
