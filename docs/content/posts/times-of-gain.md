---
author: "José Motta Lopes"
date: 2020-04-28
linktitle: Times of Gain
menu:
  main:
    parent: tutorials
#next: /posts/github-pages-blog
#prev: /posts/automated-deployments
title: Times of Gain
weight: 90
tags: [
    "how-to-change",
]
---


{{< mermaid >}}
classDiagram
    Planet --> "1..n" Product : has
    Product --> "1..n" Process : made by
    Process --> "1..n" Stage : has
    Stage --> "1..n" Skill : requires
    Stage --> "1..n" Resource : uses
    Stage --> Stage : previous_next
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

### Prerequisites for Stage execution run in parallel

- For each allocated Resource, check its availability.
- If Resource is not available then wait.
- For the first time Resource is available, wait for the **Resource Initialization Time**.
- At each transformation, wait for the **Resource Setup Time**.

{{< mermaid >}}
stateDiagram
    [*] --> Alloc_Resources : Cyclo is running
    Alloc_Resources --> Execution
    Execution --> Release_Resources
    Release_Resources --> [*]
    state Alloc_Resources {
        alloc --> Cyclo
        Cyclo --> RM
        Cyclo --> WIP
        RM --> available : rm_ok
        WIP --> available : wip_ok
        alloc --> Facility
        Facility --> Energy
        Facility --> Area
        Energy --> available : energy_ok
        Area --> available : area_ok
        alloc --> Skill
        Skill --> Worker
        Skill --> Tool
        Tool --> available : tool_ok
        Worker --> available : worker_ok
    }
    state Execution {
        stage_execution
    }
    state Release_Resources {
        release --> WIP
        WIP --> Cyclo : wip_free
        release --> Area
        Area --> Facility : area_free
        release --> Energy
        Energy --> Facility : energy_free
        release --> Tool
        Tool --> Facility : tool_free
        release --> Worker
        Worker --> Facility : worker_free
    }


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

{{< mermaid >}}
sequenceDiagram
    autonumber
    Alice->>John: Hello John, how are you?
    rect rgb(0, 255, 0, .3)
        loop Healthcheck
            John->>John: Fight against hypochondria
        end
    end
    Note right of John: Rational thoughts!
    John-->>Alice: Great!
    rect rgb(0, 0, 255, .3)
        John->>Bob: How about you?
        Bob-->>John: Jolly good!
    end
    rect rgb(0, 0, 255, .3)
        John-xBob: How about you?
        Bob--xJohn: Jolly good!
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
