---
layout: post
title: "RxJava - A Few Lessons Learned"
description: "Quick thoughts after using RxJava for a few months"
date: 2016-09-17
tags: [rxjava, android]
comments: true
share: true
---

I have recently started doing Android development full time and have been loving every minute of it.  As if the challenge of being a newbie in this domain was not enough I decided that in my most recent project, which is an entire app rewrite, that I wanted to use RxJava.  I am learning something new everyday, some times I am unlearning what I learned the week before but that is part of the process, right? Being that this is my inaugural post I just wanted to jot down some of the lessons I have learned while using RxJava over the last couple months.  Admittedly I am very new to this so I expect some(or all) of these opinions to change over time as I become more familiar.

-  **Do not be afraid of Subjects (sort of)** - You will read a lot of articles out there telling you if you are using a Subject you are doing something wrong.  That may be but, when you are tasked with converting a legacy codebase and you are just learning the paradigm of reactive programming Subjects do a good job of temporarily bridging that gap for you.  The big thing to remember about Subjects is they will stop emitting results once they call onComplete or onError.  The onError issue has tripped me up a couple times, you can consider using RxRelay in place of Subjects, which are basically subjects that do not call onError or onComplete.
- **If order matters use concatMap over flatMap** - They look exactly the same at first glance but the difference is under the hood with how they end up emitting items back into the stream.  The flatMap operator runs concurrently and the concatMap operator runs sequentially. This means flatMap can interleave the results, while concatMap will preserve ordering.
- **Declarative and Imperative can work together** - It will be tempting to use as much RxJava as possible, I was doing this, and you end up over engineering.  The tried and true imperative approach you know so well has not become the devil and can be used in conjunction with the new tools RxJava provides, done right you will get the best of both worlds.
- **RxJava makes heavy use of immutable objects** - Each observable returned in the chain is a new observable, you are not updating the same observable.  This does not mean the value inside an observable is immutable though.  If you create an observable from a property of your class and change it inside of the map operator, it will change the value of the original property.

These are just a few of the things I have picked up as I work through my massive rewrite.  In future posts I will dive deeper into each of these points as I get my head wrapped around them more.