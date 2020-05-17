---
author: "José Motta Lopes"
date: 2020-05-17
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

The **Stage** model shows below the **Facility** resources divided into two categories:

- **Facil_Infra**: includes infrastructure items, like Shop Floor Area, Energy, etc.
- **Facil_Op**: includes operational items with **Skills**, like Tools and Workers.

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
    Resource <|-- Facility
    Facility <|-- Facil_Infra
    Facil_Infra <|-- Energy
    Facil_Infra <|-- Area
    Facility <|-- Facil_Op
    Facil_Op <|-- Worker
    Facil_Op <|-- Tool
    Stage --> "1..n" Skill : requires
{{< /mermaid >}}

## Stage Resources

When the **Cyclo** is running, each **Stage** should allocate all necessary **Resources** before receiving the "green" light to be executed. The diagram below shows the allocation, execution and release states for each **Stage**.

{{< mermaid >}}
stateDiagram
    [*] --> Resource_Allocation : Cyclo is running
    Resource_Allocation --> Stage_Execution
    Stage_Execution --> Resource_Release
    Resource_Release --> [*]
    state Resource_Allocation {
        [*] --> Cyclo
        [*] --> Facil_Infra
        [*] --> Skill
        Cyclo --> RM
        Cyclo --> WIP
        RM --> [*] : rm_ok
        WIP --> [*] : wip_ok
        Facil_Infra --> Energy
        Facil_Infra --> Area
        Energy --> [*] : energy_ok
        Area --> [*] : area_ok
        Skill --> Facil_Op
        Facil_Op --> Tool
        Tool --> [*] : tool_skill_ok
        Facil_Op --> Worker
        Worker --> [*] : worker_skill_ok
    }
    state Stage_Execution {
        execution
    }
    state Resource_Release {
        [*] --> WIP
        WIP --> Cyclo : wip_free
        [*] --> Area
        Area --> Facil_Infra : area_free
        [*] --> Energy
        Energy --> Facil_Infra : energy_free
        [*] --> Tool
        Tool --> Facil_Op : tool_skill_free
        [*] --> Worker
        Worker --> Facil_Op : worker_skill_free
    }
{{< /mermaid >}}

### Resource_Allocations

- From the **Cyclo** may eventually come **RM** and **WIP** generated at previous **Stage**.
- **Infrastructure Resources** are obtained from the **Facility**, like Energy and Shop Floor Area.
- The **Skills** indicate **Operational Resources** to be sought in the **Facility**, like Tools and Workers.
- For each **Resource**, check its availability. If not available, the **Stage** must wait.
- At Resource allocation, there may be a delay due to the **Resource Allocation Time**.
- Before each Stage execution, there may be a delay due to the **Resource Setup Time**.

### Stage Execution

- As soon as resources are allocated, the **Stage** is executed according to the **Process** specification.
- At each **Stage** there is production, that is, something happens in the set of assets that enter a **Stage**, causing their exit in a different state.
- The Stage execution expects to introduce a delay known as the **Stage Execution Time**.

### Resource_Releases

- After execution, the allocated **Resources** should be freed to be used by other **Stages**.
- Any resulting **WIP** must be released for use in the next **Stage** of the **Cyclo**.
- Remaining allocated **Resources** should also be released to the **Facility**.
- At Resource release, there may be a delay due to the **Resource Release Time**.

## Stage Timing
 
The timing during the Resource allocation, execution and release is shown below.

{{< mermaid >}}
sequenceDiagram
    autonumber
    rect rgb(0, 0, 255, .3)
        Alloc-->>Setup: Resource Allocation Time
    end
    rect rgb(0, 0, 255, .3)
        Setup-->>Execution: Resource Setup Time
    end
    rect rgb(0, 255, 0, .3)
        Execution->>Release: Stage Execution Time
    end
    rect rgb(0, 0, 255, .3)
        Release-->>Free: Resource Release Time
    end
    rect rgb(255, 0, 255, .3)
        Alloc->>Free: Stage Total Time
    end
{{< /mermaid >}}

These times are originally specified by the **Process**, since it defines the **Stage** sequence for the **Cyclo**. But the amount of time each step will require at run time is ultimately defined by the **Cyclo** and **Facility** implementation.

{{< hint info >}}
**This project is published in [Business Amplifier](https://www.amazon.com/Business-Amplifier-M-Sc-Motta-Lopes/dp/B083XGK14Q), also [e-book](https://www.amazon.com/Business-Amplifier-Jose-Motta-Lopes-ebook-dp-B086L6V6QY/dp/B086L6V6QY/) and [Amplificador de Negócios](https://www.amazon.com/M-Sc-Jose-Motta-Lopes/dp/8592301009).**
{{< /hint >}}
