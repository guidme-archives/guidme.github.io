---
layout: post
title:  "API management"
date:   "2021-07-01"
author: "Jeremy Pichon"
image:  "/assets/2021-07-01-api-management/preview.svg"
---

<div class="center">
  <img src="/assets/2021-07-01-api-management/preview.svg"
    style="height: 250px; object-fit: contain;"
    alt="Banner of the post"
  />
</div>

#### Welcome visitor,

An API gateway is a management tool that will receive requests from your clients and send them to your services.

It might sounds stupid said like this, but most companies APIs are deployed behind API gateways.

It’s common for API gateways to handle tasks that are used across a system of API services.
Such as user authentication, rate limiting, and statistics.

### How we implemented it

We are using [Kong Gateway](https://konghq.com/kong/) at Guid'me. It is a quite popular service for API management and has both cloud and self-served offers.

As they provide a Docker image, it was really easy for us to start working with it.
Their documentation is well written and you should not have difficulties to set it up.

It solved a big issue we had on our API which is having a lot of non core business logic.
Basically with Kong we could remove all the following from our code and depend on Kong to handle it:

- Monitoring (request duration, status code, ...) 
Coupled with a visualization tool, we could identify efficiently which routes are the slowest or which ones are failing and how often.

We can also associate calls per consumers (Application) which helps us to identify which platform is the most used.

- App Authentication (consumers)
Before Kong, we were only relying on user tokens authentication, which was enough at the time.

But we recently opened our catalog to be visible without requiring an account.
And whithout an App Authentication system that would mean that our API could be sniffed by anyone.

- Bot protections
To be honest, this is probably the most useful plugin we installed.
We were receiving tons of attack attempts on our APIs. And this  prevented our monitoring tools to be flooded.
Besides to App Authentication that will prevent non authenticated calls to simply fails).

Of course this is not the only way we protect our systems, but not being spammed was actually appreciated.

- Rate limiting
It is quite self explanatory: To limit requests amount based on custom rules (e.g.: device IP).
It is an additional layer to protect our APIs from abusers.

- Request transformer (keep our non public APIs protected)
Even though our APIs are not accessible from the outside world, we protect them with some authentication.
This allow us to do it easily and in transparency for our clients (mobile apps).


In addition to all the mentioned features, Kong has a [plugin hub](https://docs.konghq.com/hub/) to solve most common requirements.
And if you do not find what you need there, you can develop your own plugins.


---

All of this Keeps your API focused on your business requirements. We could reduce our code base by removing a lot of code doing basically the same thing. It also reduces the maintenance time of those features as it is handled by the plugin developers themselves.

<br /><br />

**Thank you for reading**  
