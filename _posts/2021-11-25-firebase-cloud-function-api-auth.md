---
layout: post
title: Firebase Cloud Function REST API Authentication
category: firebase
tags: [firebase, api, web, rest]
---

It is so hard to find a good reference for Firebase. In particular I wasn't really able to find a good example on how to authenticate a REST API served by Firebase Google Cloud Function. AFAIK Python Admin SDK cannot call google cloud function. Actually, I'm not too sure if this is actually secure. :confused:

There is [one guide](https://firebase.google.com/docs/database/rest/auth#python) on authenticating for REST API of Realtime Database, but it didn't work for the cloud function.

### On Firebase Cloud Function

It can validate the ID Token, as well as get the data from Realtime Database as admin.

```javascript
const functions = require('firebase-functions');
const admin = require('firebase-admin');
const express = require('express');
const app = express();

let db = admin.database();

app.get('/', (req, res) => {
  const authorization = req.get('Authorization');
  if (!authorization) {
    res.send({"status":"error","error":"Not authorized"});
    return;
  }
  const idToken = req.get('Authorization').slice(6,);
  admin.auth()
    .verifyIdToken(idToken)
    .then((decodedToken) => {
      const uid = decodedToken.uid;
      return db.ref('users').once("value");
    })
    .then((value) => {
      res.send(value.val());
    })
});
exports.test = functions.https.onRequest(app);
```

### On python admin SDK

```python
# Both Firebase and Emulator needs a credential file (Service Account Key from Cloud Console)
cred = credentials.Certificate('credentials.json')
default_app = initialize_app(cred, {
  "projectId": "myproject"
})
custom_token = auth.create_custom_token("myuid")
api_key = "actualKeyForFirebaseOrRandomStringForEmulator"

# For Firebase
response = requests.post("https://identitytoolkit.googleapis.com/v1/accounts:signInWithCustomToken?key="+api_key, json={"token":custom_token,"returnSecureToken":True})

# For Emulator
response = requests.post("http://localhost:9099/identitytoolkit.googleapis.com/v1/accounts:signInWithCustomToken?key="+api_key, json={"token":custom_token,"returnSecureToken":True})

id_token = response.json()["idToken"]
url = "https://us-central1-myprojectid.cloudfunctions.net/myfunctionname"
url = "http://0:0:0:5001/myprojectid/us-central1/myfunctionname"
requests.get(url, headers={"Authorization":"Token "+id_token})
```
