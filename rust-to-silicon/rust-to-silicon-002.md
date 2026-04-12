# Rust to Silicon — Issue 002: Verified on hardware, RustWeek, and the Jetson roadmap

Last week I said the next step was a simple vector-add kernel end to end. This week that kernel is written in Rust, compiled through the stack, running, and **verified on an NVIDIA RTX 4070**. On paper it is a tiny operation; in practice it is the first time the full path—from the Rust-side representation through lowering and codegen—meets a real consumer GPU and comes back with numbers I can trust. That matters because edge work is not abstract: correctness and performance only show up when you execute on hardware, and this slice gives me a baseline to regress against as operators get harder.

A few other things I’m really grateful for:

- I’m attending the **Safety Critical Rust Foundation** meetup after **RustWeek 2026** in Utrecht—huge thanks to **Pete LeVasseur** for the slot. If you’re going to RustWeek, message me—I’d love to grab a coffee and talk Rust and AI.
- I’ve joined the **Safety Critical Rust Coding Standards Committee** (thanks again, Pete). I’m ramping up on **MISRA C** and **CERT C** so I can contribute properly, not just observe. I’m especially excited about the **Clippy**-oriented work to enforce the standard we’re defining—tooling that catches issues early is how these standards become lived practice, not shelfware.
- I’ve joined **STEAMHouse** here in the UK, it provides co-working and potential collaboration with academic at the University. Great conversations this week with founders (including a team in **eye health** developing hardware and software, no AI yet but on the roadmap) and CS faculty with deep **robotics and drones** experience—exactly the kind of cross-disciplinary environment that keeps compiler work grounded in real products.

On the product side: **YOLOv26 on NVIDIA Jetson** in pure Rust is now planned for the quarter. The timeline is aggressive, but every kernel is mapped and **active development starts now**. The point is not a one-off demo: it is to show that a Rust-native ML compiler workflow can deliver something people actually ship on constrained hardware, without Python glue holding the pipeline together.

**Next week:** activation-function kernels and **Conv2D**.

If you care about **compilers**, **edge ML**, or **safety-critical Rust**, I’m documenting the journey openly—connect and follow along.

**Note:** The next edition of this newsletter will be published on Monday, 13th April 2026. Stay tuned!

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.
Follow along for technical updates, lessons, and honest insights from the front lines.

