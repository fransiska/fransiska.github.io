---
layout: post
title: "POST API in Rails"
description: ""
category: rails
tags: [rails]
date: 2014-11-21 15:08:48
---
{% include JB/setup %}

Trying to POST without using form in Rails, I got this error:

    Can't verify CSRF token authenticity
    Completed 422 Unprocessable Entity in 1ms
    ActionController::InvalidAuthenticityToken

To (temporarily?) solve this, add this line in the Controller:

    protect_from_forgery with: :null_session