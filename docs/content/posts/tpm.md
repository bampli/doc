---
author: "José Motta Lopes"
date: 2020-04-16
linktitle: "TPM: Total Productive Maintenance"
menu:
  main:
    parent: tutorials
#next: /posts/github-pages-blog
#prev: /posts/automated-deployments
title: "TPM: Total Productive Maintenance"
weight: 40
tags: [
    "to-what-to-change",
]
---
TPM consists of a systematic program for enterprise development that addresses maintenance by optimizing equipment effectiveness. TPM consolidates failures and waste into a creative approach, using **time** as a common link.

Thus, Working Time is defined as the total journey time that company works. From then on, we will be discounting the time spent on failures and waste, creating indexes that will selectively signal machine and equipment performance problems, operation failures and product defects.

![50 2 1 TPM 2 ref small](https://user-images.githubusercontent.com/86032/79464036-f5fa4980-7fcf-11ea-891b-5e7adc758e20.png)

## Available Time Index (ati)

Given the Working Time, extract the Downtime, which is the time that machines or equipment failed, preventing production from occur. The remaining time, i.e. when the machines and equipment are running, is called Available Time. See in the following diagram that the available time index (ati) equals the Available Time divided by Working Time.

![50 2 2 tempodisponivel](https://user-images.githubusercontent.com/86032/79464045-f8f53a00-7fcf-11ea-97f1-ba420a15e555.png)

## Operating Time Index (oti)

From Available Time is now subtracted the production Breakdown Time, which represents operational waste, staff shortages or operational failure. The remaining time is called Operating Time. The operating time index (oti) is obtained by dividing the Operating Time by the Available Time.

![50 2 3 tempo operacional 2](https://user-images.githubusercontent.com/86032/79464056-fd215780-7fcf-11ea-845d-b03402a64573.png)

## Operational Performance Index (opi) 

Operating Speed indicates how close the process has come to the theoretical production cycle. See that the effective cycle is calculated by dividing Productive Time by the number of products produced. Then, the theoretical cycle is divided by the effective cycle to obtain the Operating Speed index (osi).

![50 2 4 velocidade operacional 2](https://user-images.githubusercontent.com/86032/79464071-01e60b80-7fd0-11ea-8645-0f4cd160ff56.png)

In calculating the Operational Performance Index (opi) below, the Productive Time Index is multiplied by the Operating Speed. In the numerator the Productive Time is replaced by the total quantity of products multiplied by the effective cycle. With this, we extract from Operating Time the loss of operational speed of production. The remaining time is called Productive Time.

![50 2 5 performance operacional 2](https://user-images.githubusercontent.com/86032/79464079-04e0fc00-7fd0-11ea-801d-4d8add8063b7.png)

## Zero Defect Index (zti)

Considering the product quality, the Productive Time is deducted from the time spent reworking defective products, creating the Zero Defect Time (zti) index. At this time, the production system worked fully, with no downtime, breakdowns, defects, or rework to fix them.

![50 2 7 quality](https://user-images.githubusercontent.com/86032/79464099-0ad6dd00-7fd0-11ea-901d-b8a5f9feec2d.png)

## Global Performance Index (gpi)

Finally, the company's Global Performance is achieved by multiplying the four indices of Available Time, Operating Time, Operating Performance and Zero Defect. Here's the equation that results in the Global Performance Index (gpi).

{{< katex >}}
\begin{aligned}
   gpi&=ati * oti * opi * zti
\end{aligned}
{{< /katex >}}

Following is a summary of the TPM indices:

- **Available Time Index (ati)** : Equivalent to Available Time divided by Working Time, that is, the amount of time that machines and equipment do not fail and production can occur.
- **Operating Time Index (oti)** : Equals Operating Time divided by Available Time. Considers the portion of time without a breakdown in production, due to lack of personnel or failure in operation.
- **Operational Performance Index (opi)** : This is equivalent to the multiplication of Operating Speed by the Production Time Index, reflecting the production operational speed losses.
- **Zero Defect Index (zti)** : Equivalent to Zero Defect Time, which produced only perfect products, divided by Productive Time, ie represents the portion of time free from rework on defective products.
- **Global Performance Index (gpi)** : This is the multiplication of the four indices above, corresponding to the overall performance, considering the problems caused by eventual failures and waste to which the Process is subject.

The company's overall performance index has intermediate indices that provide a selective and detailed analysis of the sources of problems. Masterfully, TPM has turned time into a decision support tool that brings together concepts as diverse as stopping machines, wasted labor, and faulty parts.

## Production Counters

For clarification of the formulas, follows the graphical representation of the production counters, including the total of products produced and those that were effectively dispatched. The Process produces **np** products, of which **nz** are free of defects, and **nw** does need rework. Of the latter, **nr** products are recovered and added to **nz**, resulting in **nd** dispatches. The **ns** unrepaired products are recycled as scratch.

![50 2 6 counters](https://user-images.githubusercontent.com/86032/79464086-07dbec80-7fd0-11ea-99a7-8d503a87454f.png)

{{< hint info >}}
**This project is published in [Business Amplifier](https://www.amazon.com/Business-Amplifier-M-Sc-Motta-Lopes/dp/B083XGK14Q), also [e-book](https://www.amazon.com/Business-Amplifier-Jose-Motta-Lopes-ebook-dp-B086L6V6QY/dp/B086L6V6QY/) and [Amplificador de Negócios](https://www.amazon.com/M-Sc-Jose-Motta-Lopes/dp/8592301009).**
{{< /hint >}}
