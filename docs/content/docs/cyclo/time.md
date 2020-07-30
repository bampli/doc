---
title: Times of Gain
weight: 5
bookToc: false
---
# Times of Gain

The following rules add more details to the **Process** specification:

- Connected as a **Cyclo**, the **Process** is specified by the timing of its **Stages**.
- **Stages** consumes **Resources**, both from **Facility** and from **Cyclo**.
- The **Stage** allocates **Resources** from the **Facility** to accomplish its task.
- Every **Stage** requires **Skills** to accomplish its task.
- The **Skill** is provided by a combination of **Workers** and/or **Tools**.
- The **Stage** also allocates **Resources** from the **Cyclo** to accomplish its task.
- The **Cyclo** supports **RM** and **WIP** flows through the **Stages**.

## Stage Model

The **Stage** model, shown below, allocates **Facility** resources divided into two categories:

- **FacilityInfra**: includes infrastructure items, like Shop Floor Area, Energy, etc.
- **FacilityOp**: includes operational items with **Skills**, like Tools and Workers.

{{< mermaid >}}
classDiagram
    Planet --> "1..n" Product : populated_by
    Product --> "1..n" Process : made_by
    Process --> "1..n" Stage : composed_of
    Stage --> "1..n" Resource : allocates
    Stage --> Stage : previous_next
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

## Resources

When the **Cyclo** is running, each **Stage** should allocate all required **Resources** before receiving the "green" light to be executed. The diagram below shows the allocation, execution and release phases for each **Stage**.

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

- From the **Cyclo** may eventually come **RM** and/or **WIP** generated previously.
- **Infrastructure** are **Resources** supported by the **Facility**, like Energy and Shop Floor Area.
- The **Skills** indicate **Operational Resources** to be sought in the **Facility**, like Tools and Workers.
- For each required **Resource**, check its availability. If not available, the **Stage** must wait.
- At **Resource** allocation phase, there may be a delay due to the **Resource Allocation Time**.
- Before each **Stage** execution, there may be a delay due to the **Stage Setup Time**.

### Stage Execution

- **Stages** execute transformations according to Deming's **Process** specification: *At each **Stage** there is production, that is, something happens in the set of assets that enter a **Stage**, causing their exit in a different state*.
- The Stage execution expects to introduce a delay known as the **Stage Execution Time**.

### Resource Release

- After execution, allocated **Resources** are freed, and become available for other **Stages**.
- Any resulting **WIP** must be released for the next **Stage** of the **Cyclo**.
- **Resources** allocated from the Facility should be released to **FacilityInfra** and **FacilityOp**.
- At **Resource** release phase, there may be a delay due to the **Resource Release Time**.

Some optimization may prevent **Facility** from eventual unnecessary release/reallocation, according to rule five of Deming's **Process** specification: *Each Stage cooperates with the next and the previous, seeking optimization*.

## Stage Timing
 
The **Stage** timing includes allocation, setup, execution and release phases, as shown below.

{{< mermaid >}}
sequenceDiagram
    autonumber
    rect rgb(255, 0, 255, .3)
        Alloc-->>Setup: Resource Allocation Time
    end
    rect rgb(255, 255, 0, .3)
        Setup-->>Execution: Stage Setup Time
    end
    rect rgb(0, 255, 0, .3)
        Execution->>Release: Stage Execution Time
    end
    rect rgb(255, 0, 255, .3)
        Release-->>Free: Resource Release Time
    end
    rect rgb(0, 0, 255, .3)
        Alloc->>Free: Stage Total Time
    end
{{< /mermaid >}}

The actual amount of time each **Stage** will require at run time is ultimately defined by the **Cyclo** and **Facility** implementations. All timing should be analyzed as **statistical distributions**, subject to variations due to existing **common** and **special causes** in the **Process**, according to **SPC** (Statistical Process Control) and [TPM](/docs/posts/tpm/) (Total Productive Manintenance) directives.

{{< hint info >}}
**This project is published in [Business Amplifier](https://www.amazon.com/Business-Amplifier-M-Sc-Motta-Lopes/dp/B083XGK14Q), also [e-book](https://www.amazon.com/Business-Amplifier-Jose-Motta-Lopes-ebook-dp-B086L6V6QY/dp/B086L6V6QY/) and [Amplificador de Negócios](https://www.amazon.com/M-Sc-Jose-Motta-Lopes/dp/8592301009).**
{{< /hint >}}
