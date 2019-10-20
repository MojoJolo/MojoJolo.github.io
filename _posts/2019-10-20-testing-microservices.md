---
layout: post
title: "Testing Microservices"
date: 2019-10-20
description: There are different kinds of testing, unit tests, integration tests, end to end tests, etc. Another kind of testing that I just recently learn about is contract testing. As I learned, contract testing is a good way to test microservices. According to Martin Fowler’s slide, contract testing is a test at the boundary of an external service verifying that it meets the contract expected by a consuming service.
---

Lately, I’ve been reading about how to test microservices. It’s been a learning experience for me since I don’t have that much background in testing.

I really enjoyed reading various software architectures. It’s actually interesting to come up architectures that can help to ease testing. As testing shouldn’t be a second class citizen. I believe that as much as possible, developers should write their own tests.

There are different kinds of testing: unit tests, integration tests, end to end tests, etc. Another kind of testing that I just recently learn about is contract testing. As I learned, contract testing is a good way to test microservices. According to Martin Fowler’s slide [1], contract testing is a test at the boundary of an external service verifying that it meets the contract expected by a consuming service.

In microservices, there is a producer and a consumer. Producer provides the input, and the consumer consumes it then do the necessary processes for an output.

Contracts, of course, are the essential part in contract testing. It determines what the consumer will expect and assert from the provider input.  Basically, a  consumer contract test is a test for the provider if it matches the expectations of a consumer [2]. If I understand it correctly, this can be called us consumer-driven contract testing.

On a different note, there is a relatively new architecture for building microservices. This is called “event-driven architecture”. There are different patterns of that architecture as can be seen in this Martin Fowler’s article [3]. One thing I like about it is “event-sourcing” in which it treats any changes in the system as an event and records it into some sort of a log. The log, or the event store is the source of truth in which the state is derived into. With this log, we can test the changes in the microservice by just replaying the events that happened.

Additional Readings:
1. [Consumer-Driven Contracts: A Service Evolution Pattern](https://martinfowler.com/articles/consumerDrivenContracts.html)
2.  [ContractTest](https://martinfowler.com/bliki/ContractTest.html) 
3. [Testing of Microservices](https://labs.spotify.com/2018/01/11/testing-of-microservices/)
4. [How to test Microservices with Consumer-Driven Contracts? - By Mateusz Sokola](https://hackernoon.com/how-to-test-microservices-with-consumer-driven-contracts-9bf5c2c05349)
5. [Don’t Let the Internet Dupe you, Event Sourcing is Hard - Blogomatano](https://chriskiehl.com/article/event-sourcing-is-hard)

Sources:
[1] [Testing Strategies in a Microservice Architecture](https://www.martinfowler.com/articles/microservice-testing/#testing-contract-introduction)
[2] Chapter 9, [Microservices Patterns by Chris Richardson](https://www.oreilly.com/library/view/microservices-patterns/9781617294549/)
[3] [What do you mean by “Event-Driven”?](https://martinfowler.com/articles/201701-event-driven.html)