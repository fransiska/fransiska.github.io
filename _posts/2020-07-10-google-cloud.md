---
layout: post
title: Google Cloud
category: web
tags: [web, cloud]
---

2 years ago when I started using cloud service, specifically google's, I didn't really know about the difference between services, blindly following tutorials. Heck, even now I don't really have a clue as well (too many cloud services, especially AWS!).

Just today I found out that google cloud function for Node.js 8 will be deprecated and everyone is asked to update to version 10, which also requires Blaze plan, which means giving google a credit card number. That sucks. I didn't know until today that I can actually make google function with python. I should've used this 2 months ago if I knew Blaze plan would be required...

## Google Function with Firebase Admin in python

1. In one folder, create `requirements.txt` and `main.py`
2. Login with `gcloud auth login`
3. Deploy function with `gcloud functions deploy firebase_test --runtime python37 --trigger-http `
4. Add allUsers by adding members from google cloud console

`requirements.txt`

```
Flask==1.0.2
firebase-admin
```

`main.py`

```python
import firebase_admin
from firebase_admin import db
import flask

firebase_admin.initialize_app(options={
    'databaseURL': 'https://<path>.firebaseio.com',
})

root_ref = db.reference('ref')

def firebase_test(request):
    name = root_ref.child("name").get()
    if not name:
        return 'Resource not found', 404
    return flask.jsonify({"name":name})
```

For Firebase Auth, I need to check [this](https://github.com/GoogleCloudPlatform/python-docs-samples/blob/master/functions/firebase/main_test.py#L67).

## Google App Engine

Dialogflow's inline fulfillment will also be required to use Node.js 10 I suppose (I think it only allows javascript). Also, without Blaze plan outbound request (request to server other than google) is not possible. I didn't remember that I was actually making outbound request in Dialogflow's fulfillment. I thought it wasn't working and finally I just noticed that 2 years ago I actually used Google App Engine for the fulfillment, which apparently **allows outbound request**.

## Sending Email

1. Google App Engine: 100 email per day, or use Mailjet (free for 6000 email per month)
2. Google Function: Using gmail only for 500 email per day, or use nodemailer with Blaze plan
