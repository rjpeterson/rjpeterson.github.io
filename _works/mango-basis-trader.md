---
title: Mango Basis Trader
description: An arbitrage bot that finds and executes basis trades on Mango Markets derivatives trading platform
category: Finance
date: 2022-07-01 08:01:35 +0300
client: Mango Markets
role: Lead Developer
image: '/images/basistrader-1.jpg'
# image_caption: 'Photo by [Freepik](https://www.freepik.com/)'
---

On the Mango Markets derivatives trading platform, perpetual future contract funding rates occasionally reached extremely high levels. This created an undesireable trading environment for retail traders. The best way to curtail this type of situationis to make it easy for any user to arbitrage funding rates (aka "basis trade") on the platform.
With this goal in mind, I developed an open source bot to find and execute these funding arbitrage trades. With many people arbitraging funding rates, funding rates will be reduced and the result is a better trading environment.
Making use of Docker-Compose, I built a Typescript bot that could be downloaded and run by anyone with only a handful of simple setup steps.

### Tools Used:
* Docker
* Typescript
* Rest API
* Websockets

### Skills Developed:
* Async Error Handling
* IDE Debugging
* Code Readability & Organization
* Creating & Publishing Docker Containers

[Github Repo](https://github.com/rjpeterson/mango-basis-trader)
