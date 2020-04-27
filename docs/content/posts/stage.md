---
author: "José Motta Lopes"
date: 2020-04-20
linktitle: The Stage
menu:
  main:
    parent: tutorials
#next: /posts/github-pages-blog
#prev: /posts/automated-deployments
title: The Stage
weight: 80
tags: [
    "how-to-change",
]
---

In order to analyze thoroughly each **Stage** of the **Process**, we should consider initially the production flow that results in the **Product**.

## The Production Flow

Although the following example shows a *manufacturing* process, these flows can also be applied to generic *environments* where **resources** are used for **tasks** that require **skills**, to achieve a **goal**.

In order to use a process sample, the [**P&Q Factory**](/docs/posts/pq-factory/) is shown below.

{{< mermaid >}}
graph LR
    PP[P-Part $5/u] --> D1[D 15min/u] --> P[P $90/u 100u/wk]
    RM1[RM1 $20/u] --> A1[A 15min/u] --> C1[C 10min/u] --> D1
    RM2[RM2 $20/u] --> B2[B 15min/u] --> C2[C 5min/u] --> D1
    C2 --> D2[D]
    RM3[RM3 $20/u] --> A3[A 10min/u] --> B3[B 15min/u] --> D2[D 5min/u] --> Q[Q $100/U 50u/wk]
{{< /mermaid >}}

The partial elements shown below represent initially **RM1 being processed by A** for 15 minutes. This means that something happens to the raw material RM1, causing its exit from A in a different state. This new asset is actually a fragment, known by the generic term  **work in process (WIP)**.

{{< mermaid >}}
graph LR
    RM1[RM1 $20/u]-- raw material --> A1[A 15min/u]-- work in process --> C1[C 10min/u]
{{< /mermaid >}}

Then, **C processes the WIP for 10 minutes**. Please note that the C input is not RM1 anymore, since it was already transformed by A. It is also implied in the flow diagram that:

- RM1 is a **resource** to A, and WIP is a **resource** to C as well.
- RM1 is an **external** asset, since it comes from outside the process.
- WIP is a **internal** asset, i.e. an intermediary result inside the process.
- The transformation in RM1 is a **task** that requires 15 minutes of A's work.
- Similarly, the WIP is processed by a **task** that requires 10 minutes from C.
- A and C are workers with specific **skills**, also named "A" and "C" here.
- It is convenient to separate the **worker** from its **skill**.
- Actually the **task** needs a **skill**.
- The **worker** is a **resource** with the necessary **skill** to accomplish the job.
- An equivalent tool with same skill is a **resource** that could also be used.
- The skills may be combined, for example, a worker commands a robot.

We can also assure that the **resources** come from different sources:

- the Raw Material and WIP are resources related to the **Cyclo**.
- the Workers, tools, shop floor area, etc are implemented by the **Facility**.

## The Stage Model

Then, we have the following modeling that includes the **Stage**:

{{< mermaid >}}
classDiagram
    Planet --> "1..n" Product : has
    Product --> "1..n" Process : made by
    Process --> "1..n" Task : has
    Task --> "1..n" Skill : needs
    Task --> "1..n" Resource : uses
    Task --> "1..n" Task : flows
    Worker --> "1..n" Skill : has
    Worker --> "0..n" Tool : command
    Tool --> "1..n" Skill : has
    Resource <|-- Cyclo
    Resource <|-- Facility
    Cyclo <|-- RM : external
    Cyclo <|-- WIP : internal
    Facility <|-- Worker
    Facility <|-- Tool
    Facility <|-- Energy
    Facility <|-- Area
{{< /mermaid >}}

{{< mermaid >}}
sequenceDiagram
    Alice->>Bob: Hello Bob, how are you?
    alt is sick
        Bob->>Alice: Not so good :(
    else is well
        Bob->>Alice: Feeling fresh like a daisy
    end
    opt Extra response
        Bob->>Alice: Thanks for asking
    end
{{< /mermaid >}}

{{< katex >}}
\begin{gathered}
   wk&=2400\,min \qquad
   OE&=\$6000/wk
\end{gathered}
{{< /katex >}}

{{< hint info >}}
**This project is published in [Business Amplifier](https://www.amazon.com/Business-Amplifier-M-Sc-Motta-Lopes/dp/B083XGK14Q), also [e-book](https://www.amazon.com/Business-Amplifier-Jose-Motta-Lopes-ebook-dp-B086L6V6QY/dp/B086L6V6QY/) and [Amplificador de Negócios](https://www.amazon.com/M-Sc-Jose-Motta-Lopes/dp/8592301009).**
{{< /hint >}}
