---
title: "Twitch Chat Scraper FAQ"
date: 2016-01-05T14:36:00Z
draft: false
---

Recently, a [side-project](https://github.com/FireEater64/twitch-chat-scraper) I've been working on to scrape Twitch chat logs has been causing quite a lot of confusion, both on Twitch and Twitter. I'll be doing a follow-up post detailing exactly what it is I've been up to, but in this post, I'll attempt to summarise some of the most frequently asked questions, and my responses to them.

## Who are you?
As my [Twitter](https://twitter.com/Fire_Eater64) explains, I'm a final-year Computer Science student at the [University of Manchester](http://www.manchester.ac.uk/).

# Why are you in every channel on Twitch?
As a recent side-project I've been writing a [Twitch chat scraper](https://github.com/FireEater64/twitch-chat-scraper), which connects to multiple Twitch chat channels - and stores any messages it sees in a database, for future analysis.

## Why are you doing this?
Mainly due to exam season boredom. I'm also using this as an opportunity to learn a bit more about the [Go](https://golang.org/) programming language, as well as a personal curiosity about whether Twitch chat really is as mindless as its reputation would have you believe.

## What are you doing with my chat messages?
Currently, nothing. As mentioned above - I'm currently in full-blown exam-panic mode at university, with little time to devote to this project. In the future, I'd like to do some more analysis on the corpus of messages collected, largely inspired by the kind of thing Twitch's [Drew Harry](https://twitter.com/drewwww) [has done recently](https://www.youtube.com/watch?v=1OPqjDcXh5g). Some possible areas of interest include:

- Number of emoticons/second for each channel
- Chat sentiment (happy/sad etc.) during eSports events
- Spectator behaviour (what percentage of chat is spammers, what kind of events inspire people to post in chat etc.)

## Why are you hiding it?
I in no way intend to hide what I'm doing. I've become aware of the fact that what I'm currently doing could definitely be more open. This is mainly due to the fact that I have limited time to work on the project, which is still very much a POC. Hopefully, this post goes some way to address people's (natural) curiosity - in the future I also plan to:

- Create a dedicated Twitch account for the scraper (something more obvious, like ChatCollector)
- Make the bot respond to PMs - with a message directing them to this page.
- Give channel owners an opt-out of data collection (more information below)

## This is evil - please stop
Firstly, I'm sorry you think so. Doing something evil was never my intention. As far as I'm aware - all the data I'm collecting is posted in a public forum, is not against the [Twitch TOS](http://www.twitch.tv/user/legal)[^n], and is really no different to the hundreds of people and organisations [scraping sites like Twitter every day](http://knightlab.northwestern.edu/2014/03/15/a-beginners-guide-to-collecting-twitter-data-and-a-bit-of-web-scraping/). If you disagree with this rationale, stick a comment down below/hit me up on Twitter.

If you do find this data collection intolerable, though, there are a couple of things you can do. Firstly, just ban me from your channel. I don't mind - seriously. In case you hadn't already guessed - I'm much more of a chat spectator/lurker than a participant. Secondly, if banning doesn't work - I'm [working on](https://github.com/FireEater64/twitch-chat-scraper/issues/2) a mechanism to blacklist certain channels if they've indicated they want to opt-out of data collection. This is currently still a manual process - so anyone interested in being added to this list should contact me (either in the comments below, or via [Twitter](https://twitter.com/Fire_Eater64)). At some point, this will be made self-serve - so channel owners can add themselves to the blacklist. For progress on this - see the [GitHub issue](https://github.com/FireEater64/twitch-chat-scraper/issues/2).

## Give me technical details
I'll do a full post at some point over the next week, with the technical details. In the meantime, feel free to check out the code on [GitHub](https://github.com/FireEater64/twitch-chat-scraper).

## Can you remove UniqBot/Some other bot from my channel?
Sadly not. The only username my scraper currently runs under is my own, 'fire_eater64'. There's nothing to stop somebody else from building my project off GitHub, and running it themselves - or writing their own. In the case of bots/scrapers like 'UniqBot' - you'll have to [contact the person responsible for running it](https://twitter.com/UniquePassive/status/695343645898076162) in order to get it removed from your channel/answer any questions you may have.

Hopefully this has helped with some of the questions/concerns people have with what I'm doing. If you have any questions/comments - feel free to stick them down below, and I'll do my best to answer them.

[^n]: If somebody from Twitch wants to/can correct me on this, please reach out to me.