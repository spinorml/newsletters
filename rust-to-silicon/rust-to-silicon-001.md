# Why I'm building a Rust-native ML compiler for the edge — and what I learned in Q1

Welcome to my weekly newsletter, where I document my journey building a startup in the AI space. Each issue shares honest updates from the trenches—technical wins, challenges, and lessons learned as I work hands-on to bring a Rust-native ML compiler to the edge.

If you build in AI today, you almost automatically build in Python. I did too. It is still the fastest way to test ideas, and the ecosystem is unmatched for research velocity.

But when you move from notebooks to edge deployment, the trade-offs become clear. On embedded and safety-critical systems, you need deterministic behavior, tight binaries, predictable performance, and strong guarantees around memory and failure modes. In that world, Python becomes a liability.

The usual alternative is C or C++. I respect how much production infrastructure they power, especially in low-level systems. But for modern ML deployments, accepting memory unsafety and brittle tooling as the default feels like avoidable risk. I wanted systems performance with stronger correctness guarantees.

That naturally led me to Rust. It has the performance profile, safety model, and developer experience I wanted. The problem is that Rust still lacks a native GPU/ML compiler stack you can run end to end. There are wrappers and bindings, but not a cohesive path where Rust stays the source language all the way to generated kernels.

That gap is why I started Teenygrad.

Teenygrad is a compiler that takes Rust functions written in a custom DSL, lowers them through MLIR and Triton, and emits PTX for NVIDIA GPUs. SPIR-V/Vulkan support for edge hardware is planned next. The long-term goal is simple and opinionated: end-to-end Rust for AI, with no Python anywhere in the pipeline.

Q1 was about proving this is not just a concept.

The biggest milestone was getting a full MIR -> MLIR -> Triton passes -> LLVM IR -> PTX pipeline working. Seeing that chain execute end to end was huge. Each stage is complex on its own, but the real difficulty is in the seams: preserving types, shaping lowering rules correctly, and keeping codegen assumptions consistent across boundaries.

I also decoupled a standalone rustc toolchain from the project. That sounds like internal plumbing, but it made daily work better. Separating compiler infrastructure from product code reduced debug overhead and sped up iteration when passes broke.

On the API side, I built a type-safe kernel interface using proc macros. One design goal for Teenygrad is that kernel authoring should feel Rust-native, not like passing fragile strings through macros and hoping errors surface at runtime. The API is early, but compile-time feedback is already much stronger than I expected at this stage.

For embedded support, I shipped a `no_std` `teeny-core` foundation. That was important because I do not want server assumptions baked into the architecture by accident. I also completed all core codegen operations required for `tensor_add`, which gave me a full vertical slice to validate lowering and emission logic through the entire stack.

Q1 also came with friction.

The hardest technical challenge has been rustc internals and MIR. Rust's compiler is powerful, but building on top of it in a durable way takes patience. It is easy to get something "working" and much harder to get something that survives refactors and edge cases.

I also did a focused SPIR-V assessment for the edge roadmap. The conclusion was encouraging: viable and worth pursuing. But I deferred implementation to avoid splitting focus too early. I wanted the PTX path to be stable first instead of maintaining two half-finished backends.

The non-technical challenge was balancing deep compiler work with customer discovery. It is easy to spend weeks inside lowering passes and lose contact with real deployment pain. Those conversations changed my direction: I am pivoting from a broad inference-market framing to a sharper focus on edge and embedded workloads, where Rust's safety and systems strengths are genuinely differentiated.

Q2 is about turning infrastructure progress into a concrete outcome: YOLOv26 running on NVIDIA Jetson in pure Rust.

The path is clear. First I need to finish the test harness so regressions are caught early. Then I need to expand operator coverage. From there, I will implement the YOLOv26 DSL representation in Rust and push deployment to Jetson hardware.

If this works, it will be more than a demo. It will be evidence that a Rust-native ML compiler workflow can deliver practical edge results without relying on Python glue at every stage.

If you care about compilers, AI infrastructure, or safety-critical systems, follow along. Connect with me on LinkedIn. And if you are building in embedded ML or safety-critical Rust, I would especially like to hear from you. I want to learn from your constraints, your failure modes, and the tooling gaps you still hit in production.

This week, I’ll be running the first end-to-end test: a simple kernel that adds two vectors. While the task itself is straightforward, reaching this point has been anything but—it’s taken real effort to make even basic operations work reliably across the entire stack.

**Note:** The next edition of this newsletter will be published on Monday, 6th April 2026. Stay tuned!

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.
Follow along for technical updates, lessons, and honest insights from the front lines.
