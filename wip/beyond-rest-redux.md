---
author: "Jose Montoya"
title: "Beyond REST redux"
date: "2018-02-16"
description: "A case for today's architects"
tags: ["rest"]
---

> _We’re implementing REST, but it is introducing problems we didn’t have before. So, what’s the point?_

I blurted out a couple of thoughts on how they must be doing REST wrong, and when their responses involving implementation went over my head, I rambled about buzzwords, industry inertia and other things, but not in any coherent sentences. I quickly realized I had no idea what I was talking about and have since spent a lot of time trying to educate myself on the popular architecture.

After reviewing a multitude of sometimes contradicting sources, I felt I had a passable grasp of what REST is and what it looks like in practice, but I still didn’t know what the point was. It wasn’t until I dug into its document of origin and related works that it all clicked. Finally, I came away with an understanding of something more important than REST itself.  What follows is an attempt to document (and sometimes ramble about) the journey, the reasons it took me where it did, and what could have been different, in hopes that it will help others and perhaps spark some engaging conversations about what we can do better as an industry.

### It’s Difficult to get REST

REST is defined in the dissertation document, Architectural Styles and the Design of Network-based Software Architectures, as a requirement for a Doctorate of Philosophy in Information and Computer Science. That’s right, there is a doctorate program for Philosophy in Computer Science. If the work was simple to produce there would be no reason for the University of California, Irvine to honor Dr. Fielding with his prefix; it is a difficult field full of highly qualified academics.

The people that are in the best position to write articles and make videos explaining it are the ones that spent their time reading and interpreting that dissertation and its sources directly. Often these are technical people too, eager to share the technical details that make REST unique, but who often miss the chance to present the practical purpose they were designed to serve. That purpose should be front and center.

> _Architecture is about intent, we’ve made it about frameworks and details_ – Robert C. Martin

There are also companies using REST as a marketing and sales tool. That’s not necessarily wrong, but under that setting the priority is to present aspects of the architecture only as they make their product or services more attractive.

We need a more accessible and objective description of REST.

### Architectural Styles and the Design of…. [for the rest of us]

The Web had been in development for some time but lacked a model to guide its design and implementation. In order to arrive at such a model, Dr. Fielding was motivated to create a framework for identifying and evaluating the use of architectural constraints to satisfy functional, performance, and social properties of a network-based architecture. REST is the product of using such a framework to derive the model for the Web.

I like to think of the dissertation as being a two-part document, and here is a gross oversimplification:

#### A Framework for Evaluating the Design of Application Architectures

Dr. Fielding identifies what properties a networked system could possibly exhibit: performance, scalability, simplicity, modifiability, visibility, portability, and reliability. These are some of the functional, performance, and social properties of any software system and what I refer to whenever I use the term properties throughout the remainder of this document.

Next, guided by the application of software principles, he classifies an array of architectural styles by the properties they induce, e.g. the client-server style applies the separation of concerns principle to achieve simplicity; this is sometimes referred to as Principled Design. I will not detail all the identified styles as the list is long and they’re overtly technical by nature which goes against the spirit of this article.

#### Designing the Web's Architecture

Armed with the framework above, Dr. Fielding first identifies how the Web should behave: it should be simple, modifiable, and scalable. Then he starts building an architecture, starting from scratch and layering styles as they supply the properties needed. Finally, Dr. Fielding presents a set of styles that when combined result in a system that satisfies the requirements for the Web, REpresentational State Transfer (REST).

REST is strictly defined by that set of style constraints, but the key point is the properties those constraints serve:

Client-server style adds simplicity, scalability, and evolvability
Stateless style adds scalability but reduces network performance
Caching style adds simplicity and scalability
Uniform interface style adds evolvability but reduces network performance
Layered system style adds scalability and evolvability

Applying REST will result in a system that is highly simple, evolvable, and scalable just as required by the use case that is the Web, an Internet-scale, multi-organization, anarchically scalable information system. But a system that’s not very network performant, and average or just above average at every other property.

### No Silver Bullets

