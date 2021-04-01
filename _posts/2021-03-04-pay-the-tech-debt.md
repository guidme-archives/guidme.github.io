---
layout: post
title:  "Pay the Tech Debt"
date:   "2021-03-04"
author: "Jeremy Pichon"
image:  "/assets/2021-03-04-pay-the-tech-debt/preview.svg"
---

<div class="center">
  <img src="/assets/2021-03-04-pay-the-tech-debt/preview.svg"
    style="height: 250px; object-fit: contain;"
    alt="Banner of the post"
  />
</div>

#### Welcome visitor,

<br />
> Technical Debt is the coding you must do tomorrow because you took a shortcut to deliver a feature today. 
To estimate your debt, find tasks you do everyday that are not related to product development.  

They can have various forms as the following: 
* Manual processes (database update, customer email, ...)
* Poorly automated processes and workflows (half automated deployment, ...)
* Legacy code with significant shortcomings (poor logs, low code coverage, ...)   

Technical debt can be of different types. But most experts agree on two different types: Inadvertent and Deliberate. 

**Deliberate**
- It is worth it to deliver the feature in a "quick and dirty" way, even if you have to pay the debt later. It is made consciously and it is planned to be fixed later on.

**Inadvertent** 
- Team is pressured to deliver ASAP and violates best practices to deliver the feature.
- The team is ignorant of best practices, and makes the codebase difficult to manage. This might happens with junior teams or by using a new language/framework.
- It happens, even with great programmers. Programming is a learning journey, right?   

### Why is it a problem

When the size of the debt grows, your team will spend more time to fix it.  
Tech debt causes issues that you want to avoid:
* Stress for devs to deliver features of bad quality
* Devs feels rushed as a lot of time is required to fix the previous bad code
* Bad estimations (accuracy gets less good as the debt increase)
* Code is less maintainable
* Prone to production bugs as UTs are usually skipped when feature is under pressure

Anyway, the appealing shortcuts ends up being a burden for the team as it requires time to maintain/fix. 

Circle of death

```
One problem with technical debt is that the impact can be slow growing and somewhat hidden.
To the question ‘Fix the technical debt, or build new features’ we know how it is usually answered.
As it gets worse, customers complain about slow delivery.
That will increase the pressure to take more short cuts.
Which increases the technical debt.
Which slows the delivery process
Which increases customer dissatisfaction, in a spiraling vicious cycle. 
Unfortunately, many organizations are paying attention, all the solutions are bad ones:
1) Do nothing and it gets worse,
2) Replace or rewrite the software (expensive, high risk, doesn’t address the root cause problem),
3) Systematically invest in incremental improvement
```

### The tech debt at Guid'me

We started as University students. Therefore we were lacking of  experience in company (Junior Devs, right?) even if we were doing apprenticeship. 

Because of that, we stacked a lot of **Inadvertent** debt. 

Also, as a mall team and little time available, we added a lot of **Deliberate** debt on top of that. We wanted to deliver new features often. 

Per sprint, I had to 50% of my time to fix issues. Mostly missed during the development phase (low UTs), new bugs or miscommunication.

### How we decided to fix it

Of course we are heading to have only **Deliberate** debt. But **Inadvertent** debt will still happens as coding is a lifetime learning.

Due to the small time available, we work by feature to release. We focus on a single feature / fix to deploy. This prevent lots of context switching so we can optimize our focus and speed.

At the time we were giving an ASAP estimations. So we can deliver features quickly and build an attractive product.

We used Laravel (PHP framework) at first. It was a good pick back then considering we wanted something easy to go for both backend and frontend. Then the product got more complex and we needed to split it to be digestible.

The objective was not to fix everything in once. This is of course not acceptable for business to wait a quarter without new features/content. Even if the product quality will improve. 

We made a list of important improvements to do at Guid'me. Sliced them in the smallest units possible. And then we slightly increased the estimation of each "sprint" to add a few of those every time.

The product will not be perfect soon, but at least we stopped doing it the bad way all the time. And the quality is improving. 

First we will be moving frontend parts on JS Web Frameworks for better animations.
Then we will be migrate backend on Javascript micro-services. To do a proper refactor, and because the language is attractive to us. 

### Conclusion

Tech Debt is not something we should avoid at all costs. It is important to follow business needs and not do beautiful code for the sake of it.

But it is important to pay the debt when possible.

I would suggest a smooth approach as we did. Define a list of improvements you can do, slice them in small items, and bring a few (even one) of them on each sprint.   

#### Human impact

We talked about the cost of tech debt for your product and development, but it also impacts peoples. 

You can read this [article](https://daedtech.com/human-cost-tech-debt/) from Erik Dietrich for more details about this. 
  
<br /><br />

**Thank you for reading**  
