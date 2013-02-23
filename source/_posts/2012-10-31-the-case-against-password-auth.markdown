---
layout: post
title: "The Case Against Password Auth"
date: 2012-10-31 00:06
comments: true
categories: [security, opinion]
---

### tl;dr

Password auth is hard and you're going to screw it up. Don't put your users at risk, and instead let someone who has better resources at their disposal handle password security.

## Introduction

Passwords are ubiquitous. We have passwords for everything: email, phones, cars, mobile apps, ATMs, bank-accounts, ecommerce sites, alarm systems, picking up our kids, even for sex (say "pickles" if this hurts too much). 

As we move to an ever more connected, seemless service world, we are inundated with more and more passwords. With all the passwords we have to deal with on daily basis, we're defacto behaving in an insecure manner, just to ease the burden that password based security has placed on us.

If you need to protect a section of service, passwords are quickly becoming a bad alternative.

Developers should think twice before implementing a password base system, as it's time consuming and very easy to screw up.

<!-- more -->

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

### An Almost Perfect Solution

If you're inclined to believe any of what I've written, password auth systems aren't worth their time. A user's password has now more valuable that the stuff we're likely protecting it with. We could generate a password that is guarenteed to be unique, but they'll forget and rely on the "Forgotten Password" mechanism to login.

[Editors note: As I was writing this, I had to use the forgotten password system to get access to my Disquss account. How the fuck would I remember a password I use every 6+ months?]

As I mentioned earlier, this Forgotten Password mechnasim is essentially a proxy for password auth. You click a link saying you forgot your password, you're emailed a new link that takes you to a site, where you create a new password, and then you're let in to do your business.

So why even have the password in the first place?

This is the core concept behind OpenID. Instead of supporting passwords, I'll defer my authentication to a well-trusted provider like Google. Google will provide us with identity information, and handle the authentication, and mangement of secure data.

Google Engineers (whom I consider to be the cream of the crop of corporate-slave engineers) are smart. Google has the resources to build the proper comprehensive layered system that we need. Let's let them manage auth for us.

But the idea of letting Google manage our user identities, doesn't sitwell with the bosses. "Not everyone has a Google account."

### Bringing Balance to the Force

Instead of deferring identity management to OpenID providers, I propose a solution that instead defers authentication to your users email provider. It's the Forgotten Password Scenario, without actually having passwords to forget.

It works like this:

1. Alice visits Bob.com
1. Alice decides to create an account.
1. Alice enters her email address.
1. An email is sent to Alice's address containing a link. (Note: This is usually done anyway to validate that Alice does actually own the email submitted ) 
1. Alice Clicks the Link, which takes Alice to the secure portion of Bob.com
1. Bob.com stores an auth cookie on Alice's computer, that expires in 30 days.
1. Anytime Alice visit's Bob.com, Alice is allowed to access the secure portion of Bob.com 

### A rose by any other name

The way forgotten passwords scenario typically works is essentially generating a "one time passsword." If you've done online banking, you've no doubt come across a OTP. The bank will usually send you a text message with a short code that you enter that gives you access to your account. This is called 2nd Factor Auth; it's part of the concept of layering security. The three factors most commonly employed are: Something you know (password), Something you have (a cell phone), and Something You are (Biometrics). The more you add, the harder it is to fake an identity.

So the link is a one-time password. You click the link, and you're allowed into the site. The password entry mechanism is transparent to users (it's part of the URL), but the password is only good for one use, and usually will expire after a set time.

With the forgotten password scenario, we have close to 2-factor auth: Something you know (your email password), and something you have (an email account). It's not quite 2-factor, as proper 2-factor requires two distinct systems (your brain, and a physical token generator for example).

### Examples in the Wild

We've seen this approach used now when it comes to authenticating devices. If you enable Netflix streaming on your XBox, you're given a short-code to enter, instead of entering your email and password--a cumbersome process when using a gamecontroller.

When you don't have an easy way to enter in text, it's much easier to use a short-code to auth devices.

This was also solution I proposed at my previous company. Instead of using a username and password, instead authorize the device with a one-time password. The idea was sound, but the execution was terrible (Math.Random to generate a security token...the horror, the horror.)

Windows8 now allows login via a 4 digit pin, even with access to a keyboard, because typing in a password that is long and secure will make users less likely to use passwords in the first place.

### Even roses have a thorns

This solution is pretty straight forward, but it's not perfect (no secure system is.)

#### Extra Work for the User
It requires the user to login to their email account to retrieve the access code (or access link). For many of us, we have our emails open constantly, and it's no big deal, but it is an extra step that doesn't exist with password auth.

#### Kiosk Mode
Storing a cookie for 30-days isn't a good idea for people who are accessing thier accounts from a non-secure computer.

You could prompt the user to remember the login for 30-days (this is usually done via a checkbox at the login screen), but that is more work to support.

#### Unfamiliar Workflow
For many users, this workflow is unfamiliar, and thus causes Suits to worry about it's impact.

#### The email is the weakest link in the chain
If it was already, this approach puts the responsibility of security on the email provider. Granted, that's been the case thus far--anyone who can log into my personal email account could potentially wreak untold havok: order a ton of stuff from amazon, take down my companies entire infrastructure, remotely wipe my ipad, iphone, and laptop, and of course, access my facebook account, and worst of all, send dick-photos to my contacts.

### 
Despite the downsides mentioned above, getting rid of passwords is a better solution. You no longer are liable for storing super valuable information, and the complexity of your security system is reduced drastically, with *NO* reduction in security at all. Moving forward, companies should take a hard look at using deferred authorization schemes such as OpenID, but if they can't handle the deferred ownership of user information, consider a One-Time Password based security system using email addresses.

In the long run, your users will benefit, and you won't be adding to the problem.