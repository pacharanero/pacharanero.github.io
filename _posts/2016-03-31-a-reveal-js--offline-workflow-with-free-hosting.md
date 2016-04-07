---
title: 'Using Reveal.js for presentations, with a (mostly) offline git-based workflow, and free hosting'
author: pacharanero
layout: post
---

<iframe src="http://www.bawmedical.co.uk/nhswifi2015/#/" width="100%" height="400" frameBorder="0" text-align="center"></iframe>

<br/>

## Reveal.js

For a few years now I've been using the JavaScript-based, interoperable presentation platform called [Reveal.js - the HTML presentation framework](http://lab.hakim.se/reveal-js/#/)

It's great for presentations that look different enough to be visually interesting, without hijacking the purpose of the presentation by over-embellishing the slides. The slides are not the point of the presentation. The *presentation* is the point of the presentation.

I try to only use visual aids when I **need** to back up the point I'm making with a visual. I often use large, simple, full screen images for this, and little else.

Open standards and open source is important to me. I also run Linux so I don't have the option of KeyNote or PowerPoint (not that I would actually want to use them anyway)

I guess I *could* use [Libreoffice Impress](https://www.libreoffice.org/discover/impress/) or something like it, but I've found that the editing tools are not that great, especially trying to work out what is going on with a template affecting all your slides. (In Reveal.js you can style everything easily and consistently using CSS/SASS)

LibreOffice is also just a PowerPoint clone, meaning it apes a lot of PowerPoint behaviours that I don't like and don't need - including the automatic hierarchy of bullet points that has been [criticised for implying semantics that aren't there](http://www.edwardtufte.com/tufte/powerpoint).

I quite like [Google Slides](https://www.google.co.uk/slides/about/), but when travelling a lot on trains with decidedly wobbly WiFi, there's just too much activity on the wire to work with Google Docs, and it can seriously hamper productivity.

So: I now use Reveal.js with a (mostly) offline git-based workflow, which means I can work locally, and then when I want to push to the remote repo, the presentation is hosted by GitHub pages. It also means I can branch the repo and make new changes without changing the live Internet-based version, until I'm ready.

## Prerequisites

* familiarity with [git](https://git-scm.com/) for local and remote work
* basic HTML and text editing skills
* basic CSS understanding and skills
* some idea of how to host pages with GitHub pages. I already have 'organisation' level GitHub pages set up on my GitHub username, so new presentations appear as {bawmedical.co.uk}/{presentation-name}

## Howto

1. create a new GitHub repo with the name you want the presentation to be known as (NB: other online git-integrated source control platforms are available :-) )
1. `git clone` this repo to a suitable local directory, which should create a subdirectory of the same name as your presentation
1. Get a blank reveal.js presentation from https://github.com/hakimel/reveal.js/releases - this comes with some 'placeholder' or demo slides which are all the introduction you need. I have a blank presentation stored locally that includes all the theming I like to use, and has some of my preferences preset. So I just copy and paste the code
1. Start adding content to your slides. The Reveal.js documentation is very simple, and very helpful.
1. Make local commits (eg `git commit -am "commit message"`) as required. Usually I just work in the master branch, and make commits irresponsibly infrequently. So sue me.
1. To push to GitHub for hosting of the presentation, create a local `gh-pages` branch (`git checkout -b "gh-pages"`)
1. When you push this `gh-pages` branch to GitHub, your' pages will be hosted as a subdirectory of your main site (in my case http://www.bawmedical.co.uk/ is the base URL, and presentations are hosted at http://www.bawmedical.co.uk/presentation-repo-name)

## Upsides
* All your **content** is in HTML
* All your **styling** in in CSS/SASS and therefore can be applied consistently to all slides, a subset of slides, or individual elements. Global templates therefore behave more predictably than templates do in LibreOffice (awful) or even Google Slides (better than LO but still not great)
* You can present direct from the Internet, so there's no hassle with USB keys and local machines, you just fire up Chrome, hit the URL of your presentation, full-screen it with F11 and get going.
* Because it's just HTML5, in a browser, you can present via Chromecast to basically anything (see my other blog on this)
* Your presentations get hosted online for free, and you don't need to cosy up with the Militiary-Industrial-SlideShare-LinkedIN Complex.
* Because your presentations are natively web-based, you can easily share URLs of your slides before, during, or after your presentation. Great for tweeting the link at an event. 
* You can embed a presentation in a web page with an `iframe` (like I have done at the top of this page)

## Downsides
* You can't easily get other people to work with you collaboratively on these slides, unless they also understand enough about HTML/CSS/Git etc to be able to grok it. In those cases, I guess would recommend Google Slides.
* Reveal.js seems to be a pretty large library, so initial page loads are sloooowwwww, as well as any fonts, image and other assets you included. Once downloaded, it's pretty cool.
* When event organisers ask for your USB key with your presentation on it, and you say 'don't worry I only need a browser', they universally look a little freaked out.
