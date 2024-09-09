---
title: "Work Musings"
description: ""
pubDate: "Aug 29 2024"
heroImage: "/Gordon_HL1_promo.webp"
tags: ["professional", "opinions"]
---



Well, I've had a little time to settle into my new position, and I think I'm starting to hit my stride, so I'll jot down some quick thoughts while they're still fresh. 

# AWS

It's been interesting working with AWS more directly. For the past 3 years of my career, I've been focused almost entirely on app code, not worrying about how things are hosted or updated -- we've had a great DevEx team that provided solutions to handle all the K8s orchestration of the services that I was working on. Now I'm back to having to think about how and where things are set up in AWS. 

### What does a server look like?

When I was at Talent, we had a couple of PHP monolith-type services, a couple of Go services, and a dozen or so lambdas for cron-type jobs. At the time, I remember thinking "huh, that's interesting -- lambas are super cheap. I wonder if you could build an HTTP server off of them."

As it turns out, you can! Is it a good idea? Maybe.

With a traditional containerized service, you write some code, chuck it into a container, and then (if you're fancy) configure some way to determine at execution time if you need more containers of your service spun up to respond to increased traffic. Similarly, you can kill containers to save money if you're in a lull.

With a lambda, you're only paying for the execution of a given function. So a "route" for an HTTP server could instead look like this:
![cool](/public/API-to-Lambda.svg)

Compared to EC2 instances, this is pretty cheap. And it scales without you having to think about it.
 

Sounds great, but in my next few posts, I'll talk about some of the complications I've encountered working on an architecture like this.