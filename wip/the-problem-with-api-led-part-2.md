---
author: Jose Montoya
title: The Problem with API-Led - Part 2
date: 2021-12-23
description: ???
tags: [ "integration", "api", "patterns" ]
categories: [ "integration" ]
---

In the first part of this series I talked about the issues around the unusable name of "API-Led". For some time I thought that we could address this problem with either clarifying exactly what API-Led is and isn't and/or proposing a better name. In fact, during our time at MS3 my friend Josh Erney (the DataWeave guru) and I collaborated on such an effort of clarifying what an API-Led implementation should look like. Alas the article never came to light.

Today I'm convinced the pattern as designed, even without misuse, is just not a very good one. Though it may be possible to address its issues, it's not worth the necessary effort. We should just move on from it entirely.

With that said, before I try to convince you of why the pattern isn't good we must, once again, agree on what it _is_.

<br/>
<p align="center">
<img src="https://i.imgflip.com/5ymect.jpg" alt="is this an api led" />
</p>
<br/>

In order to do this I've codified API-Led directly from the _API-Led Connectivity_ whitepaper by Mulesoft into the Pattern Language structure. Software professionals sure love patterns so presenting the pattern in this format should be conducive to level-setting. Note that I've put some effort in explicitly re-using the wording from the whitepaper in order to avoid any discussion around "my interpretation".

### API-Led in Pattern Language

**_Name_**: API-Led

**_Context_**: Digital transformation has enabled companies to engage with their stakeholders in new and innovative ways, irreversibly reshaping industry boundaries and business models. Technologies like SaaS, mobile and IoT, have dramatically increased the number of endpoints to connect to.

Organizations must stay relevant to their customers, else risk ceding market share to competitors who are able to adapt more quickly.

**_Problem_**: Ensure stability and control over core systems of record, while enabling innovation and rapid iteration of the applications that access those systems of record.

**_Solution_**: Two-speed IT through a multi-tiered architecture with three distinct layers:

{{<table "table table-sm">}}
| Layer            | Ownership                                      | Frequency of Changes          |
|------------------|------------------------------------------------|-------------------------------|
| System Layer     | Central IT                                     | 6-12 months                   |
| Process Layer    | Central IT and Line of Business IT             | 3-6 months                    |
| Experience Layer | Line of Business IT and Application Developers | 4-8 weeks; or more frequently |
{{</table>}}

The System Layer encompasses the slower changing systems of record, APIs in this layer expose and abstract the underlying data to decouple the consumer from the system. The Process Layer encapsulates as services the more frequently changing business processes, independent of the source systems and the target channels of engagement. The Experience Layer and its APIs reconfigure the data from the previous layers to provide a common data source for multiple channels of engagement, which change most often.

**_Resulting Context_**: Increased productivity through re-use, and agility through loose coupling of systems.

---

Let's first dig into the mismatch between the Solution and the Resulting Context, then we'll challenge the Problem which is the root of why the pattern usually unsuccessful in the long term.
