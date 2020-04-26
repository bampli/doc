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

{{< mermaid >}}
graph LR
    PP[P-Part $5/u] --> D1[D 15min/u] --> P[P $90/u 100u/wk]
    RM1[RM1 $20/u] --> A1[A 15min/u] --> C1[C 10min/u] --> D1
    RM2[RM2 $20/u] --> B2[B 15min/u] --> C2[C 5min/u] --> D1
    C2 --> D2[D]
    RM3[RM3 $20/u] --> A3[A 10min/u] --> B3[B 15min/u] --> D2[D 5min/u] --> Q[Q $100/U 50u/wk]
{{< /mermaid >}}

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

{{< katex >}}
\begin{gathered}
   wk&=2400\,min \qquad
   OE&=\$6000/wk
\end{gathered}
{{< /katex >}}

{{< hint info >}}
**This project is published in [Business Amplifier](https://www.amazon.com/Business-Amplifier-M-Sc-Motta-Lopes/dp/B083XGK14Q), also [e-book](https://www.amazon.com/Business-Amplifier-Jose-Motta-Lopes-ebook-dp-B086L6V6QY/dp/B086L6V6QY/) and [Amplificador de Negócios](https://www.amazon.com/M-Sc-Jose-Motta-Lopes/dp/8592301009).**
{{< /hint >}}
