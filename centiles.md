---
layout: default
title: 
id: centiles
active: active
permalink: /centiles
---

## Centiles

My wife is a School Nurse and back in about 2013 she asked me if there was any kind of App to calculate child growth centiles. I looked extensively and it turned out (at the time) that there weren't any. This was the start of a journey that led me to find out where the Centile chart data tables come from, and to discover that they are proprietary - copyright of the Medical Research Council.

To get use of these 'UK90 LMS tables' I had to apply for a licence to use them - it only took a mere 9 months from applying to being sent a licence agreement. The MRC didn't charge me anything for this, but the length of time it took was simply unacceptable.

I initially wrote a simple HTML5 site that would calculate Centiles: [centile.org](http://www.centile.org/)

An NHS Hack Day friend, Chris Casey, developed some Centile calculation code that runs on Node.js via EWD.js, and wrapped this into an API, which is currently not deployed.

In 2015, a group of young people at the Young Rewired State Festival of Code 2015 used my licence for the UK90 LMS data tables, and developed the idea even further, to create Clinical Calculator - a more comprehensive API for calculating a range of different parameters that are used by health professionals in the care of patients, including child growth charts:

<http://api.clinicalcalculator.org>

Note that this API link does not work in a normal browser, I would recommend using an API runner such as [Postman](https://www.getpostman.com/) to interact with the API.

Some example requests:

`GET http://api.clinicalcalculator.org/obesity_by_postcode?postcode_search=wn72nx`

`GET http://api.clinicalcalculator.org/centile?weight_in_kg=29&height_in_m=1.20&year_of_birth=2006&month_of_birth=11&day_of_birth=10&sex=M`
