---
layout: post
title: threading
---

Down to the last home stretch of my masters and then I'm done. Today's standup was about pipelining and I'm pretty
done now.

Implemented multithreading an item I built that dumps output to a shared queue. At the time I thought the queue could
be a single db connection to write to a single table, but after talking to the db admin, who said it was possible to
utilize multiple connections even on the same table without locking issues, started looking at the sqlalchemy pool set 
up again to see if this indeed the case. I had trouble with the sqlalchemy pool previously, but perhaps this will
not be the case this time around.

Also learned to use suppress from the contextlib. Not sure I'm a big fan of this in most scenarios, but contextlib 
itself is very handy.