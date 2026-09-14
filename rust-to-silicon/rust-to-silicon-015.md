# Rust to Silicon — Issue 015: RISC-V lands in teenygrad, and Anduin is back on

## What I promised vs. what shipped

**Short version:** RISC-V support is now integrated into teenygrad via triton-cpu, with most QEMU hardware tests passing. The Milk-V Jupiter 2 has shipped, and I am switching back to the Anduin optimizer until the hardware arrives.

## RISC-V support integrated into teenygrad

I was able to take the triton-cpu implementation and integrate it into the teenygrad compiler. That gives me a RISC-V RVV 1.0 implementation I can test against real hardware.

Out of 286 hardware integration tests (via QEMU), only 66 are failing, and the root causes come down to about five issues. Some are more complex than others, but they are fixable.

A huge thanks to the triton-cpu folks. This gives me a baseline from which I can build my vision of a state-of-the-art ML framework for RISC-V.

I am now faced with a decision: fix these remaining issues, or get back to Anduin (the fusion compiler, which will really move the needle). I think I will switch back to Anduin. Once that is fully working — and the RISC-V hardware has arrived (the Milk-V Jupiter 2 is on the way, and the partner hardware is most likely mid to late October) — I will focus 100% on the RISC-V backend.

So, all in all, a great week and real progress.

## Milk-V Jupiter 2 has shipped!

I have been waiting a couple of months for the Milk-V Jupiter 2 to ship, because it has been on pre-order from Aracetech. Their support office has been really great, and they have answered my dispatch queries promptly. I will definitely use them again for future hardware purchases.

The shipment should arrive in one to two weeks. I am not sure how customs works in the UK — this is my first foreign import — and there may be some duty to pay. But I assume I will have the hardware to hand within two to three weeks, and I am incredibly excited to start working with it.

## Papers I am reading this week

I did not quite finish the Tensor Seeks Layout paper from last week, so I will finish that and then I have two further papers to read (all prerequisites for the Anduin optimizer work).

1. [Tensor Seeks Layout: Formalizing Layout Selection for ML Compilers](https://arxiv.org/abs/2608.21555)
2. [RAMMER: Enabling Holistic Deep Learning Compiler Optimizations with rTasks](https://www.usenix.org/system/files/osdi20-ma.pdf)
3. [ROLLER: Fast and Efficient Tensor Compilation for Deep Learning](https://www.usenix.org/system/files/osdi22-zhu.pdf)

## Next week

I plan to dedicate the week to making real progress on the Anduin optimizer. The goal is to have at least pointwise kernels fused, and if possible fusion of pointwise prologue operations (for example, Conv2d + SiLU).

I am also weighing whether to submit a talk to a couple of upcoming conferences. I need some professional headshots and other marketing material, so I will also look into this.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published next Monday. Stay tuned.

