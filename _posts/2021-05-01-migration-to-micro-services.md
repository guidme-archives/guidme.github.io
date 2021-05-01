---
layout: post
title:  "Micro-services's migration"
date:   "2021-05-01"
author: "Jeremy Pichon"
image:  "/assets/2021-05-01-migration-to-micro-services/preview.svg"
---

<div class="center">
  <img src="/assets/2021-05-01-migration-to-micro-services/preview.svg"
    style="height: 250px; object-fit: contain;"
    alt="Banner of the post"
  />
</div>

#### Welcome visitor,

> For context, we started Guid'me as University students. Therefore we were lacking some experience in company (Junior Devs, right?).
>
> At the time we (I, the author) decided to go for PHP with Laravel for the backend.
>
> It was a convenient solution for us at the time as we could do web and API development (which I was responsible for) on the same codebase 


### The backend state

With the conditions mentioned above, you can easily guess what hapened to the product over the years.

It became a complex and monolithic PHP API/web-app that was difficult to maintain. This choice and the release frequency requirements, we cumulated a decent amount of tech debt (c.f.: previous post "[Pay the tech debt]({% post_url 2021-03-04-pay-the-tech-debt %})").

At its peak, I was spending around 50% of my time to fix various issues or trying to find how an old piece of code was working.

As you can guess, this is not an acceptable amount. So I have been thinking about how to solve those issues (non exhaustive list):
* Monolithic API
* No layers in the code architecture (pretty much everything in the controller)
* No Unit Tests
* Poor/Missing code documentation
* API Specs not synchronized with deployed code
* API was handling a lot of non business logic with in-house solutions (error logging, App authentication, ...)


### Our solution: Micro-services

After some investigations, micro-services appeared to be our  solution to solve our issues.

**Cons**

* Initial cost (It is long to start/migrate to micro-services)
The main con for us. We do not have much human time (small team) available.
So I had to explain that this initial cost would be worth way more soon after.

* Have to maintain dependent services contracts
Having multiple services that could interact together is a risk.
It requires extra care when updating contracts in order to not break dependencies.

* Global testing is difficult
Required to solve the previous issue, but represent quite some work by itself.
A solution for this would be:
- Use our containers to run our entire infrastructure before releases
- Run a test that ensure everything works fine altogether


**Pros**

Each services will be independent and have its own responsibility (e.g.: UserAPI, ServicesAPI, BookingAPI, ...).
This scope down quite a lot the size of each service and make it way easier to develop, maintain, and deploy.
Also you limit dependencies per services. An simple example could be that only UserAPI might require an authentication lib. So it will not be in your OtherAPI service.

The codebase being smaller, it is easier to pay the tech debt when you have to.
As services are weakly coupled, we can rewrite an entire service without having to upgrade your entire application.
For example when we want to change for a new framework version or another stack  

It also has a better failure as the potential crash of 1 service would not resolve into your app not working at all.

Also the scalability is easier and cheaper as you will only scale services that needs it rather than your entire application.


**How did it solve our issues**

We still have some legacy (monolithic API) code alive, but We pay the debt little by little by identifying the most urgent components to migrate.

When identified, we revise the specs as necessary as the initial definition might have flaws or the need changed.

Once done we implement the new API as a micro-service with proper layers:
* **Framework**: Contains all framework specific code (controllers, middlewares, ...)
* **Logic**: All our business logic lives here (What makes Guid'me what it is)
* **Data**: Contains models and repository to handle the datasource operations (eg: DB schemas and calls)

And finally, a proper code documentation and tests are added.

<br /><br />

**Thank you for reading**  
