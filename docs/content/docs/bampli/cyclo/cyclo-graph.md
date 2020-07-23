---
title: Graph
weight: 10
---
# Graph

The Cyclo graph has **Product** and **Stage** vertices and a bidirecional **sendW** edge.

![cyclo-v1-schema](https://user-images.githubusercontent.com/86032/86792421-dad42e80-c040-11ea-98c6-7e7f324c8d1b.jpg)

The raw material is a product that enters the process through a stage. Then, it becomes a work-in-process (wip) asset that moves from one stage to another, until the final product is obtained. The sendW edge expects to carry **wips** along the production flow, clustered by **timestep** property.

```groovy
// cyclo-v1-schema
schema.vertexLabel('Stage').
       ifNotExists().
       partitionBy('stage_name', Text).
       create();

schema.vertexLabel('Product').
       ifNotExists().
       partitionBy('product_name', Text).
       create();

schema.edgeLabel('sendW').
       ifNotExists().
       from('Stage').
       to('Stage').
       clusterBy('timestep', Int, Desc).
       create();

schema.edgeLabel('sendW').
       ifNotExists().
       from('Stage').
       to('Product').
       clusterBy('timestep', Int, Desc).
       create();

schema.edgeLabel('sendW').
       ifNotExists().
       from('Product').
       to('Stage').
       clusterBy('timestep', Int, Desc).
       create();
```
More details are shown at the links below:
- [Cyclo-v1](https://github.com/bampli/bampli/blob/master/datastax/models/cyclo-v1-schema.groovy) schema is provided for the Cyclo graph.
- Also a [CQL](https://github.com/bampli/bampli/blob/master/datastax/models/cyclo-v1-schema.cql) schema for Cassandra NoSQL. 
- This preliminar schema is inspired by the Datastax [graph-book](https://github.com/datastax/graph-book).

## P&Q Factory Cyclo

The [**P&Q Factory**](/docs/posts/pq-factory/) is used as a sample, its manufacturing production flow is shown below:

{{< mermaid >}}
graph LR
    PP[P-Part $5/u] --> D1[D 15min/u] --> P[P $90/u 100u/wk]
    RM1[RM1 $20/u] --> A1[A 15min/u] --> C1[C 10min/u] --> D1
    RM2[RM2 $20/u] --> B2[B 15min/u] --> C2[C 5min/u] --> D1
    C2 --> D2[D]
    RM3[RM3 $20/u] --> A3[A 10min/u] --> B3[B 15min/u] --> D2[D 5min/u] --> Q[Q $100/U 50u/wk]
{{< /mermaid >}}

It is also represented according to the product and stage vertices, as shown below:

![p q-graph](https://user-images.githubusercontent.com/86032/86799006-d2332680-c047-11ea-8d02-9da1042c1e51.png)

## Cyclo API

The [Cyclo API](https://app.swaggerhub.com/apis/motta/bampli) is located at the Business Amplifier project.

## Cyclo server

**bAmpli Cyclo Control**: Given a Cyclo, start it.

Product (Raw Material) --> Stage --> Stage --> Product (for Sale)
