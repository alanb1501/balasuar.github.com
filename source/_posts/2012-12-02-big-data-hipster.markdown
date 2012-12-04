---
layout: post
title: "Big Data Hipster"
date: 2012-12-02 23:56
comments: true
categories: rant, buzzwords, bigdata 
---
*Note: I know that [gizmodo][giz] just ran an article about BigData, however that was purely coincidence. I'll assume most of you read it, and won't bother repeating most of what was covered on it.*

These days suits (def: suit. [n] pejorative term for people who don't add real value) are all clamoring about BigData. I tend to dislike techbuzz words, and I *REALLY* despise folks who've never actually delt in the space, giving advice or giving opinions:

> "Oh, you really should learn Ruby on Rails. It's very good stack." 

> "Have you built anything via Ruby on Rails?"

> "..."

As an aside, Ruby on Rails is a fine technology, but it's not the *only* technology that does what it does. Choosing a stack based on the recommendation from someone who has no direct experience working with it, makes as much sense as calling a random payphone in New Guinea and asking for a dental referral.

I digress.

Since the suits are all talking about BigData, everyone is trying to jump on the BigData bandwagon, to earn some sort of points. 

* "Mobile?" [x] 
* "Social Media?" [x]
* "Responsive Design?" [x]
* "BigData?" [x] 

Congratulations: 4 for 4. You have a 100m company! 

BigData is really two parts:

1. Storing and processing large quantities of data, too large for standard scale computing
1. Using that data to find information that wouldn't otherwise be available

#### *So you generate a lot of data? Who cares. What the fuck are you doing with it?*

[Super Crunchers][crunch] got me pretty excited about finding patterns and meaning behind data. Data driven analytics is whats *really* hot, not generating a lot of data. Any asshole can fire up hadoop, or map reduce and churn through a butt load of Apache Webserver Logs (okay actually that's not true. There are many dipshits devops guys who can't do that). What's far more interesting: learning from that data, and extracting valuable insight. Pandora (aka the Music Genome Project) is a great example of this. They churned through a lot of user experimental data to create a learning algorithm to predict music tastes based on a variety of factors. Amazon.com has done this as well to an amazing degree. Google's ab testing for ad unites is another use of large scale data crunching.

But you're still stuck trying to process TB of data using rack mounted window's machines? Okay chief. That's not BigData. It was in 2004, but not anymore. If you don't require cloud infrastructure to get through your data, it's not big. it's just unweildy.

Even still, processing a large load of data isn't anything new. Back in 2004, we was crunching through GB's of historical stock record data, feeding that data into a scalable processing math engine developed by a ninja team of PhD's. The idea was to find a signal to use to make predictions in highspeed stock market trading. We didn't have hadoop, or AWS, and the Cloud was something that hung over Seattle constantly. We built our own scalable processing network infrastructure to churn through all that data, and invested in a ton of ubercheap, but ultra powerful off-the shelf dell pc's to farm through the data. We had so many machines that we had to have the office rewired to handle it. We had a specific sequence to power on machines, to prevent from overwhelming the circuit loops.

Now though, there are ginourmously large data-centers the size of small town, that house hundreds of thousands of machines, that each run virtual machines on them. That's the scale of BigData. 

So now when people try and talk to me about BigData, I just pop open a PBR, and tell them "I was in big data, before it was cool to be in BigData."


[giz]: http://gizmodo.com/5964737/what-is-big-data "Gizmodo"
[crunch]: http://www.amazon.com/Super-Crunchers-Thinking-Numbers-Smart/dp/0553384732 "Super Crunchers"