What makes REST so popular is that it’s a well informed and documented architecture for what is unarguably the greatest networked application of all, the Web. It has come to be considered the ideal choice for all networked applications. If you’re familiar with microservices, networked APIs, or application networks, you know how it is prescribed, and it makes sense; if it worked for the World Wide Web it should work for you.

But what if you cannot sacrifice network performance for your specific use case? If that’s your priority then you must make different trade-offs. What if you have the perfect solution on paper but in practice the effort required behind one style choice implementation outweighs its benefit to your use case? Then you must make different trade-offs.

There is no silver bullet in software design, and the subject matter experts on the current popular industry practices warned us:

… your team and management will have to determine if a system … deserves the cost of [Domain Driven Design]
– Vaughn Vernon, Implementing Domain Driven Design

Every company, organization, and system is different. A number of factors will play into whether or not microservices are right for you…
– Sam Newman, Building Microservices

Almost all modern applications can … run successfully … on a serverless platform. However, there are a few times [it] is not the best choice…
– Amazon Web Services, Optimizing Enterprise Economics with Serverless Architectures

And most relevant,

My dissertation is about Principled Design, not the one true architecture.
–Dr. Roy Fielding, A little REST and Relaxation

Yet the industry is quick to blindly prescribe REST and it’s because even though the work is admittedly about Principled Design, that’s not a buzzworthy term.

### Design by Buzzword

Fashionable jargon is not exclusive to the software industry but rather it’s a common occurrence across many different fields because it’s a sales and marketing tool. There’s nothing inherently wrong with arming our business teams with as many tools as we can, after all we may not have a job if it wasn’t for them.

The problems surface when we take these ideas at their buzzword face value and use them to make technical decisions. In the process of becoming fashionable, the original purpose behind these ideas takes second place and the trade-offs made have no place at all. Most people are aware that REST is highly scalable, but not that it’s not very network performant for example. When we forget there are no silver bullets, and don’t dig deeper to learn the trade-offs behind them, we risk making uninformed decisions.

Consequently, details and frameworks become the source of active debate as Robert C Martin pointed out. We’re trying to satisfy different requirements with the same “universal” idea. When we don’t understand the purpose behind the technical constraints of an architecture we risk making compromises and misjudging the results for not exhibiting the properties we expected.

As a side note, I do consider the current industry implementations of “REST” to be misguided. While we do have an architecture that better serves our circumstances, I believe it is a disservice to call it that. I can imagine the eye rolls from some readers already. However, this is something more technically oriented and that I’ll try to tackle on another occasion.

That’s how we end up with questions like “What’s the point of REST?” halfway through an implementation or with the many debates on “what a RESTful service should look like” when the architecture is purposely constraining. This can be a costly mistake with a considerable amount of time and money spent on an inadequate solution.

These problems are not particularly special to software development but it is the common risk of making decisions on incomplete information. Yet it seems its effect in our industry is much more pronounced. Ironically, Dr. Fielding acknowledged this problem in his dissertation, yet couldn’t avoid it.

… [often] software projects begin with adoption of the latest fad… and only later discover whether… system requirements call for such an architecture. Design-by-buzzword is a common occurrence
–Dr. Roy Fielding, Architectural Styles and the Design of Network-based Software Architectures

The overreliance on buzzwords in software, more than other fields, can be attributed to the fact that ours is one that has been evolving much faster than it can mature. Not only have we not met the demand for qualified professionals, we have yet to formalize a process for classifying and qualifying them. Which is why we rely on experience instead, but is it the same? More importantly, there’s a lack of general awareness of the risks behind uninformed designs. Do we know the cost, in a dollar amount, behind choosing a microservices architecture just because it is used at Netflix? In contrast, in established fields like civil and architectural engineering there are widely recognized credentials. While experience is still important, you can count on any accredited engineer to design a sound structure, there’s not a number of years of experience that equates. Moreover, the risks behind an unqualified building design seem obvious, but can certainly be studied and quantified, and when money comes into play customers will be motivated to find the appropriate resource. While I don’t presume that software and these fields hold the same weight, the point is there are things we’re yet to figure out.

