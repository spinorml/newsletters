# Rust to Silicon — Issue 014: Anduin on hold, RISC-V takes the lead

## What I promised vs. what shipped

**Short version:** The full Anduin optimizer did not ship. It is sitting on a branch to be picked up later. Plans for this month have changed: I will be focusing on a QEMU-verified RISC-V RVV backend for the teenygrad compiler.

## Accelerating RISC-V development

The Anduin work was going pretty well. I had solutions for all the major issues. It still probably needed two to three weeks for the full implementation across all my kernels — particularly the thorny ones, such as convolutions with padding and reductions.

The choice I had to make was to focus on performance or start work on the RISC-V backend. I have a potential partner who is interested in a Rust toolchain and SDK for machine learning on their new hardware, targeting industrial edge applications.

At this point in the project, I really need to reach out to industry to ground the work. So the natural next step is to get RISC-V working, then focus on performance. Their use cases and hardware are ideally suited to my vision: low-cost embedded hardware in industrial applications such as robotics and drones.

Therefore, I have decided to focus fully on RISC-V for the next two months, to get a full compiler and computer vision SDK that runs on a low-cost RISC-V processor.

To this end, I spent the latter half of last week scaffolding a RISC-V backend for the compiler and adding first-class integration test support — which Rust's features make incredibly easy. The whole system builds, generates a dummy kernel, and runs the integration test suite end-to-end using QEMU.

## Papers I am reading this week

1. [TensorIR: An Abstraction for Automatic Tensorized Program Optimization](https://arxiv.org/abs/2207.04296)
2. [Tensor Seeks Layout: Formalizing Layout Selection for ML Compilers](https://arxiv.org/abs/2608.21555)

## Next week

Now that the foundations are ready, I am looking for the right approach to building the compiler backend. The goals for the project are:

1. AOT compilation support.
2. Highest performance on constrained hardware (compute, memory budget, and so on).
3. The ability to natively integrate with cameras, motors, and other peripherals.
4. Easy customization for specific processors and memory hierarchies.

There are a number of projects I can look at to see how they approach the problem. The most interesting are:

1. Triton CPU — a generic CPU backend for Triton (not RISC-V specific).
2. Hexagon MLIR — again Triton, but this time targeting other dialects that lower using other machinery (for example, XLA).
3. Buddy Compiler — a more generic compiler research project, but one that does target a variety of hardware.

So I will spend this week getting a deep dive into each of these projects, and seeing how they approach the task of taking high-level AI workloads to non-GPU targets.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published next Monday. Stay tuned.

