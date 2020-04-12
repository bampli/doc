# 4th Level of Menu

## Caesorum illa tu sentit micat vestes papyriferi

The engineering of the P&Q Factory presents the manufacturing process in
the following diagram, showing the production flows that result in P and Q.
As shown in the lowest left side of the diagram, RM1 raw material enters Step
A, takes 15 minutes processing, then goes to Step C for 10 minutes and ends
in Step D, which assembles product P.

Another flow starts with RM2 being processed in Step B for 15 minutes,
continuing to Step C for a further 5 minutes and reaching P and Q assembly
steps D. The central flow is used in both P and Q fabrication. To manufacture
one of each, it is necessary to process RM2 twice through B and C.

Lastly, RM3 spends 10 minutes in Step A, then is processed for 15 minutes in
Step B and goes to Q mounting at Step D. P&Q mounting Steps D are
processed in respectively 15 and 5 minutes.


{{< mermaid >}}
graph LR
    PP --> D1[D] --> P[P $90/u]
    RM1 --> A1[A] --> C1[C] --> D1
    RM2 --> B2[B] --> C2[C] --> D1
    C2 --> D2[D]
    RM3 --> A3[A] --> B3[B] --> D2 --> Q[Q $100/U]
{{< /mermaid >}}
