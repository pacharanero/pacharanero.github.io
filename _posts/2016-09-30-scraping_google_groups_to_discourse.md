---
title: Scraping Google Groups to Discourse
layout: post
date: 2016-09-30
---
**Update 2016: I've since found a better way to do Google Group to Discourse migrations and have written an updated howto [here](https://meta.discourse.org/t/migration-of-google-groups-to-discourse/48012):**

Someone who knew more about Google Groups had managed to make a script which can extract the messages from a Google Group as a series of .mbox files. Discourse already has an importer for these .mbox files.

I wrote a [fairly hacky script](https://github.com/pacharanero/google_group.to_discourse) which connects the exporter to the importer, for a more seamless migration. Please do [contact me](mailto:marcusbaw@gmail.com) if you've tried the script, I'd like to know it's being used, and of course if you have any problems too please contact me and I'll try to help.

<br/>

------

<br/>

Back in 2015, eHealth Insider (shortly afterwards rebranded Digital Health Intelligence) were working on a new Social Collaboration Platform for the CCIO Network and Health CIO Network. We experimented with various platforms including [Drupal Commons](https://www.drupal.org/project/commons) and [Open Atrium](http://www.openatrium.com/#!/) (both of which were too complex to set up and have looking nice, without having to become a PHP dev, which nobody really wanted ;-) )

We eventually settled for [Discourse](http://www.discourse.org) (and the rest is history). As part of this I had to migrate the existing CCIO Leaders' Network and Health CIO Networks over from the Google Groups they are in over into Discourse.

Discourse has a nice REST API so the Discourse end of things was pretty easy. On the Google Groups side, it proved very difficult to extract the content of the messages cleanly. I tried a variety of approaches but ended up having to scrape the content from the viewed, rendered pages using Selenium Webdriver (really a web testing tool, not a scraping tool)

The **deprecated** original script I used is [here](https://github.com/pacharanero/google_group.to_discourse) 

Here's a [screencast](https://youtu.be/RZLD8tXREvw) of how it looked as Selenium iterated through all the pages in the Google Group while it scraped them and sent them to Discourse.
