---
layout: post
title: poetry
---

hate poetry. should be simple and then you try to use ssl certs with it 
and it does all sorts of weird things. it explicitly relies on pip but
not the pip.conf, so you can't trusted-host random stuff - although
i learned how to add trusted hosts so i can pip install stuff without
thinking too hard so there's that - and then when you are actually
reasonably sure you are using a legitimate certificate then the 
config settings don't appear to respect it. idk. as this was an issue
explicit to the poetry set up and not particularly anything else in 
the system, i just wget the gz files from the alternate repo and then
appended them to the install with a local path. /shrug

turns out aws cloudwatch is the only place where they use the 6 digit
thing going. if you ever needed to know this. 