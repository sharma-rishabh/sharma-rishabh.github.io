---
title: "Event Driven Systems"
date: 2024-04-07T12:14:09+05:30
draft: false
tags:
  - tech
---

A system which does something on the basis of a consumed event is considered an event driven system.

### Event

An event is defined as a "significant change in state".

```
for sale -> sold
interviewed -> hired
low battery -> charging
```

We can build a system that performs certain operation on basis of these state changes. Any and all state changes can be considered an event.

An event shouldn't be confused with the message/data that we send with it.

### Publisher

A publisher is the part which observes these state changes and publishes an event with the attached message.

### Subscriber

A subscriber is the part which subscribes to one or more of the published event and may decide to perform an action or not.

### Why do we need it?

An Event driven system provides the freedom to deal with things asynchronously.
Any communication between a publisher and consumer need not be blocking as a publisher can move and perform other operations after publishing an event.

They are extremely useful for single threaded platforms which need to communicate with one another.

### Problem Statement

We want to make a system that can simulate a play where two characters talk to each other but both take some time to respond to each other. Like normal humans do. Try to come up with a solution of your own before looking at my [solution](https://github.com/sharma-rishabh/play)
