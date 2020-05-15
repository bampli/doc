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
## Stage Model

The **Stage** model shows below more details about the **Facility**, that is now divided into:
- **Facility_Infra** that includes the infrastructure items, like Shop Floor Area, Energy, etc.
- **Facility_Op** that takes care of operational items, like Tools and Workers with **Skills**.

{{< mermaid >}}
classDiagram
    Planet --> "1..n" Product : has
    Product --> "1..n" Process : made by
    Process --> "1..n" Stage : has
    Stage --> "1..n" Resource : uses
    Stage --> Stage : previous_next
    Worker --> "1..n" Skill : has
    Worker --> "0..n" Tool : command
    Tool --> "0..n" Tool : command
    Tool --> "1..n" Skill : has
    Resource <|-- Cyclo
    Cyclo <|-- RM : external
    Cyclo <|-- WIP : internal
    Resource <|-- Facility_Op
    Facility_Op <|-- Tool
    Facility_Op <|-- Worker
    Resource <|-- Facility_Infra
    Facility_Infra <|-- Energy
    Facility_Infra <|-- Area
    Stage --> "1..n" Skill : requires
{{< /mermaid >}}

## Stage Resources

When the **Cyclo** is running, each **Stage** should allocate all necessary **Resources** before receiving the "green" light to be executed. The diagram below shows the allocation, execution and release states for each **Stage**.

{{< mermaid >}}
stateDiagram
    [*] --> Alloc_Resource : Cyclo is running
    Alloc_Resource --> Stage_Execution
    Stage_Execution --> Release_Resource
    Release_Resource --> [*]
    state Alloc_Resource {
        Cyclo --> RM
        Cyclo --> WIP
        RM --> available : rm_ok
        WIP --> available : wip_ok
        Facility_Infra --> Energy
        Facility_Infra --> Area
        Energy --> available : energy_ok
        Area --> available : area_ok
        Skill --> Facility_Op
        Facility_Op --> Tool
        Tool --> available : tool_skill_ok
        Facility_Op --> Worker
        Worker --> available : worker_skill_ok
    }
    state Stage_Execution {
        execution
    }
    state Release_Resource {
        release --> WIP
        WIP --> Cyclo : wip_free
        release --> Area
        Area --> Facility_Infra : area_free
        release --> Energy
        Energy --> Facility_Infra : energy_free
        release --> Tool
        Tool --> Facility_Op : tool_skill_free
        release --> Worker
        Worker --> Facility_Op : worker_skill_free
    }
{{< /mermaid >}}

### Alloc_Resources

- From the **Cyclo** may eventually come **RM** and/or the **WIP** generated at previous **Stage**.
- Global Resources are obtained from the **Facility**, like Energy and/or Shop Floor Area.
- The **Skills** indicate **Resources** to be sought in the **Facility**, like Tools and/or Workers.
- For each **Resource**, check its availability. If not available, the **Stage** must wait.
- The first time the Resource is allocated, there may be a delay due to the **Resource Initialization Time**.
- At each transformation, there may be a delay due to the **Resource Setup Time**.

### Stage Execution

- The **Stage** is executed according to the **Process** rule.
- At each **Stage** there is production, that is, something happens in the set of assets that enter a **Stage**, causing their exit in a different state.

### Release_Resources

- After execution, the allocated **Resources** should be freed to be used by other **Stages**.
- Any resulting **WIP** must be released for use in the next **Stage** of the **Cyclo**.
- Remaining allocated **Resources** should also be released to the **Facility**.

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
