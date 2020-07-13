---
author: "José Motta Lopes"
date: 2020-04-17
linktitle: Company & Planet
menu:
  main:
    parent: tutorials
#next: /posts/github-pages-blog
#prev: /posts/automated-deployments
title: Company & Planet
weight: 60
tags: [
    "how-to-change",
]
---
## The Company and the Planet

The following relationships rule the interaction between the Company and the Planet.
{{< columns >}}

## COMPANY

- The **Company** has **Investors**
- that own **Shares**
- that decide how to manage a **Facility**
- that implements a **bAmpli Circuit**
- with at least one **bAmpli**
- that handles at least one **Cyclo**
- composed by one **Stage** or more.

<--->

## PLANET

- The **Planet** is a living **System**
- populated by cooperative **Work**
- made by a **Process**
- expressed by a **bAmpli Circuit**
- with at least one **bAmpli**
- that handles at least one **Cyclo**
- composed by one **Stage** or more.

{{< /columns >}}

The following diagram clarifies the Company & Planet containerships.

![Z1 1 company-planet-2](https://user-images.githubusercontent.com/86032/81451969-0bd8d580-915c-11ea-807f-3185ef213fed.png)

The corresponding relationships are outlined below:

- The **Company** has **Investors** that are the shareholders.
- The **Investors** own **Shares** that elect **Company**'s top management.
- The **Facility** in this context is not a building!
- The **Facility** is a commitment to lend. It is like a credit card that entitles the Company to borrow on demand up to a prearranged limit at a predetermined interest rate. When the Company use the card, it creates an outstanding loan, and each additional charge is a drawdown against the Facility that increases the loan. Finally the Company pays the loan principal, and may also pay an annual fee for the privilege of having the Facility, independently of the loan. This definition is inspired by Eric Evans "Domain Driven Design" book, seen at chapter eight.
- The **Facility** designs the **bAmpli Circuit** in order to manage the **Process**.
- The **bAmpli Circuit** is an abstraction implemented by the **Company**, similar to an electronic circuit schematic that may be applied to different equipment.
- The **bAmpli Circuit** is composed of at least one **bAmpli**, or Business Amplifier.
- The **bAmpli** is responsible for at least one **Cyclo**, or Gain Machine.
- The **Cyclo** is composed of at least one **Stage**.

## Financial Indicators

Initials | Indicator | Description
--- | :--- | :---
RI | Return on Investment | At initial version, RI is returned to Investors according to their Shares. This simple rule maybe extended in future versions.
I | Investment | It is all the money that the Facility invests by buying Inventory that will be converted into sales.
NP | Net Profit | This is the Company NP, considering all the existing bAmpli Circuits inside the Facility.
PS | Product Sales | It is the cash flow received from the sale of products from each existing Cyclo inside the Facility.
RM | Raw Material | It is the cash flow that remunerate suppliers from each existing Cyclo inside the Facility.
G | Gain | This is the rate at which the system generates money through sales. Equals revenue from Product Sales minus Raw Material expenses from each Cyclo inside the Facility.
WF | Workforce | Company expenses with Labor, related to all bAmpli Circuits that exist in the Facility.
OH | Overhead | Other fixed costs of the Company, also related to all bAmpli Circuits that exist in the Facility.
OE | Operating Expense | It is all the money the system spends turning Inventory into Gain. It is the sum of the Workforce and Overhead of the Facility.

## Formulas

{{< katex >}}
\begin{aligned}
   RI&=\frac{NP}{I} \\
   NP&=(PS-RM)-(WF+OH) \\
   G&=PS-RM \\
   OE&=WF+OH \\
   NP&=G-OE \\
   RI&=\frac{G-OE}{I}
\end{aligned}
{{< /katex >}}
{{< hint info >}}
**This project is published in [Business Amplifier](https://www.amazon.com/Business-Amplifier-M-Sc-Motta-Lopes/dp/B083XGK14Q), also [e-book](https://www.amazon.com/Business-Amplifier-Jose-Motta-Lopes-ebook-dp-B086L6V6QY/dp/B086L6V6QY/) and [Amplificador de Negócios](https://www.amazon.com/M-Sc-Jose-Motta-Lopes/dp/8592301009).**
{{< /hint >}}
