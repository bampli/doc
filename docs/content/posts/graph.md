---
author: "José Motta Lopes"
date: 2020-07-13
linktitle: Cyclo Graph
menu:
  main:
    parent: tutorials
#next: /posts/github-pages-blog
#prev: /posts/automated-deployments
title: Cyclo Graph
weight: 100
tags: [
    "how-to-change",
]
---
## Cyclo Graph Model

The Cyclo has **Product** and **Stage** vertices and a **sendW** edge with **timestep** property.

![cyclo-v1-schema](https://user-images.githubusercontent.com/86032/86792421-dad42e80-c040-11ea-98c6-7e7f324c8d1b.jpg)

- [Cyclo-v1 Schema](https://github.com/bampli/bampli/blob/master/datastax/models/cyclo-v1-schema.groovy) is provided for the Cyclo graph
- Also a [CQL Schema](https://github.com/bampli/bampli/blob/master/datastax/models/cyclo-v1-schema.cql) for Cassandra NoSQL database 

## P&Q Factory Cyclo

The [**P&Q Factory**](/docs/posts/pq-factory/) is loaded as a sample, the corresponding graph is shown below.

{{< mermaid >}}
graph LR
    PP[P-Part $5/u] --> D1[D 15min/u] --> P[P $90/u 100u/wk]
    RM1[RM1 $20/u] --> A1[A 15min/u] --> C1[C 10min/u] --> D1
    RM2[RM2 $20/u] --> B2[B 15min/u] --> C2[C 5min/u] --> D1
    C2 --> D2[D]
    RM3[RM3 $20/u] --> A3[A 10min/u] --> B3[B 15min/u] --> D2[D 5min/u] --> Q[Q $100/U 50u/wk]
{{< /mermaid >}}

![p q-graph](https://user-images.githubusercontent.com/86032/86799006-d2332680-c047-11ea-8d02-9da1042c1e51.png)

This schema is inspired by the valuable [Datastax graph-book](https://github.com/datastax/graph-book).

## Cyclo server

**bAmpli Cyclo Control**: Given a Cyclo, start it.

Product (Raw Material) --> Stage --> Stage --> Product (for Sale)

## Cyclo API

The [Cyclo API](https://app.swaggerhub.com/apis/motta/bampli) is located at the Business Amplifier project.


