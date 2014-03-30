---
title: Consolidating personal network services with Dokku and Docker
---

I run a number of network services for our household. These include VPN servers, handlers for web services like Twilio, and a couple of websites. Most of these aren't actually very interesting, but they need to work without a lot of fuss and without a huge investment of capital. File serving happens inside the house, but I found that I needed a number of independent services running outside in order to avoid network anarchy.

Enter [Heroku](https://www.heroku.com/), a stable, managed platform designed to simplify deployment of web services and sites. Heroku is a PaaS (Platform as a Service) designed originally for Ruby apps but supporting a variety of languages and frameworks. Their way of doing things is attractive for a number of reasons:

- Each independent site/app is isolated in its own environment, with its own resources and dependencies.
- Deployment is set up in a structured and modular way, using [Git](http://git-scm.com/). Push your content to their site, and it's live, with recursive dependency fetching.
- It's straightforward to add cloud-sourced backend services like databases, caching layers, analytics, etc. There's a whole ecosystem, and billing is centralized.
- There's a very capable free tier that lets you host small projects with no investment (and the same applies for most of the standard add-on services).

The problem with Heroku – if it can be called a problem – is that it's overkill for most personal projects. This makes a lot of sense if you're running a company off of it; however, their pricing is a harder proposition if the consequence of downtime is mild inconvenience. Like, $34.50/mo (USD) for the initial paid tier, as of March 2014. Speaking personally, that's well above my [latte threshold](/glossary), though you definitely get rock-solid performance for the money.

On a personal note, I have limited discretionary funds before I have to start justifying such critical tasks as: backing up data three times, running carrier grade VoIP services for our house, insisting on UPS battery backups, making lighting computer controllable, runnning gigabit *everywhere*, etc.

## That'll do, Pig; that'll do

Let's introduce things recursively:
[Dokku](https://github.com/progrium/dokku) is a minimal open-source re-implementation of the Heroku Procfile-based PaaS infrastructure ("the smallest PaaS implementation you've ever seen"), which runs on 
[Docker](https://www.docker.io/), itself a set of services designed to make [LXC Containers](https://linuxcontainers.org/) usable. Docker is billed as "an open source project to pack, ship and run any application as a lightweight container". Docker is useful because it simplifies deployment of lightweight containers that encapsulate the dependencies and functionality of a whole application stack. Dokku makes it straightforward to depoloy things in a Heroku-esque environment running on your own hardware.

So, 
