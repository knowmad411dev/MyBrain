---
tags:
- systems
---

## **From Monolithic to Microservices Architectures 101

## [](https://dev.to/encore/from-monolithic-to-microservices-architectures-101-3f2e?context=digest#introduction)Introduction

[![https://media4.giphy.com/media/UYgK6kSXD1WDu/giphy.gif?cid=7941fdc6fptefe0fdm2rpfsnozxvox6mvw4065mg2pbhymrp&ep=v1_gifs_search&rid=giphy.gif&ct=g](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fh17c3k5o2xmx9grw53a9.gif)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fh17c3k5o2xmx9grw53a9.gif)

Hello there, dear reader! Well, if you’re reading this I assume that you probably have already a basic understanding of how the web works and you probably got a few things done by yourself as well, so congrats on that!

The next big step is to understand a few of the patterns and architectures that exist out there. Not only that will make your software building more consistent, but also, way more solid too — from scalability to maintainability.

This article will explore two of the most popular software architectures: the monolithic architecture and the microservices architecture (with some other important concepts in between).

As always, we have a bunch of discussions regarding which of them is better and the answer here is as always the same: there’s no silver bullet, you should learn which are the cases for using each of them and how to transition between both as well to be a rational engineer.

## [](https://dev.to/encore/from-monolithic-to-microservices-architectures-101-3f2e?context=digest#first-one-the-monolith)First one: The Monolith

[![https://media4.giphy.com/media/kvT69yjOSlPtGPUexS/giphy.gif?cid=7941fdc6hg2npd5vgfjywwuckuamkd1c4u7j1u1sknwolmrp&ep=v1_gifs_search&rid=giphy.gif&ct=g](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fwq14ghsmp2kqb31xrn8x.gif)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fwq14ghsmp2kqb31xrn8x.gif)

In case you’re unfamiliar, the monolithic architecture is one of the most traditional ways to design software applications. In this approach, an application is built as a single unit — which we call the **monolith** — where the components of the software are interconnected and interdependent.

[![MVC model](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Ff1ydzol3dob0n2nn1kjh.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Ff1ydzol3dob0n2nn1kjh.png)

This architecture is characterized by a single codebase (usually using the [MVC pattern](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)), shared database, and typically a single deployment unit.

### [](https://dev.to/encore/from-monolithic-to-microservices-architectures-101-3f2e?context=digest#advantages)Advantages

Monolithic applications are often simpler to develop, especially for smaller projects or teams. They have a straightforward development process since the interactions between different parts of your application reside in the same place — this also means that there are generally fewer API calls and fiddling data around to make stuff work!

In terms of deployment, it generally is easier as well. Since you have a single unit, once you deploy it, everything should be up and running, meaning you don’t have any extra work on that.

When we talk debugging, it is generally simpler because the entire application runs within a single unit (which means you generally don’t have to jump around between multiple applications, trying to find the problem). End-to-end testing can also be easier and can run smoothly through entire journeys.

### [](https://dev.to/encore/from-monolithic-to-microservices-architectures-101-3f2e?context=digest#disadvantages)Disadvantages

As the application grows, a few challenges start to appear. The first one is organization-wise — since everything is in the same place keeping the context of a really big application and all the ramifications it goes through starts to become really hard (of course, there are ways to plan ahead — e.g. the [Modular Monolith](https://www.milanjovanovic.tech/blog/what-is-a-modular-monolith), for example — for that, but, when you build fast, this generally are not thought through).

The second one is scaling per se. Since the whole application is inside a single unit, specific usage-intensive points of your application will share the same resources as your whole app. This generally means that scaling things becomes a more complex task than just “pay more server power” or “rewrite that part in a different tech”.

## [](https://dev.to/encore/from-monolithic-to-microservices-architectures-101-3f2e?context=digest#microservices-architecture)Microservices Architecture

[![https://media4.giphy.com/media/3o7TKzhPqGvUDm3pba/giphy.gif?cid=7941fdc6gzzw7dc1eobe4qlg3miho0oxvu4dt4ozve3x0bmc&ep=v1_gifs_search&rid=giphy.gif&ct=g](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fo36zk5b54blsd5s0cg75.gif)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fo36zk5b54blsd5s0cg75.gif)

Now, the general alternative to a Monolith is the Microservices architecture. It’s an approach to developing a single application as a suite of small services (that’s where the micro comes from), each running in its own process and communicating with lightweight mechanisms to keep it all running. They can usually be developed, deployed, and scaled separately. Each service typically has its own database and communicates with other services through well-defined APIs.

It also has its own patterns of organization (which there are a ton of famous books about) where one of the most common ones is [DDD (Domain-Driven Design)](https://en.wikipedia.org/wiki/Domain-driven_design#:~:text=Domain%2Ddriven%20design%20(DDD),which%20have%20their%20own%20model.).

### [](https://dev.to/encore/from-monolithic-to-microservices-architectures-101-3f2e?context=digest#advantages)Advantages

The first and most obvious one is scale. Microservices can be scaled independently, allowing for more efficient resource utilization throughout the segments of your app. Since everything has to communicate as a black box, this architecture also provides flexibility in choosing technologies for different services.

The second one is that when we are talking about really big apps, the complexity of the code of microservices is distributed between them. This generally means that, if a microservice has a bug, it’s simple to send a new engineer of the team to go take a look at it — there’s not that much space where this bug can exist anyway.

### [](https://dev.to/encore/from-monolithic-to-microservices-architectures-101-3f2e?context=digest#disadvantages)Disadvantages

The first one is that making all those things communicate and interact properly can be a real challenge. God only knows how much time an engineer is capable of spending trying to find why messages from Kafka are not arriving or any other weird problem that can happen. Managing all that, their infrastructure, and deployments can be hard.

The second one is that the context is more segmented — this can be a good thing when we look at it coming from the point of view of learning the code base, but this can be a pain when looking at it as learning the product — it’s way easier to follow if your code goes through 5 files than 5 different apps.

The last one is that microservices have a caveat which is **Latency**. If they’re not designed properly, it’s quite possible that the separation of concerns and expected speed increase will not pay off since now you also added a bunch of different calls for them all to communicate.

___

And sometimes, when people create new stuff, they try to fix part of those problems, which is part of the feature set of Encore, the sponsor of this article:

[![Encore Logo](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F3ukalf9gco9fxdwater5.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F3ukalf9gco9fxdwater5.png)

A great standout feature for me is that you [don’t need to worry about the communication between different microservices](https://encore.dev/docs/ts/primitives/api-calls) as much as you’d normally have to. It’s a really great idea — you have almost the same developer experience as when you’re working with a monolith, but, with all the scaling power of a microservice.

[![Picture of an architectural flow](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Frh9lamz2gpldqdnkffby.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Frh9lamz2gpldqdnkffby.png)

In this case, for example, you can call a service from inside another one by simply importing it

[![Service call from inside of other service](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fo567j3c9n17t6tb7fctp.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fo567j3c9n17t6tb7fctp.png)

There are also a ton of features to make the [deployment process of multiple services](https://encore.dev/docs/platform/infrastructure/infra) easier as well. They’re really trying hard to make that bridge of having the best of both worlds happen and it would be awesome if you could check them out and give them a star!

[⚡ Star Encore ⚡](https://github.com/encoredev/encore)

___

## [](https://dev.to/encore/from-monolithic-to-microservices-architectures-101-3f2e?context=digest#choosing-the-right-architecture)Choosing the Right Architecture

[![https://media3.giphy.com/media/3oKIPqsXYcdjcBcXL2/giphy.gif?cid=7941fdc66769jwvvnan2swwe8q12afmc8k5gdignwevs3s5i&ep=v1_gifs_search&rid=giphy.gif&ct=g](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Facmpmybod9sld8ymyyw0.gif)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Facmpmybod9sld8ymyyw0.gif)

When deciding between architectures, you'll need to consider your application's growth potential, team size, and how complex your product actually is.

The simpler your app is, the more you can benefit from a monolithic approach. If you’re in doubt, the safest choice is going with a monolith — you can always break things apart later, but, stitching things up is HARD (here’s a great source to read if you’re still in doubt: [Monolith First](https://martinfowler.com/bliki/MonolithFirst.html))

| **Architecture** | **Key Benefit** | **Key Disadvantage** | **Best For** |
| --- | --- | --- | --- |
| Monolithic | Simplified development, deployment and debugging | Growing issues | Small to normal-sized applications and MVPs (e.g. [DEV.to](https://github.com/forem/forem) is a monolith!) |
| Microservices | Independent scaling of components | Complex management | Really large applications with multiple teams (e.g. [Netflix](https://netflixtechblog.com/the-making-of-ves-the-cosmos-microservice-for-netflix-video-encoding-946b9b3cd300) uses a ton of microservices) |

As complexity grows, you might want to consider breaking things apart, so, let’s talk a little bit about how can you convert a monolith into a series of microservices.

### [](https://dev.to/encore/from-monolithic-to-microservices-architectures-101-3f2e?context=digest#converting-how-to-migrate-from-monoliths-to-microservices)Converting: How to migrate from monoliths to microservices.

![https://media2.giphy.com/media/26BGIqWh2R1fi6JDa/giphy.gif?cid=7941fdc6uggvsyc10h6vs8so9wj77mderowc1fc9f8ovssc4&ep=v1_gifs_search&rid=giphy.gif&ct=g](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Faqahwgb1eevzvof3x9an.gif)

There are a few ways to migrate from a monolith into the microservice world. Let’s quickly go through them:

-   [Greenfield](https://en.wikipedia.org/wiki/Greenfield_project) Replacement: Simply creating things from the ground up — not having constraints from prior work can be really beneficial in some cases. But, of course, we have a bunch of inherent possible problems here (how long will it take? how much time will users suffer? etc)
-   [Brownfield](https://en.wikipedia.org/wiki/Brownfield_(software_development)) Replacement: New architectures should coexist with live software. When we’re talking about brownfield replacement, there can be a lot of pain and headache in coexisting things with old/problematic software. An interesting approach to solve on how to tackle this problem is the [Strangler Fig pattern](https://en.wikipedia.org/wiki/Strangler_fig_pattern), where, we’ll generally wrap, little by little as a strangler fig, the old code and redirect it to newer code, eventually killing it. This makes the transition more smooth and also less risky.

Generally, here are the steps we are going to take:

1.  Identify clear boundaries within the existing application.
2.  Gradually extract services, starting with less critical components.
3.  Implement new features as separate services
4.  Refactor the existing codebase to support the new architecture
5.  Ensure robust testing and monitoring throughout the migration process → Nothing is as hard as changing your application blindly

## [](https://dev.to/encore/from-monolithic-to-microservices-architectures-101-3f2e?context=digest#conclusion)Conclusion

[![https://media0.giphy.com/media/T9JtEyoJ43gY4wLOqW/giphy.gif?cid=7941fdc6termxktyz4bgwbvc106kw8jauebencv8291a4w6m&ep=v1_gifs_search&rid=giphy.gif&ct=g](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fh7k8o0gx9s32coqytkim.gif)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fh7k8o0gx9s32coqytkim.gif)

Hey! We've gone through quite a journey here. We talked about two main architectural approaches: the good old monolith (simple, and straightforward, but with growing challenges) and microservices (flexible, and scalable, but way more complex to manage).

I hope that you’re now able to choose things (or at least have a great gut feeling) for the next choice you’re going to make, but, remember: there's no "one size fits all" - if you're starting something new, go with a monolith first if not, think it through!

At the end of the day, what matters is picking the right tool for the job. Understanding these patterns will help you make better decisions for your specific needs. And remember: you can always change things later - just make sure you have a solid plan for that transition!

[[Software Architect Knowledge Roadmap]]  [[Information Architecture]]