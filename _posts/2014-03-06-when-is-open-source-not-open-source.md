---
title: When is Open Source not Open Source?
author: pacharanero
layout: post
permalink: /2014/03/06/when-is-open-source-not-open-source/
categories:
  - Uncategorized
---
I had an interesting conversation at the NHS England Healthcare Innovation Expo on Monday and Tuesday of this week (3-4th March 2014) with a pathologist Fred Mayall who has done some excellent work enabling clinicians to develop small databases within their own trusts.

Excellently, the Intellectual Property of the work is released under the GNU Affero GPL V3, an OSI approved open source license, meaning the IP can be freely shared and reused. 

One problem: the project has a single major dependency on the proprietary and closed source FileMaker Pro package. The IP of the project is only really available as a binary blob in FileMaker Pro format. You can&#8217;t see anything inside it without FMP. Meaning there IS no way to reuse this code or IP in any other way except:

a) use FileMaker Pro free for 30 days &#8211; (not really what I would call a sustainable solution)

b) Buy FileMaker Pro license(s) &#8211; (not really in the spirit of Free and Open Source computing)

c) use your 30-day FileMaker Pro free trial to reverse engineer the intellectual property out of this project and into a genuinely interoperable and open source form, without the FMP dependency and separating the IP out into manageable pieces where the source is in some way viewable.

Hands up if you think that&#8217;s what&#8217;s meant by Open Source&#8230;&#8230;&#8230;..anyone?&#8230;&#8230;&#8230;..no, me neither.

Myself and a couple of other people had an attempt at persuading Fred that there was a real need to free the IP from its dependency on FMP, perhaps by finding some &#8220;platform agnostic&#8221; way of representing the object model and/or decision support tree that the clinicians are writing in FMP, and thereby allowing the same IP to be used in a variety of other database engines, possibly including FileMaker Pro for those trusts already with licenses.

Fred&#8217;s principal counter-arguments (to the need for replatforming or for having an abstraction layer above FMP) were:

1) &#8220;lots of trusts already have FMP licenses therefore they can just use FMP at those trusts.&#8221; My rebuttal: They may have licenses for existing deployments in other parts of the hospital like HR, payroll etc. Extending the use of FMP to another area of the trust may still require further purchases of licenses by the Trust and is therefore not just a free addition.

2) &#8220;clinicians only take 4 weeks to be shown how to create their own databases in FMP, and they won&#8217;t learn to code&#8221;. My rebuttal: (and the view of others present) There are open source database engines which you can teach clinicians in less time than 4 weeks. I learned the basics of Ruby on Rails in 2 days. There is also now a GUI frontend for designing Rails object models (Rails Conductor). Thinking you have empowered a clinician by teaching them FileMaker Pro is like teaching a starving man how to phone for a takeaway &#8211; it creates further dependency, not freedom.

3) &#8220;I don&#8217;t forsee anything changing in the NHS for a while and therefore see no reason to prepare or be aware of the need for change.&#8221; Ermm&#8230;.. I might have to disagree with you there&#8230; <img src="http://www.bawmedical.co.uk/wp-includes/images/smilies/simple-smile.png" alt=":-)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

Find out more about Fred&#8217;s Project FreeDP <a href="http://freedp.org/" target="_blank">here</a>