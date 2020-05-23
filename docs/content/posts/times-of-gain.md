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

The **Stage** revised model shows below the **Facility** resources divided into two categories:

- **FacilityInfra**: includes infrastructure items, like Shop Floor Area, Energy, etc.
- **FacilityOp**: includes operational items with **Skills**, like Tools and Workers.

{{< mermaid >}}
classDiagram
    Planet --> "1..n" Product : populated_by
    Product --> "1..n" Process : made_by
    Process --> "1..n" Stage : composed_of
    Stage --> "1..n" Resource : uses
    Stage --> Stage : previous
    Stage --> Stage : next
    Worker --> "1..n" Skill : has_skill
    Worker --> "0..n" Tool : commands
    Tool --> "0..n" Tool : commands
    Tool --> "1..n" Skill : has_skill
    Resource <|-- Cyclo : from_cyclo
    Cyclo <|-- RM : external
    Cyclo <|-- WIP : internal
    Resource <|-- Facility : from_facility
    Facility <|-- FacilityInfra : infrastructure
    FacilityInfra <|-- Energy
    FacilityInfra <|-- Area
    Facility <|-- FacilityOp : operation
    FacilityOp <|-- Worker
    FacilityOp <|-- Tool
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
        [*] --> FacilityInfra
        [*] --> Skill
        Cyclo --> RM
        Cyclo --> WIP
        RM --> [*] : rm_ok
        WIP --> [*] : wip_ok
        FacilityInfra --> Energy
        FacilityInfra --> Area
        Energy --> [*] : energy_ok
        Area --> [*] : area_ok
        Skill --> FacilityOp
        FacilityOp --> Tool
        Tool --> [*] : tool_skill_ok
        FacilityOp --> Worker
        Worker --> [*] : worker_skill_ok
    }
    state Stage_Execution {
        execution
    }
    state Resource_Release {
        [*] --> WIP
        WIP --> Cyclo : wip_free
        [*] --> Area
        Area --> FacilityInfra : area_free
        [*] --> Energy
        Energy --> FacilityInfra : energy_free
        [*] --> Tool
        Tool --> FacilityOp : tool_skill_free
        [*] --> Worker
        Worker --> FacilityOp : worker_skill_free
    }
{{< /mermaid >}}

### Resource Allocation

- From the **Cyclo** may eventually come **RM**, and **WIP** generated at previous **Stage**.
- **Infrastructure Resources** are obtained from the **Facility**, like Energy and Shop Floor Area.
- The **Skills** indicate **Operational Resources** to be sought in the **Facility**, like Tools and Workers.
- For each required **Resource**, check its availability. If not available, the **Stage** must wait.
- At Resource allocation, there may be a delay due to the **Resource Allocation Time**.
- Before each Stage execution, there may be a delay due to the **Resource Setup Time**.

### Stage Execution

- As soon as resources are allocated and setup, the **Stage** is executed, according to rule three of Deming's **Process** specification.
- *At each **Stage** there is production, that is, something happens in the set of assets that enter a **Stage**, causing their exit in a different state*.
- The Stage execution expects to introduce a delay known as the **Stage Execution Time**.

### Resource Release

- After execution, the allocated **Resources** should be freed to be used by other **Stages**.
- Any resulting **WIP** must be released for use in the next **Stage** of the **Cyclo**.
- Remaining allocated **Resources** should be released to **FacilityInfra** and **FacilityOp**.
- At Resource release, there may be a delay due to the **Resource Release Time**.
- Some optimization may prevent **Facility** from eventual unnecessary release/reallocation, according to rule five of Deming's **Process** specification.
- *Each Stage cooperates with the next and the previous, seeking optimization*.

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

These times should be specified by the **Process**, since it defines the **Stage** sequence for the **Cyclo**. The actual amount of time each **Stage** will require at run time is ultimately defined by the **Cyclo** and **Facility** implementations. This means that all timing should be analyzed as statistical distributions, subject to variations due to **common and special causes** in the **Process**, according to **SPC** (Statistical Process Control) directives.

{{< hint info >}}
**This project is published in [Business Amplifier](https://www.amazon.com/Business-Amplifier-M-Sc-Motta-Lopes/dp/B083XGK14Q), also [e-book](https://www.amazon.com/Business-Amplifier-Jose-Motta-Lopes-ebook-dp-B086L6V6QY/dp/B086L6V6QY/) and [Amplificador de Negócios](https://www.amazon.com/M-Sc-Jose-Motta-Lopes/dp/8592301009).**
{{< /hint >}}
