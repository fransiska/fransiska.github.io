---
layout: post
title: Firebase Rules Unit Testing
category: firebase
tags: [firebase, test]
---

I just recently started reading about Agile and Test Driven Development. Youtube video of Uncle Bob speaking in Netherland was really insightful (The way he describes customer don't know what they want until they see what they don't want is so true!).

Anyway, I want to start using test functions in my codes, and a good start is to implement it in a new project. Just at this time I'm developing another Firebase project. I need mocha for the test and typescript to be able to import the interface that I used in my App. I hate setting up node js projects because I don't really understand how to make it work (and the versioning problem as well). But I managed to set it up quite easily.

Installed dependencies (dev):
- "@firebase/rules-unit-testing": "^1.1.10"
- "@types/mocha": "^8.2.0"

Installed dependencies:
- "firebase": "^7.21.1"
- "firebase-admin": "^9.4.2"
- "firebase-tools": "^8.18.1"
- "mocha": "^8.2.1"
- "ts-node": "^9.1.1"

Running script (`package.json`): `mocha --exit --require ts-node/register test/test.ts`


Importing mocha in `test/test.ts`:
```typescript
import "mocha";
import * as fs from "fs";
import * as firebase from '@firebase/rules-unit-testing';
```

And the rest is as the example from [here](https://github.com/firebase/quickstart-testing/blob/master/unit-test-security-rules/test/database.spec.js)

Neat!
