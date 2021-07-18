---
layout: post
title: aws lambda
---

Spent more time than I would have liked setting up a kinda sorta simple scrape and upload job
on aws lambda. Setting up the lambda itself was pretty straightforward (ish...), and it took a little
bit longer to understand layers, but still relatively straightforward, but then actually setting a 
real script up to some standard cronjob (aka cloudwatch event) took a few hours. 

The wonderful things I ran into:
- Cloudwatch cronjob events require a slightly special set up for day of month/day of week values
if you use them ("_One of the day-of-month or day-of-week values must be a question mark (?)._")
- Turns out aws lambda layers have a hard limit of 250 MB unzipped and this is very disconcerting 
  to work around. After a bit of fiddling, managed to get a yfinance + pandas + numpy + pymysql + 
  sqlalchemy set up going without burning through the 250 limits (use aws' layer for numpy, 
  <a href="https://github.com/keithrozario/Klayers">klayers amazing layers repo</a> for pandas, 
  and then do the yfinance layer on your own with no dependencies and then add in the requests + 
  multitasking packages to round out yfinance, and then added pymysql and sqlalchemy on top of that - 
  I used my raspberry pi to build the folder setup and zipping). The reason I didn't do numpy
  and pandas on my own for this was that I ran into rather peculiar issues when I tried to install
  a zip file with those installed as part of a custom layer - ran into numpy and pandas 
  c extension missing errors, so ended up using external layers to attach them. If you blow past
  this 250 limit (some packages are _gigantic_) then you are forced to set up a layer to call a 
  S3 bucket externally but I really didn't want to do that. In any case, this makes aws lambda
  not entirely the _easiest_ go to substitution out of the box for your random scripts...
  
Other things I have learned, somewhat superficially, but perhaps will pick up more traction later:
- redis key value store
- the ibapi app, which is some level of the same kind of stupid as the blpapi app
- cloudwatch events
- writing some more performant db functions, made one switch so far and am pleased with the result