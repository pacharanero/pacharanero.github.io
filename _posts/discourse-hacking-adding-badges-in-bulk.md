---
title: '#discoursehacking &#8211; adding Badges to Users, in bulk, in Discourse'
author: pacharanero
layout: page
---
<pre>emails = [array containing all the email addresses of attendees]

# initialize blank array for User objects
userlist = [] 

# pulls only Users where the email matches the one they used for SS registration without causing errors
emails.each { |e| userlist &lt;&lt; User.try(:where, email: e) } # the use of try avoids errors when no match is found

userlist.reject!(:&empty) # get rid of any non-matches which are an empty entry in the array
userlist.flatten! # flatten the array by one level

# BadgeGranter requires the Badge object and the User object to be passed in as parameters
# In our case we were assigning the Badge with the id number 108
userlist.each {|u| BadgeGranter.grant ( Badge.find(108), u ) }

</pre>

Done!