---
title: 'child health centiles&#8230; doing them in code part 1'
author: pacharanero
layout: post
categories:
  - Uncategorized
---
## What is a centile? (because not *all* techies are `/^math|maths/` geeks)

A centile is a way of demonstrating where a particular measurement lies within a distribution of data. A good way to express it in a way that makes sense is if a measurement is at the 20th centile, then it is higher than 20% of the population&#8217;s measurement. (and, therefore, lower than 80%). So, to pick random examples, a low measurement might be at something like the 5th centile, a high measurement could be the 97th. In the very centre of the distribution and at the very middle value, is the **Median**, which is mathematically identical to the 50th centile.

## How are the centiles calculated?

For each sex and age point (in months), there is a normal distribution of weight and height. The characteristics of this normal distribution are described in terms of the parameters L, M and S &#8211; these stand for median (M), the generalized coefficient of variation (S), and the power in the Box-Cox transformation (L). The equation for calculating a centile from a measurement (eg height or weight) and the L, M and S characteristics is:

**Step 1** &#8211; calculate z-score (degree of deviation from the mean of a measurement in units of 1 SD)

           ((X/M)**L) - 1
    Z = -------------------- (assumes L≠0, which it is for our dataset)
           LS


(source: http://www.cdc.gov/growthcharts/percentile\_data\_files.htm)

**Step 2** &#8211; convert z-score into a percentile

This is done via a mathematical &#8216;lookup table&#8217; of a typical normal distribution. In the programming languages I have looked at, and on Wolfram|Alpha the lookup is described as the Cumulative Distribution Function CDF.

In Python (yuk &#8211; but nobody else wanted to use Ruby), these two steps boil down to:

`centile = scipy.stats.norm.cdf( ( ((measurement/M)**L)-1.0) / (L*S) )`

We also ported the code into JavaScript in order to use a node.js back end.We used the good but under-documented JStat library for the statistics work.

## Going Backwards

In order to provide context for the centile number produced, we also wrote a bit of code that generates *measurements* from a range of centiles. For example, if you have a child that is on the 25th centile for height, it&#8217;s sometimes helpful to know what the heights are for various points on the normal distribution. Sometimes there is only a few centimetres difference between the 3rd centile and the 97th. So we used the inverse function to the centile calculation function to go backwards and work out a range of measurements from the centiles.  
This was straightforward in Python, but for the JavaScript version it was a bit more tricky, mainly because the JStat library is so poorly documented it was hard to find the right functions.

## What is the MRC License all about?

The Medical Research Council own the copyright on the &#8216;LMS Tables&#8217; (statistical numeric charts which enable calculations that render a centile). They have granted us a free licence to use this data to make a free non-profit web app/mobile app. So, while our application code can be open source, the open source licence does not apply to the data tables. These are freely available elsewhere on the Internet, therefore we have not chosen to restrict distribution of them &#8211; but anyone downloading them must seek permission of the MRC to use them in their own deployment. It&#8217;s not hard and they will probably say yes.

It seems silly to me that the MRC haven't made this Open Data. They continue to spend time and money in producing a licence agreement for each and every user of the data. They have told me that they never refuse any request, and there's nothing special in the data or the license that would preclude the release of the data on an Open Data license. But hey, it's only taxpayer money....