This presents a challenge for any business to identify and procure the resources qualified to make software decisions and to see the incentives behind doing so. As we fill those gaps, decisions will continue to rely on industry marketing to give us the latest and greatest and then further popularize it by adoption; a self-fulfilling industry inertia.

Buzzwords will not be going anywhere anytime soon, even if we wanted them to. What we can do is acknowledge it and try to better understand the role of an expert in an effort to identify ways in which we can enable today’s decision makers to avoid their pitfalls.

### An Architect’s Job

It is the responsibility of the software architect to have a complete understanding of relevant concepts, platforms, tools, and industry standard practices; no small task. It is also their responsibility to stay up to date with new ideas by acknowledging the nature of buzzwords and educating themselves on their underlying purpose and tradeoffs.

Not only must an architect master technical knowledge in order to be universally valuable, they must also have the business awareness to first probe and discover the functional, performance, and social properties of the system to be built. Only then, guided by these goals, they must consider all the tools at their disposal to make informed design choices to satisfy those requirements. This is why Dr. Fielding’s showcase of Principled Design is far more useful to an architect than the result itself.

An architect must also recognize that they don’t operate in a strictly academic field and concede when practical compromises should be made in the face of external circumstances, usually in the form of time or money constraints. While the results of these compromises may result in a less than ideal design, it is different than uninformed design. There are conscious decisions made on the interest of the business. That’s why we should also beware of engaging architects from companies with vested interest in REST or any other buzzworthy product to design our systems, as they may propose a solution without genuinely considering the particular needs of the business, plus the added risks of vendor lock-in. Because,

if all you have is a hammer, everything looks like a nail
– Law of the Instrument

It then becomes imperative not only to count on qualified experts, but to ensure that they are trusted to put the interest of the business first when making these choices. Having someone technically inclined in management could be advantageous here as it makes it easier to communicate the merits of a design choice and gain their trust. They may even become an allied technical advocate. Conversely, whether there is someone technically inclined or not, if an architect does not gain the trust of management they may be inclined to make or influence the architect’s choices, where all the same risks of uninformed designs apply.

In the years that I’ve been defining and implementing networked APIs with MS3, none of them have been RESTful, and that’s OK! We were tasked with designing custom solutions and thus given license to make technical decisions. We identify the required properties for any particular system and, with the business’s interest in mind, we end up with something that is sometimes similar and sometimes much different than REST, but something that better serves our goals.

The responsibilities of a good architect are many, but ultimately solutions are not universal because problems are not. Any case may indeed warrant the latest fashionable architecture, but only through informed evaluation can an architect determine that. The room for today’s decision makers to improve is big, but there are concrete ways in which we can help. Let’s better present the tools at our disposal and establish a process for evaluating them.

I propose we do so in two efforts: First, let’s try to compile and re-present popular tools by focusing on their overall intent and highlighting their trade-offs in an objective manner. Let the details be secondary, at most, until we’ve established what a tool is and is not for. Maybe going as far as starting with the trade-offs as if issuing a warning, e.g. “microservices pose the following trade-offs and challenges … but in return serves the following properties … “. Second, at least for a networked applications architecture, there is already an informed methodology that has long been overlooked, and that is Dr. Fielding’s framework for evaluating design of application architectures. Let’s take this framework and make it more accessible by, perhaps, shaping it into an interactive tool where we can quickly mix and match architectural constraints to see what properties we end up with. Maybe take it even further and adapt it to also take into considerations the tools as presented by our first effort. These steps should help us further our industry by warding against buzzwords and silver bullet statuses and thus allow us to manage their risks.

### TL;DR

REST is the architecture for one specific networked application, but the one that became the most successful ever. So, the already difficult concept became a buzzword, an idea over-prescribed as a silver bullet, with its purpose and trade-offs lost in the hype. The over reliance on trending terms can lead to costly mistakes in any industry, and while we strive to formalize the roles and qualifications of software architecture we’re especially susceptible to them. What’s most important about REST is not the architecture itself, but that it showcases Principled Design and how qualified architects can derive a solution to any use case. To help today’s architects make informed decisions we must find more accessible ways to present the tools and methodologies at our disposal
