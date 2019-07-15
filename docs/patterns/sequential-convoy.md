---
title: Sequential Convoy   
description: The sequential convoy cloud design pattern allows for first-in-first-out processing of data in a serverless environment.
keywords: serverless, biztalk, sequential convoy, fifo, functions, messaging
ms.date: 07/12/2019
pnp.series.title: Cloud Design Patterns
pnp.pattern.categories: [design-implementation, messaging, performance-scalability] 
---

# Sequential Convoy

[!INCLUDE [header](../_includes/header.md)]

## Context and problem

Often, enterprises need the ability to process messages in the order in which they arrived, but in a way that allows the architecture to scale - often "infinitely" - to meet the needs of the load. First-in-first-out processing of messages is not straightforward in a distributed architecture like the cloud where many workers can scale independently of one another and often pull messages off queues, buses, or other messaging mechanisms independently.

## Solution

By pushing related messages in to categories within the queuing system, and forcing listeners on the queue to lock & pull only from one category, one message at a time, we can achieve this goal even in a distributed system.

## Issues and considerations

Consider the following points when deciding how to implement this pattern:

- Category/Scale unit - what property, if any, of your incoming messages *can* you scale out on?
- Throughput - what is your target message throughput? If it is very high, you may need to reconsider your FIFO requirements.
- Service capabilities - do provided services offer the level of control to allow for one-at-a-time processing of messages within a queue or category of a queue?
- Future scale - what will the process of adding a new category of message to the system look like?

## When to use this pattern

Use this pattern when:

- You have messages which **arrive in order** and must be **processed in the same order**.
- Arriving messages are or can be "categorized" in such a way that the category becomes a unit of scale for the system.

This pattern might not be suitable:

- Extremely high throughput scenarios (millions of messages/minute or second) as the FIFO requirement clamps the scaling which can be done by the system.

## Example

[orders + transactions diagram here]

## Next steps

The following information may be relevant when implementing this pattern:

- <a href="https://docs.microsoft.com/en-us/azure/service-bus-messaging/message-sessions" target="_blank">Service Bus Message sessions</a>
- <a href="https://docs.microsoft.com/en-us/rest/api/servicebus/peek-lock-message-non-destructive-read" target="_blank">Service Bus Peek Lock REST API</a>
- <a href="https://blogs.msdn.microsoft.com/logicapps/2017/05/02/in-order-delivery-of-correlated-messages-in-logic-apps-by-using-service-bus-sessions/" target="_blank">In order delivery of correlated messages in Logic Apps by using Service Bus sessions</a>
