---
layout: post
title: Scalable CI with Buildkite
excerpt: In this post I'll talk a bit about my thoughts on Buildkite, a continuous integration platform that allows companies to scale easily by providing an agents-based infrastructure.
tags: [2017, retro, year]
comments: true
image:
  feature: headers/2017.jpg
  credit: Photo by Pedro Piñera
sitemap   :
  priority : 0.9
  isfeatured : 1
---

It's hard to imagine a software project without any continuous integration nowadays. Our projects hosted on Git platforms are integrated with continuous integration infrastructures that build and run the tests. If a company is big enough they usually build an on-site infrastructure and have a team to maintain it. [Jenkins](https://jenkins-ci.org/) is probably one of the most popular solutions widely used in the industry. It's open source and highly extensible, which gives companies a lot of flexibility to set it up to satisfy their needs. If the company doesn't have enough resources for that, we find a lot of third-party solutions that take over all the related costs and lets you focus on just defining what needs to be done by their platform. Some examples of these solutions are [Travis CI](https://travis-ci.org/), [CircleCI](https://circleci.com), [Bitrise](https://www.bitrise.io/) or [BuddyBuild](https://www.buddybuild.com/) *(the last two are focused on mobile apps projects)*.

I personally use Travis CI in my open source projects *(they are mainly written in Swift)*. It's just a personal preference. I got used to it, it's simple and it just works. When you need a third-party service for open source projects they all offer the same so in the end, it's just a personal preference. You should just pick the one with which you are familiar and go ahead with it.

All these third party solutions offer a premium version of the product that allow you use it with private repositories. Moreover, it gives you things like more monthly builds, concurrent builds... These plans are thought to be used by companies that first, have the obvious need of maintaining their repos private and second, need the system to be efficient with its project and team size.

When software projects and teams grow, and there are a lot of people opening PRs during a work-day, the CI infrastructure can quickly become a bottleneck. As a result developers need to wait until there are availabe resources to build and test their changes, and get some feedback before proceeding with its work or merging the changes back to master. Any considerably-big company has been in a situation like this before, and it's something that can be improved in different ways. The first and most obvius is to optimize the build/test process. 


It's something that can usually be done by passing some flags or removing unnecessary steps. Although this helps, it doesn't a lot. The si


- Building and testing only what's necessary.
- Passing artifacts between pipeline steps.
- Easy parallelization.







there are a lot of people working on the projects. T


devote
commit