---
title: "Design for a Event-driven Mocking Tool"
date: 2021-03-13T07:37:15Z
draft: true
---

I need to implement a simulator for event-based systems. This article is a
summary of the design decisions and details.

I'm going to call this simulator _EventMock_, inspired by
[WireMock](http://wiremock.org/).

## Why do I need EventMock?

Well, I'm building [Sagas](https://microservices.io/patterns/data/saga.html),
using orchestration to coordinate event-based services and I need to be able to
[test orchestrator flows isolated](https://martinfowler.com/articles/microservice-testing/#testing-component-in-process-diagram).

(TODO: give an example with an image)

## Event-driven architectures

_Event-driven architecture (EDA) is a software architecture paradigm promoting
the production, detection, consumption of, and reaction to events_
([wikipedia](https://en.wikipedia.org/wiki/Event-driven_architecture)).

EDA commonly centers in a message broker, like the example below:

`Publisher -> Message Broker -> Subscriber`

Let's go over the concepts in more detail.

### Message broker

A message broker (or "broker") is responsible of receiving messages and
delivering them to those who need to process them. Examples of brokers are
RabbitMQ, Apache Kafka, AWS EventBridge, etc.

### Publisher/Subscriber

A publisher (or producer) is an application that sends messages to the broker.

A subscriber (or consumer) is an application that connects to the broker,
manifests an interest in a certain type of messages, and leaves the connection
open so the broker can push messages to them.

### Message

A message is a piece of information that's sent by the publishers to the broker,
and received by all the interested subscribers. The content of the message can
be anything, but they are frequently catalogued as events and commands.

Events communicate a fact that occurred. Commands are very much like requests in
REST APIs: they tell the subscribers "do this".

Technically speaking, events and commands are the same. The only difference is
in their semantics.

### Channels

All the brokers support communication through multiple channels. The industry
doesn't have a common term though so you may find them as topics, routing keys,
event types, etc.

## Brokers / Protocols

When using REST APIs, the most common transport is HTTP/S. For event-based
systems, the options are much more diverse. So I'm considering a design where
the core of EventMock can be agnostic of the transport or message broker used.
Therefore, it should be possible to support MQTT, Kafka, AWS EventBrige, and
others without significant effort.

### AsyncAPI

_AsyncAPI is an open-source initiative that seeks to improve the current state
of Event-Driven Architectures (EDA). Our long-term goal is to make working with
EDAs as easy as working with REST APIs. That goes from documentation to code
generation, from discovery to event management. Most of the processes you apply
to your REST APIs nowadays would apply to your event-driven/asynchronous APIs,
too._

More info at [https://www.asyncapi.com](https://www.asyncapi.com).

:bulb: Should the configuration of EventMock use AsyncAPI or use a simpler
approach like WireMock, only minimal definitions are needed to set a
request/response?

## What features do I like about WireMock?

The following features of WireMock make it very easy to setup, use and manage:

1. Easy to run as a standalone server (JAR file & Docker)
1. Easy configuration using a REST API and JSON
1. Request matching with support for patterns
1. Request matching using priorities
1. Support for transformers for the responses
1. Supports dynamic responses using
   [handlebars templates](https://handlebarsjs.com/)
1. Support for post response actions

## Mocking flow

The mocking flow:

1. Subscribe channel
1. Receive message
1. Match request
1. Generate response
1. Send response

The _Match request_ and _Generate response_ steps should be agnostic from the
broker used and therefore use standard like JSON to represent the events.

Let's get into the details.

### Subscribe Channel

### Receive message

### Match request

### Generate response

### Send response
