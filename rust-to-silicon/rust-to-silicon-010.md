# Rust to Silicon — Issue 010: Back from Hiatus, teenygrad 0.1.0, and Betting on RISC-V

## What I promised vs. what shipped

**Short version:** I’m back. teenygrad 0.1.0 and a Vision SDK are live with a demo you can run in about 30 minutes, and I’m shifting the hardware bet toward RISC-V.

I’ve been quiet for a while. Not because I stopped building — because I spent a stretch talking to potential customers and trying to figure out where this project actually sits in the market.

## Lessons from the hiatus

The honest takeaway: this project is early. Maybe one to two years early.

Rust adoption is growing, but the inertia of the traditional C/C++ ecosystem is still very strong. Rust on embedded is moving in the right direction, and I can ride that wave — but it will be slow. That is the reality.

This is a pattern I keep running into. I have been early to most of the problems I care about. In 2000 I was working on hosted e-commerce (Shopify before Shopify), and as a small solo company in the UK I could not get credit card processing sorted. Limited resources, right idea, wrong moment. Timing is everything in a startup, and poor timing is a killer.

I like being on the cutting edge. That is not going to change. But the path forward for this project is clearer now: build something people will actually use. I will still be guided by my vision, but I am also going to try things, ship demos, and let usefulness decide what sticks.

The focus going forward is more demos, more content, and building a community.

## teenygrad 0.1.0 is live

Version 0.1.0 of the teenygrad compiler and a Vision SDK are now available, with an easy install path and a demo you should be able to get running in about 30 minutes.

I will publish a more detailed release blog post soon. For now: it is out, you can try it, and I want feedback from anyone building compilers, ML infra, or edge AI systems.

The project also now has a [website](https://teenygrad.org) — please check it out and let me know what you think.

## Claude Maxxed Out

AI assistance has been invaluable to this project. I could not have gotten where I am without it. The surface area the compiler and kernels cover is pretty competitive with PyTorch. Hardware support is more limited — but so is PyTorch on the edge, where the vast majority of deployments still use ONNX Runtime.

Going forward, I do not see AI use as central in the same way. The hard problems now are new hardware, and I am not going to vibe-code those. That work needs deep knowledge of the hardware and memory hierarchies. Letting an AI build it out without that grounding is just asking for trouble.

In that vein, I have downgraded my Claude subscription back to Pro. That should be enough for paper summaries, the odd debugging session, and — combined with Cursor — all the AI I need for this next phase.

## Betting on RISC-V

To differentiate the project, I am betting on RISC-V and open ISA hardware. Reverse-engineering closed ISAs is no fun, and RISC-V is the most exciting place to be right now.

I am currently working on SpacemiT K3 support (Milk-V hardware is on the way — I cannot wait to get my hands on it). That means a new custom Triton backend for RISC-V, so expect more content on edge AI hardware and Triton internals as I get my head around building a high-performance backend.

## Next week

Shipping the release write-up, more demos, and starting the SpacemiT / RISC-V Triton backend work in earnest.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published next Monday. Stay tuned!

