---
author: Jose Montoya
title: The Problem with API-Led - Part 2
date: 2021-12-25
description: ???
tags: [ "integration", "api", "patterns" ]
categories: [ "integration" ]
---

In the first part of this series, I talked about the issues around the name "API-Led." For some time, I thought we could address this problem by clarifying further what API-Led is and isn't and proposing a different name. In fact, during our time at MS3, my friend Josh Erney (the DataWeave guru) and I collaborated to clarify what an API-Led implementation should look like. Alas, the article never came to light.

However, after years of seeing organizations struggle to implement it correctly and experience some pain even when they get it right, I realized the pattern does not fit modern organizations, even without misuse. Though it may be possible to address some of its issues, I'm not convinced it's worth the necessary effort. We should move on from it entirely.

With that said, before I try to convince you of why the pattern isn't good, we must once again define what it _is_.

<br/>

<div class="row align-items-center">
<div class="col-md-2"></div>
<div class="col-md-6"><img class="rounded img-fluid" src="https://i.imgflip.com/5ymect.jpg" alt="is this an api-led" /></div>
<div class="col-md-2"/></div>
</div>
<br/>

To do this, I've codified API-Led directly from the _API-Led Connectivity_ whitepaper by Mulesoft into the Pattern Language structure. Software professionals sure love patterns, so presenting API-Led in this format should be conducive to level-setting. Note that I've explicitly re-used the wording from the whitepaper to avoid any discussion around "my interpretation."

### API-Led in Pattern Language

**_Name_**: API-Led

**_Context_**: Digital transformation has enabled companies to engage with their stakeholders in new and innovative ways, irreversibly reshaping industry boundaries and business models. Technologies like SaaS, mobile and IoT, have dramatically increased the number of endpoints to connect to.

Organizations must stay relevant to their customers, else risk ceding market share to competitors who are able to adapt more quickly.

**_Problem_**: Ensure stability and control over core systems of record, while enabling innovation and rapid iteration of the applications that access those systems of record.

**_Solution_**: Multi-speed IT through a multi-tiered architecture with three distinct layers:

{{<table "table table-sm">}}
| Layer            | Ownership                                      | Frequency of Changes          |
|------------------|------------------------------------------------|-------------------------------|
| System Layer     | Central IT                                     | 6-12 months                   |
| Process Layer    | Central IT and Line of Business IT             | 3-6 months                    |
| Experience Layer | Line of Business IT and Application Developers | 4-8 weeks; or more frequently |
{{</table>}}

The System Layer encompasses the slower changing systems of record, APIs in this layer expose and abstract the underlying data to decouple the consumer from the system. The Process Layer encapsulates as services, the more frequently changing business processes, independent of the source systems and the target channels of engagement. The Experience Layer and its APIs reconfigure the data from the previous layers to provide a common data source for multiple channels of engagement, which change most often.

**_Resulting Context_**: Increased productivity through re-use, and agility through loose coupling of systems.

---

<br/>

Let's first dig into the mismatch between the **Solution** and the **Resulting Context**, then we'll challenge the **Problem**, which is the root of why the pattern is usually unsuccessful in the long term.

Let's assume a greenfield implementation that avoided the widespread pitfalls we see organizations trip over: equate the three-layered architecture with the State-Logic-Display (aka. Three-Tier) architectural pattern; or constantly implementing all three tiers for every single use case even if a particular component ends up being a proxy or "passthrough"; or not abstracting a system, e.g., a Salesforce API vs. a CRM API.

A simple API-Led implementation for a bank may look something like this:
<br/>
<img class="mb-3 m-auto rounded img-fluid" alt="api led example" style="display:block;" src="/images/api-led-problem-p2-colored.png"/>
<br/>

OK, so we have implemented the **Solution**, let's examine the promised **Resulting Context**: reusability and loose coupling.

In Jez Humble et al.'s  "Accelerate: Building and Scaling High Performing Technology Organizations," we have two architectural capabilities that predict high org performance: Loosely coupled architecture and Empowered teams.

While reusability is sometimes achieved through API-Led, it is not a predictor for high performance, and though it is a noble pursuit, it becomes a trade-off to speed. Gregor Hohpe puts it this way:

<figure class="mx-5">
  <blockquote class="blockquote">
    <p><em>Evolving a widely reused resource also requires coordination because changes must be compatible with all existing systems or users. Such coordination can slow down innovation... Some digital companies have even begun to explicitly favor duplication because their business environment rewards economies of speed.</em></p>
  </blockquote>
  <figcaption class="blockquote-footer">
    Gregor Hohpe in <cite title="The Architect Elevator">The Architect Elevator</cite>
  </figcaption>
</figure>

So let's talk through loose coupling, that a change to one service should not require a change to another. If the frequently changing Experience APIs only ever change by re-arranging existing data, then, sure, the layers are loosely coupled. They can deploy at their own rates. But the changes that drive an innovative company are on capabilities that span all layers! The most straightforward example would be adding a new field to a user interface.

In our bank example, let's say that we wanted to show our mobile users the last time they checked each account, which we weren't tracking before. So what does an API-Led org have to do? The stakeholders will drive the initiative and coordinate with all the engineering managers or project managers for each team involved in the change. Coordination across teams must occur to accommodate the project: what system of record should contain the new data? What will be the name of the field in the system? What will be the name in the abstracted application interface? What will it be in the layer above that one and the one above that one? What will it be in the UI? Then the actual work has to be done across layers and the UI. Sometime later, when the stakeholders want to know the progress of the change, no one knows; all teams must be interrogated to know each of their progress and compose a report.

