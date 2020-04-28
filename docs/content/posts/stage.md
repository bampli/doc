---
author: "José Motta Lopes"
date: 2020-04-28
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

In order to analyze thoroughly the **Stage** of the **Process**, we should consider the production flows that results in the final **Product** for the consumer.

## The Production Flow

Although the following example shows a *manufacturing* process, these flows can also be applied to generic *environments* where **resources** are used for **tasks** that require **skills**, to achieve a **goal**.

In order to extract a process sample, the [**P&Q Factory**](/docs/posts/pq-factory/), shown below, will be used as an example.

{{< mermaid >}}
graph LR
    PP[P-Part $5/u] --> D1[D 15min/u] --> P[P $90/u 100u/wk]
    RM1[RM1 $20/u] --> A1[A 15min/u] --> C1[C 10min/u] --> D1
    RM2[RM2 $20/u] --> B2[B 15min/u] --> C2[C 5min/u] --> D1
    C2 --> D2[D]
    RM3[RM3 $20/u] --> A3[A 10min/u] --> B3[B 15min/u] --> D2[D 5min/u] --> Q[Q $100/U 50u/wk]
{{< /mermaid >}}

Initially, the partial elements shown below represent **RM1 being processed by A** for 15 minutes. This means that something happens to the raw material RM1, causing its exit from A in a different state. This new asset is actually a fragment, known by the generic term  **work in process (WIP)**.

{{< mermaid >}}
graph LR
    RM1[RM1 $20/u]-- raw material --> A1[A 15min/u]-- work in process --> C1[C 10min/u]
{{< /mermaid >}}

Then, **C processes the WIP for 10 minutes**. Please note that the C input is not RM1 anymore, since it was already transformed by A. It is also implied in the production flow diagram that:

- RM1 is a **resource** to A, and WIP is a **resource** to C as well.
- RM1 is an **external** asset, since it comes from outside the process.
- WIP is a **internal** asset, i.e. an intermediary result inside the process.
- The transformation in RM1 is a **task** that requires 15 minutes of A's work.
- Similarly, the WIP is processed by a **task** that requires 10 minutes from C.
- A and C are workers with specific **skills**, also named "A" and "C" here.
- It is convenient to separate the **worker** from its **skill**.
- Actually the **task** is a **Stage** that requires a **skill**.
- The **worker** is a **resource** with the necessary **skill** to accomplish the job.
- A **tool** with a skill is another **resource** that can also be used.
- The skills may be combined, for example, a worker **commands** a robot.

We can also assure that the **resources** come from different sources:

- RM and WIP are resources related to the **Cyclo**.
- Workers, tools, shop floor area, etc. are implemented by the **Facility**.

## The Stage Model

Then, we have the following modeling that includes the **Stage**:

{{< mermaid >}}
classDiagram
    Planet --> "1..n" Product : has
    Product --> "1..n" Process : made by
    Process --> "1..n" Stage : has
    Stage --> "1..n" Skill : requires
    Stage --> "1..n" Resource : uses
    Stage --> "1..n" Stage : flows
    Worker --> "1..n" Skill : has
    Worker --> "0..n" Tool : command
    Tool --> "0..n" Tool : command
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

The model highlights the following features:

- The **Planet** has at least one **Product**.
- Each **Product** has at least one **Process** that leads to its creation.
- Each **Process** has at least one **Stage** to be executed.
- The **Stage** must use at least one **Resource**.
- The **Stage** proceeds to at least another **Stage**, until the consumer **Product** is reached.
- The **Resource** must be related to the **Cyclo** or to the **Facility**.
- The **Cyclo Resource** shall be **Raw Material (RM)** or **Work in Process (WIP)**.
- **RM** is a **external** resource coming from another **Process**.
- **WIP** is a **internal Process** resource.
- The **Facility** has resources like **Worker**, **Tool**, **Area**, and **Energy**, among other.
- Both **Worker** and **Tool** have at least one **Skill**.
- **Worker** & **Tool** may handle a **Tool** with a **Command**, but this is not mandatory.
- The **Stage** requires at least one **Skill**, satisfied by a **Worker** or **Tool** resource attached to it.

In order to audit a Process and certify that it is able to run, the information system shall follow all its Stages, and check if the corresponding Skills are being satisfied by the Facility implementation. Attached Worker and Tool resources must permanently comply with the required Stage expertises, in order the Process may keep running.

{{< hint info >}}
**This project is published in [Business Amplifier](https://www.amazon.com/Business-Amplifier-M-Sc-Motta-Lopes/dp/B083XGK14Q), also [e-book](https://www.amazon.com/Business-Amplifier-Jose-Motta-Lopes-ebook-dp-B086L6V6QY/dp/B086L6V6QY/) and [Amplificador de Negócios](https://www.amazon.com/M-Sc-Jose-Motta-Lopes/dp/8592301009).**
{{< /hint >}}
