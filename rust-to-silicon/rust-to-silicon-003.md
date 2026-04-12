# Rust to Silicon — Issue 003: Triton ops in Rust, standards tooling, and RustWeek

## What I promised vs. what shipped

Last week I said the next move was **activation kernels and Conv2D** for the YOLOv26 path. That step is still the goal, but it depends on having enough of the **Triton-style DSL** available in Rust first. So this sprint went into that prerequisite instead of the kernels themselves.

## Compiler work: DSL operations at scale

Rather than hand-writing every builder, I pointed an LLM at the Triton docs and asked for DSL operations. The first pass was intentionally vague; it was still useful, and I expect to tighten the API as real use shakes out.

The more systematic half of the work was mechanical in a good way:

1. **Inventory** — I pulled the operations from the **Triton MLIR dialect** and turned each into a tracked item. I’m using [**beads**](https://github.com/gastownhall/beads) for that: a CLI-friendly issue tracker that fits well with agent-assisted workflows.
2. **Plans** — I scripted generation of a plan per op (I had already done a handful manually with unit tests). I spot-checked the output; it looked sane enough to run with.
3. **Implementation** — Same pipeline to scaffold the **Rust API** that constructs each operation. Plenty of items will need rework once integrated, but this is the kind of repetitive boilerplate that would have burned something like a week if I did it entirely by hand. The outcome is a **typed Rust surface** for building these ops, ready to wire into the compiler.

A **potential freelance engagement** took up about three days of the sprint. The extra runway is appreciated, though it inevitably comes with tradeoffs (and as a bonus, I was reminded of Java’s many shortcomings as a language).

## Reading: Feature Pyramid Networks

On the research side I read the **Feature Pyramid Network** paper. I’m not turning this newsletter into a literature review, but it was a useful lens on **multi-scale representations**—the kind of thing that matters when you’re thinking about real detectors and how operators and memory layout need to behave on hardware.

## Safety-critical standards: MISRA C and Clippy

I’m still deepening my **MISRA C** study (alongside the broader picture from last issue). The point is the same: contribute to the **Safety Critical Rust Coding Standards Committee** with enough grounding that feedback is concrete, not hand-wavy.

New this week: I’ve started learning **how Clippy lints are written**, with an eye on the committee’s **Clippy workstream**. Standards stick when tooling encodes them; I’d rather help build that bridge than only discuss rules on paper.

## RustWeek

**RustWeek** is on the calendar in a more tangible way: **hotel is booked**. I’m already looking forward to it—and to meeting people in person. I have a **LinkedIn connection at Espressif** I’m hoping to connect with there; edge and silicon people in one place is exactly why these trips are worth it. If you’re going to **RustWeek**, message me—I’d love to grab a coffee and talk Rust, compilers, and edge ML.

## Next week

The focus next week is on **activation-function kernels** and **Conv2D**—returning to the original plan now that the DSL scaffolding is in much better shape. If possible, I’ll also work on implementing the Feature Pyramid Network architecture. The main challenges ahead are composing kernels effectively and designing complete operators (that is, implementing both forward and backward kernels).

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

**Note:** The next edition of this newsletter will be published on Monday, 20 April 2026. Stay tuned!

