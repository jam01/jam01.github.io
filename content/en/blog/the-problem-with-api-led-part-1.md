---
author: Jose Montoya
title: The Problem with API-Led - Part 1
date: 2021-12-21
description: ???
tags: [ "integration", "api", "patterns" ]
categories: [ "integration" ]
---

In my years of helping organizations with modernization or API-enablement through integration, I constantly interact with Mulesoft's API-Led architectural pattern proponents. Either because they sincerely believe in its technical merits or because some variation of _it was given to us from above_.

If you've worked with me in the past, you know that API-Led is not anywhere near the top of my go-to patterns, to put it politely.

I'll usually engage honestly in a discussion around the applicability and limitations of the pattern based on my experience and that of other thought leaders in this space. Then I'll usually suggest another pattern in its place because when you criticize any solution without an alternative, you're just whining. Not coincidentally, though, every conversation always starts with or arrives at the part where we need to agree on what we mean by API-Led. This forces me to keep handy my printed copy of the whitepaper.

Earlier this year, I had one such discussion with the lead architect for an organization, whom we'll call Jim. Now, Jim is a smart and experienced professional, truly. Jim's organization had started on a greenfield product a little less than a year prior and leveraged Mulesoft to implement all of their backend systems (🚩). Jim directed the architects in his team to employ API-Led pattern across the board (🚩🚩) to drive API reusability. It's unclear to me whether this was entirely Jim's decision or if it was at the suggestion of a consultant.

The organization saw a high lead time to add features or general changes to the platform. A high level of collaboration needed to occur, and multiple things needed to be tested across layers for individual changes. However, my task in the org was to help a team craft new APIs around some particular business area. I made some high-level designs and shared them with the lead engineer. The first question from them was, "Where are the system, process, and experience APIs? That's what we need to do."

You might be nodding your head or are recounting a similar conversation. So I decided to reach out to Jim to discuss API-Led's (ab)use and suggest some more consideration around its applicability and other approaches that would speed up how we delivered value to our customers. I started by explaining at a high level how the way the pattern works is known to slow digital native organizations (more on this in Part 2), Jim's reply was, "Well, there's different interpretations of API-Led…" (🚩🚩🚩).

<div class="row align-items-center">
<div class="col-md-2"></div>
<div class="col-md-6"><img class="rounded img-fluid" src="https://i.imgflip.com/2ze11z.jpg" alt="here we go again" /></div>
<div class="col-md-2"/></div>
</div>
<br/>

There are two main parts to codifying things into patterns. The main one is the technical: its implementation, the context in which it can be applied, the resulting context, limitations, challenges, etc. The second one is the cognitive or semantic one; when I say MVC, you immediately know what I'm talking about; those working in the presentation domain will think about its limitations around data binding compared to a pattern like MVVM, for example. If I say Pipes and Filters, you'll think of Unix or even the Mule DSL itself. You get the idea.

The authors of Fearless Change, Patterns for Introducing New Ideas, put it this way:

_The name of the pattern is of critical importance. When pattern names are used in a community, the individuals speak a common language… If it can be used and the people working in the area understand what you mean, then the name is probably a good one… That's an effective test for a pattern name._

If every time we discuss API-Led's applicability we have to level-set what it means, then it's a bad name. The extra cognitive hurdle has more implications than "just semantics"; it leads to some parties applying the pattern one way and others in another. And once you change something from the pattern, you can no longer guarantee that the predicted outcomes will be realized. If I give you a recipe for some dessert, but you skip the sweetener, then we're in trouble.

<div class="row align-items-center">
<div class="col-md-2"></div>
<div class="col-md-6"><img class="rounded img-fluid" src="https://i.imgflip.com/5ymcj9.jpg" alt="it does not mean what you think" /></div>
<div class="col-md-2"/></div>
</div>
<br/>

"API-Led" suggests something along the lines of API-driven or API-first design, which is hardly groundbreaking or descriptive at all. The name seems driven more by marketing than anything technical, which should make some suspect of the motivation behind it. Ultimately it's about layering API-enabled microservices sliced by their rate of change; you create layers as building blocks, from more stable systems of record up to frequently changing systems of engagement.

API-Led doesn't sound bad! Narrator: it was.

In Part 2, we'll dive into the technical part. Stay tuned!

P.S.: I am indeed related to Iñigo Montoya.
