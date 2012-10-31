---
layout: post
title: "The Case Against Password Auth"
date: 2012-10-31 00:06
comments: true
categories: [security, opinion]
---

## Introduction

Passwords are ubiquitous. We have passwords for everything: email, phones, cars, mobile apps, ATMs, bank-accounts, ecommerce sites, alarm systems, picking up our kids, even for sex (say "pickles" if this hurts too much). 

As we move to an ever more connected, seemless service world, we are inundated with more and more passwords. With all the passwords we have to deal with on daily basis, we're defacto behaving in an insecure manner, just to ease the burden that password based security has placed on us.

If you need to protect a section of service, passwords are quickly becoming a bad alternative.

Developers should think twice before implementing a password base system, as it's time consuming and very easy to screw up.

### Axiom 1: People reuse passwords because it's easy.

As Bruce Schneier wrote in [The Psychology of Security](http://www.schneier.com/essay-155.html), security is a trade off. It's a trade-off between being secure and {Money, Time, Freedom} and so forth. With the explosions of passwords, people's natural tendancy is to reuse the same password across multiple sites. It's hard to remember a unique password for each site, and much easier to have one password. So we use the same passwords all over. Some people are move savvy and have a set of passwords, while others prefer to use a code to come up with a unique password. By and large however, people reuse passwords.

The reuse of passwords causes a downstream issue. A security breach of your password data not only means that attackers have access to your user's data on your site, but could compromise their data on other more valuable sites.

### Axiom 2: Designing a "Secure Enough" system is hard

Since there is no real such thing as an absolute secure system, building one that is good enough will have to suffice. Of course, "good enough" is subjective. A bank account has a different set of requirements than securing access to a web forum for Cross-fit Enthusiasts. However, with people reusing passwords over and over again, the minimum bar for a secure-enough system has been raised, such that it's very difficult to do properly.

* Cryptographically secure hashing algorithms.
* Key Strengthening
* SSL
* Salting Hashs with Cryptographically Random Data
* Password Complexity
* Account Lockout
* Proper Hash Storage

These are just some of the parts required to properly secure a password.

#### Getting it mostly wrong

[passportjs](http://passportjs.org/guide/username-password.html) was passed to me as a potential toolkit for our password needs. We're built ontop of nodejs, and at the time of this post, there aren't any plug-in-play end to end auth systems. This was suggested as a potential off-the-shelf solution that would save time. I took a look at the guide and had to dismiss it. It's not my intention to knock this toolkit, but one look at the Username/Password guide and it raised serious doubts about how well this was implemented.

### Axiom 3: Attacks always get better

Attackers are smart. They're smarter than me, and they're definitely smarter than you. Staying ahead of them is hard. Smart companies like Sony, Valve, LinkedIn, have all been victims of sophisticated attacks that have left user data exposed in one way or another. With the attackers learning and iterating, brings the problem that the minimum-bar in Axiom-2 is always being raised. Hash algorithms are broken; computing power becomes better/faster/stronger/cheaper; vulnerabilities in software are found. 

How likely are you going to go back and revisit your security system? 
What if you found out about a serious attack on a site that you could be vunerable to?
How often do you pay attention to attacks?

### A problem waiting to happen

By opting to store user passwords, you're essentially signing up to guard what could be very valuable information. Users may have inadvertantly given you the keys to their kingdom, access to which could have [dire consequences](http://www.emptyage.com/post/28679875595/yes-i-was-hacked-hard).

So you have to get it right. *The first time*

But you won't. 

Because it's hard, and you're not that good.

### Challenge this!

You can attempt to protect the users from themselves: force a highly obtuse password complexity policy that pretty much guarentees a unique password.

But they'll probably forget it, and have to use the password reset feature.

Which may use a challenge response question (What highschool did you attend?).

But did you remember securely hash the answer to the challenge?

Kudos.

What about the question itself? 

Fuckbeans.

If you're not careful, your challenge system will become a proxy for your password system, and will likely be easier to get around.

#### All too easy

When I first started at my last company, I required access to our customer demo system to make some changes. While I was waiting for someone to approve my account, I snooped around the User table database looking for creds, so I could start working (Winners want the ball in their hands). Of course the passwords were hashed, as were the answers for the challenge question. However the question themselves were not, and taking a look through them, I was suprised at the number of questions that read "The name of the company you work for." One look at one persons registered email, and I was in, and able to make changes to the customer demo portal.


