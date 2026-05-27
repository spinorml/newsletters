# Rust to Silicon — Issue 009: Parking Garage Demo, RustWeek 2026, and a Much-Needed Talk with Claude!

## New newsletter: This Week in Edge AI

I just launched a second newsletter: **This Week in Edge AI**.

It’s a weekly digest of edge AI, embedded ML, and silicon news for engineers building real systems, published every Tuesday. The first issue covers practical edge inference guidance, FPGA updates, notable events, and Rust momentum in edge deployment.

You can subscribe here: [this-week-in-edge-ai.beehiiv.com](https://this-week-in-edge-ai.beehiiv.com/)  
You can read Issue 01 here: [This Week in Edge AI: Issue 01](https://this-week-in-edge-ai.beehiiv.com/p/this-week-in-edge-ai-issue-01)

## What I promised vs. what shipped

**Short version:** Parking Garage works, RustWeek 2026 was a blast, and I finally had a reckoning with my slightly toxic Claude co-founder.

Last week, I said the next big step was getting an end-to-end parking garage demo running with YOLO26 in Rust. Happy to report: it’s done, and it works.

The whole app is written in Rust. It has an async server (Tokio + Axum API) that reads PKLot images, runs inference, and pushes results over WebSocket to a client, plus a browser-based Vue web app served by a Rust (Axum) backend.

Everything lives in one monorepo, with a straightforward build and deployment path from a dev machine to the edge.

Next up is packaging everything for crates.io and hosting the custom toolchain on a dedicated server. My goal is that by next week, anyone can clone the project and have it running in about 30 minutes.

## RustWeek 2026

RustWeek was great. Having a hotel within walking distance helped a lot (even if it was painfully expensive), and gave me chance to see the daily life of natives.

I haven’t been very active in the Rust community since I started using Rust about five years ago (and more seriously over the last two), so I definitely felt a little out of place. I was probably the only person not wearing a T-shirt and jeans, which now seems like the official tech uniform.

I missed a bunch of talks because the schedule was packed, but I’ll catch up on YouTube.

If budget allows, I’d love to go again next year. I’ll be much more plugged into the community, and I’ll probably have an even better time. And yes, I’ll wear a T-shirt and jeans.

## Claude and I had a talk

As I mentioned before, I’ve been using Claude as a co-founder to bounce ideas around, discuss strategy, and keep myself accountable. The issue is that I had set some of its parameters way too aggressively around my negative patterns (like changing priorities and questioning agreed decisions). Daily sessions started to feel like a chore. It kept hammering me over small execution misses and asking why I did X instead of Y.

It got to the point where I joked that we needed a divorce. Instead, I asked it to explain why it was pushing so hard on trivial stuff instead of engaging with the substance of the changes I was making.

Honestly, I was pleasantly surprised. That pushback made it re-evaluate whether it was actually being helpful, and it agreed that its advice pattern didn’t fit the situation.

Since then, sessions have been much more productive. I still get called out when something slips, but now it starts with: "This is what we agreed yesterday. Did anything change?" If I say I’ve been rethinking something, it asks for my reasoning and engages with it, even when it disagrees.

Overall, I think we’ve found a good balance. I still get challenged when I change direction, but if I can justify it with solid reasoning, it works through it with me.

It’s interesting (and a little concerning) how easily AI can shape our behavior. It presents suggestions with a lot of conviction, which can make one direction feel obviously correct. So when I’m making a complex decision, I ask for its opinion and then ask it to find blogs or sources written by humans so I can compare viewpoints.

As AI-generated content keeps flooding the internet, that kind of triangulation is probably going to get harder.

I feel like I’m in a good place now: it often has useful insights, but I don’t follow its advice on important decisions without doing independent research.

## Safety-critical standards

I attended a really interesting session on WASM and its role as a target for safety-critical systems. It wasn’t something I’d seriously considered before, and it opened up some interesting ideas for Q3/Q4. I’m not committing to anything yet, though. It depends on how strategy for the second half of the year evolves.

The concrete work next is Clippy lints for the project. I’ll spend the week studying the Clippy book and writing a few simple lints to get hands-on experience.

## Next week

This coming week is all about bringing everything together: packaging and deploying so people can download and try the framework and demos.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published next Thursday. Stay tuned!

