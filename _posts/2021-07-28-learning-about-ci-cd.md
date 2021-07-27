---
layout: post
title: Gitlab Pages and Learning About CI/CD
---

Just recently (duh!) I came to realize that Gitlab Pages is actually a CI/CD process. The automation of everything is so mind blowing!

I am looking for an easy way to use Gitlab Pages as internal documentation. Not sure what to use, Sphinx or MkDocs, or even a custom one. It's be nice if we can customize the documentation build (internal / customer A / customer B, etc). MkDocs sounds simple enough to use and even people who are not proficient with programming can write in MarkDown format. Gitlab view itself is actually good enough for internal documentation since it's rendered automatically and intenal hyperlinking works.

And while looking at the documentation for [Gitlab Pages](https://docs.gitlab.com/ee/user/project/pages/getting_started/pages_from_scratch.html#choose-a-docker-image) I came accross that it's actually using a Docker image. I've been wanting to learn more about Docker. It's cool that there is DockerHub where lots of images are available to be used from Gitlab CI/CD! And it seems like we can create public images for free! [This](https://www.vipinajayakumar.com/continuous-integration-of-latex-projects-with-gitlab-pages.html) small tutorial also helps me understand more about CI/CD and Docker. Now I feel like I know more about it. But it seems to be so cumbersome to set up a custom one.. It feels like setting up dot emacs file.

Relating on that, I've been looking at the quota being used. I saw my quota is 400, but I only see minutes being consumed for one repo, a private one. Apparently Gitlab is limitting public repo's CI minutes to be 50,000 for free plan (Adjusted by 0.008 to the 400 minutes quota), not unlimited anymore (Not sure why our group's quota is still 2000 minutes, though). I was reading [the issue](https://gitlab.com/gitlab-org/gitlab/-/issues/243722) where they're discussing how to implement the limitation. The limitation is [quite recent](https://docs.gitlab.com/ee/subscriptions/gitlab_com/index.html#ci-pipeline-minutes), just 2 weeks ago.

Working remotely for Gitlab sounds so nice, but I think every company has the problem of business policies vs engineering solutions, =|

I was wondering if I were to build ROS packages, that'd take a lot of time, and wonder if there are other services like Travis maybe. Then I came across an issue at [curl](https://github.com/curl/curl/issues/7150) that Travis is also limitting the minutes for public projects that they're replacing it to another service. Wow.

Not a productive morning just reading through these issues, but it was an interesting insight.
