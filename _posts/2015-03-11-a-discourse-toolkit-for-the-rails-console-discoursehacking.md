---
title: 'A Discourse Toolkit for the Rails Console #discoursehacking'
author: pacharanero
layout: post
permalink: /2015/03/11/a-discourse-toolkit-for-the-rails-console-discoursehacking/
categories:
  - Uncategorized
---
I&#8217;ve been working for Digital Health Networks (e-Health Media) for the past few months, migrating them from a Google Group which lacked some of the nicer social features we have become used to, to a new shiny <a title="http://www.discourse.org/" href="http://www.discourse.org/" target="_blank">Discourse</a> forum.

<a title="http://www.discourse.org/" href="http://www.discourse.org/" target="_blank">Discourse</a> is a modern flat forum with some lovely features, a responsive and speedy UI (using the <a title="http://emberjs.com/" href="http://emberjs.com/" target="_blank">Ember.js</a> client-side app framework) and a back-end based on <a title="http://rubyonrails.org/" href="http://rubyonrails.org/" target="_blank">Ruby on Rails</a>, a mature web framework and the so-called &#8216;killer app&#8217; of the <a title="https://www.ruby-lang.org/en/" href="https://www.ruby-lang.org/en/" target="_blank">Ruby</a> language.

Even with Discourse&#8217;s awesome functionality and almost daily updates of the software containing new tweaks and features, I did find a few things I needed to do in Discourse for which there is no admin UI. I worked out some ways to do these using the Rails console, so I thought I&#8217;d put them up here for others to see and use (and add to!)

I also put most of them on <a title="https://meta.discourse.org/" href="https://meta.discourse.org/" target="_blank">Discourse Meta</a> because that&#8217;s the main place to go for Discourse info.

They are all tested on a standard Discourse Docker installation running latest updates and cloudin&#8217; it on a Digital Ocean Ubuntu 14.04 LTS box.

&nbsp;

# #1

#### make a group of users get email notifications for every post on a Category

When starting a new forum (or in my case, migrating to a new platform), users do need to be encouraged to participate and visit the site using email notifications. We found that in the early few weeks following migration, traffic on the site dropped to almost nothing. We realised that this is because the default setting in Discourse is for users to get notifications only if they are @mentioned or have participated in a topic &#8211; fine for a large established site especially if lots of unrelated groups are on there, but it was killing our site.

Here is the menu where an individual user can set their Notification status. Unfortunately at the time of writing, there is no way to change the default, and no admin over-ride.

[<img class="alignnone size-large wp-image-424" src="http://www.bawmedical.co.uk/wp-content/uploads/2015/03/Selection_025-1024x296.png" alt="Selection_025" width="620" height="179" />][1]

You can get to the Rails console in Discourse by using the following commands:

<pre>ssh root@your-discourse-server 
cd /var/discourse
./launcher ssh app
rails c</pre>

You need to find out the `category_id` of your Category that you want users to Watch:

<pre>pry(main)&gt; Category.where(name: "Health CIO Network").first.id
=&gt; <strong>6</strong>
Then find the group id of the Group that you want to set the watching status of:
pry(main)&gt; Group.where(name: "Health_CIO_members").first.id
=&gt; <strong>43</strong></pre>

Then set the user watching status like this:

<pre># initialise an empty array for the users in the group
pry(main)&gt; userlist = []

# get array of user ids who are in that group
pry(main)&gt; GroupUser.where(group_id: <strong>43</strong>).each { |u| userlist &lt;&lt; u.user_id }

#check the array of user ids looks sensible       
pry(main)&gt; userlist
=&gt; [1, 3, 6, 78, 112]

# set the group's users to Watching (represented in Discourse by integer 3) the category_id 6
pry(main)&gt; userlist.each { |u| usr = User.find(u) ; CategoryUser.set_notification_level_for_category( usr, 3, 6); usr.save! }  

# check the bulk Watching assignment worked       
pry(main)&gt;  CategoryUser.where (category_id: 6, notification_level: 3)</pre>

It&#8217;s worth noting that the only reason I was able to work out how to do this is because I was able to look at Discourse&#8217;s data model in their <a title="https://github.com/discourse/discourse/tree/master/app/models" href="https://github.com/discourse/discourse/tree/master/app/models" target="_blank">source code on github</a> &#8211; just another reason why <a title="https://github.com/discourse/discourse/tree/master/app/models" href="https://github.com/discourse/discourse/tree/master/app/models" target="_blank">Open Source Is The Only Way!</a>

### 

# #2

### prevent Discourse from suppressing Daily Digests for users that have been seen recently

Discourse&#8217;s default behaviour is to suppress the Daily Email Digest if the user has been seen on the actual Discourse forum recently. This can be turned off per-user but unfortunately there&#8217;s no Admin UI for doing it globally. We felt that even though our users had been to the Discourse forum recently didn&#8217;t mean they&#8217;d seen *everything* that&#8217;s of interest.

You can switch off this suppression behaviour by getting a Rails console on your server (see #1 for instructions), and then this line:

<pre>pry(main)&gt; User.all.each { |u| u.email_always = true; u.save }</pre>

This will of course affect all users, but they will still have the option to reinstate the Daily Digest suppression in their preferences if they want.

# #3

### reassign posts to a different user

Do this in the Discourse UI &#8211; it&#8217;s easier. I didn&#8217;t realise there was an Admin only UI feature for this.

[<img class="alignnone size-large wp-image-446" src="http://www.bawmedical.co.uk/wp-content/uploads/2015/03/Selection_0281-1024x638.png" alt="Selection_028" width="620" height="386" />][2]

<del>If you want to reassign posts from User A to User B this is not currently possible via the Discourse Admin UI (or if it is, I haven&#8217;t found it yet! <img src="http://www.bawmedical.co.uk/wp-includes/images/smilies/simple-smile.png" alt=":-)" class="wp-smiley" style="height: 1em; max-height: 1em;" /> ). So we do it in Rails &#8211; follow the instructions in #1 to start the rails console if you haven&#8217;t already &#8211; then:</del>

<pre><del># find out a User's ID number from their name
pry(main)&gt;  User.where(username: "pacharanero").first.id
=&gt; 23</del></pre>

<pre><del># this would transfer all of User 23's posts to User 75
Post.where(user: 23).each { |post| post.user_id = 75; post.save }</del></pre>

 [1]: http://www.bawmedical.co.uk/wp-content/uploads/2015/03/Selection_025.png
 [2]: http://www.bawmedical.co.uk/wp-content/uploads/2015/03/Selection_0281.png