Because of the necessary coordination between many teams going through the actual implementation, the un-escapable change in requirements, testing, and integration testing, a simple change like this can take months to get to production, especially if the teams are working on multiple initiatives at once. I've experienced this. You've experienced this.

Digital companies ~~do not~~ _can not_, take months to add a field to some UI.

In our bank API-Led architecture, we didn't define what those underlying systems of record were. Let's say that for our CRM, we used Salesforce. In your experience, does Salesforce change only every 6-12 months? Nope. It usually changes as fast or faster than any Experience API! All of the frequent changes in Salesforce that impact our Web & Mobile API will affect all layers, with all the lead-time associated before delivering that value to our customers.

I've wanted to write this article for a year, maybe two, and since sharing Part 1, I've been shown similar ones by colleagues that have similar opinions, but we're super late; ThoughtWorks realized this in 2018(!!!):

<figure class="mx-5">
  <blockquote class="blockquote">
    <p><em>... organizations who've adopted a layered microservices architecture, which in some ways is a contradiction in terms... have fallen back to arranging services primarily according to a technical role [like those in API-Led]... delivering any valuable business change requires slow and expensive coordination between multiple teams.</em></p>
  </blockquote>
  <figcaption class="blockquote-footer">
    ThoughtWorks <cite title="Technology Radar">Technology Radar 2018</cite>
  </figcaption>
</figure>

<br/>
<div class="row align-items-center">
<div class="col-md-2"></div>
<div class="col-md-6"><img class="rounded img-fluid" src="https://i.imgflip.com/5yzu93.jpg" alt="hey guys" /></div>
<div class="col-md-2"/></div>
</div>
<br/>

The problem with API-Led is that the **Problem** is inaccurate. The dichotomy between slow and stable, and fast and less-critical no longer holds. Gregor Hohpe (you know, the guy that wrote the book on Enterprise Integration) expressed this way:

<figure class="mx-5">
  <blockquote class="blockquote">
    <p><em>... the separation between systems of engagement and systems of record is artificial and doesn’t line up well with the overall rate of change from a business or end-user perspective ... hardly any digital business follows such a setup. Digital companies only know one speed: fast.</em></p>
  </blockquote>
  <figcaption class="blockquote-footer">
    Gregor Hohpe in <cite title="The Architect Elevator">The Architect Elevator</cite>
  </figcaption>
</figure>

<br/>
<div class="row align-items-center">
<div class="col-md-2"></div>
<div class="col-md-6"><img class="rounded img-fluid" src="https://i.kym-cdn.com/photos/images/newsfeed/001/142/233/897.gif" alt="now what" /></div>
<div class="col-md-2"/></div>
</div>
<br/>

Let's now introduce a better approach: we want to find the team-bound, _vertical_ fracture planes of the solution space. There are a few different ways to find the appropriate fracture planes for a given organization, the main one being the business domain bounded contexts, or what Sam Newman calls "Just Enough Domain Driven Design."

A superficial attempt at our bank example may result in something like this:

<br/>
<img class="mb-3 m-auto rounded img-fluid" alt="api led alternative" style="display:block;" src="/images/api-led-problem-p2-alternative.png"/>
<br/>

There's a lot to unpack in this depiction, but there are a couple of specific things I want to call out:

* We're moving away from an outdated understanding of IT where things are thrown over the wall in stages like an assembly line, where an isolated "Central IT" only manages systems of record, towards a post-industrial understanding that IT is the leading enabler in digital organizations and must drive and co-create value. Read _Designing Delivery_ by Jeff Sussna.

* Instead of changes spanning multiple teams, requiring coordination and lacking visibility in delivery, the vertical fracture planes help us assign stream-aligned teams:
<figure class="mx-5">
  <blockquote class="blockquote">
    <p><em>... a team aligned to a single, valuable stream of work... the team is empowered to build and deliver customer or user value as quickly, safely, and independently as possible, without requiring hand-offs to other teams...</em></p>
  </blockquote>
  <figcaption class="blockquote-footer">
    Matthew Skelton and Manuel Pais in <cite title="Team Topologies">Team Topologies</cite>
  </figcaption>
</figure>

* A team-first organization through team-bound services will maximize their abilities by focusing their efforts and therefore the org's own ability to deliver value to their customers:
<figure class="mx-5">
  <blockquote class="blockquote">
    <p><em>... there is an effective upper limit on the cognitive load that a single team can bear... The team needs to own the system or subsystems they are responsible for. Teams working on multiple codebases lack ownership and, especially, the mental space to understand and keep the corresponding systems healthy.</em></p>
  </blockquote>
  <figcaption class="blockquote-footer">
    Matthew Skelton and Manuel Pais in <cite title="Team Topologies">Team Topologies</cite>
  </figcaption>
</figure>

For an in-depth understanding of this approach, I'd recommend _Team Topologies_ by Matthew Skelton and Manuel Pais, and How to Model Microservices from _Building Microservices 2nd Edition_ by Sam Newman.

---

Further reading:
* _Designing Delivery_ by Jeff Sussna
* _Accelerate: Building and Scaling High Performing Technology Organizations_ by Jez Humble et al.
* [_You Can't Buy Integration_](https://martinfowler.com/articles/cant-buy-integration.html) by Brandon Byars
