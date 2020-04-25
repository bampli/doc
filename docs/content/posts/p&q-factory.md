---
author: "José Motta Lopes"
date: 2020-04-20
linktitle: P&Q Factory
menu:
  main:
    parent: tutorials
#next: /posts/github-pages-blog
#prev: /posts/automated-deployments
title: P&Q Factory
weight: 70
tags: [
    "to-what-to-change",
]
---

This is the **Process** used as a sample when a process is needed in this project.

The P&Q Factory gives no room for apology and demonstrates how the "Theory of Constraints" can help managers with their decision-making logic. The fictional factory portfolio has products P & Q.

## P&Q Factory

Using TPM to describe the P&Q Factory, there is little reason to blame poor corporate results:

- **ati = 1** Equipment runs nonstop for the working time, available time index is 1.
- **oti = 1** There is no break in the operation, operating time index is 1.
- **opi = 1** There is no speed loss, operational performance index is 1.
- **zti = 1** There are no defective products, then zero defect index is 1.
- **gpi = 1** Multiply above indexes to get the P&Q global performance index of 1.

Using the week as a unit, the factory's working time is 2,400 minutes per week. Due to unitary **gpi**, this time is all used in the process to manufacture P and Q at the highest quality and speed possible. More details about the P&Q Factory that make life easier to investors and managers:

- **Sales**: There is no difficulty in moving the P&Q products because the market
has potential to buy up to 100 pieces of P and 50 pieces of Q per week.
- **Prices**: The unit prices are preset at $90 for P and $100 for Q. If production exceeds market volume limits, the products become stranded.
- **Operating Expenses**: There are no surprises for fixed costs, since Operating Expenses are immutable $6,000 per week, including Workforce and Overhead.
- **Raw Materials**: The raw materials used in the process are P-Part, RM1, RM2, and RM3, at costs respectively of $5, $20, $20 and $20, with no surprises.
- **Workforce**: The P&Q Factory has four workers with different **skills**: A, B, C, and D. They are absolutely perfect workers during all the working time. No delays, no errors.

## P&Q Process

The engineering of the P&Q Factory presents the *manufacturing* process in the following diagram, showing the production flows that result in P and Q. These flows could also be applied to other *environments* where **resources** are used for **tasks** that require **skills**, to achieve a **goal**.

{{< mermaid >}}
graph LR
    PP[P-Part $5/u] --> D1[D 15min/u] --> P[P $90/u 100u/wk]
    RM1[RM1 $20/u] --> A1[A 15min/u] --> C1[C 10min/u] --> D1
    RM2[RM2 $20/u] --> B2[B 15min/u] --> C2[C 5min/u] --> D1
    C2 --> D2[D]
    RM3[RM3 $20/u] --> A3[A 10min/u] --> B3[B 15min/u] --> D2[D 5min/u] --> Q[Q $100/U 50u/wk]
{{< /mermaid >}}

{{< katex >}}
\begin{gathered}
   wk&=2400\,min \qquad
   OE&=\$6000/wk
\end{gathered}
{{< /katex >}}

As seen at the top of the diagram, RM1 is processed by A for 15 minutes, then C processes it for 10 minutes. It is finished by D that assembles product P using the purchased P-Part.

The middle flow starts with RM2 being processed by B for 15 minutes, continue to C workstation for 5 minutes and may reach both assembly tasks done by D. This central flow is used in both P and Q fabrication. To manufacture one of each, it is necessary to process RM2 twice by B and C.

Lastly, RM3 spends 10 minutes being processed by A, then is processed for 15 minutes by B and goes to Q assembly workstation. D assembles P and Q in respectively 15 and 5 minutes.

## What is the net profit of the P&Q Factory?

What is the maximum net profit that P&Q Factory can earn per week? Think about the time each stage has for producing P&Q. This exercise is solved in the books "The Haystack Syndrome" and [Business Amplifier](https://www.amazon.com/Business-Amplifier-M-Sc-Motta-Lopes/dp/B083XGK14Q).

{{< hint info >}}
**This project is published in [Business Amplifier](https://www.amazon.com/Business-Amplifier-M-Sc-Motta-Lopes/dp/B083XGK14Q), also [e-book](https://www.amazon.com/Business-Amplifier-Jose-Motta-Lopes-ebook-dp-B086L6V6QY/dp/B086L6V6QY/) and [Amplificador de Negócios](https://www.amazon.com/M-Sc-Jose-Motta-Lopes/dp/8592301009).**
{{< /hint >}}
