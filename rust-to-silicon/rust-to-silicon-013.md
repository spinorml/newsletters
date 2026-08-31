# Rust to Silicon — Issue 013: Anduin optimizer progress, and looking ahead to RISC-V

## What I promised vs. what shipped

**Short version:** I spent the last two weeks on the Anduin optimizer, and I started getting up to speed on RISC-V ahead of the Milk-V Jupiter 2 arriving.

## Closing the performance gap with TensorRT (work in progress)

I spent the last two weeks working on the Anduin optimizer for the compiler. Its purpose is to schedule and fuse operations in the neural network model.

This optimizer is based on the paper [Welder: Scheduling Deep Learning Memory Access via Tile-graph](https://www.usenix.org/conference/osdi23/presentation/shi) by Yining Shi et al.

The Welder approach is to take a neural network graph and walk backwards from the end to the beginning, inferring the shapes of all intermediate operators. Once we have the shapes, we can partition them using an appropriate tiling strategy — this may take account of hardware such as MMA — and the available memory in the accelerator hierarchy (device memory, shared memory, registers, and so on), and then schedulee based on memory traffic and latency.

In my case there are three complications that mean the paper cannot be applied directly.

**1. Shape propagation.** Welder propagates operator shapes backwards through the graph by walking the tensor expressions (the TVM representation). I cannot do this directly, because Triton kernels can perform arbitrary pointer arithmetic, which in general cannot be analysed. The initial solution is for developers to annotate their kernels with metadata that drives shape inference. Longer term, a number of well-known patterns may be analysed automatically; those that cannot would produce a warning and a fusion break.

**2. Triton's own allocation strategy.** Triton has its own strategy for allocating shared memory and registers, and for when MMA instructions can be used. I need to see how Triton can co-exist with this approach. That will stay work in progress as I convert the kernels to be fusable.

**3. Blocks, threads, and barriers.** GPU execution typically breaks kernel work into blocks and threads. That is problematic because different operators may prefer different block and thread counts. When operators are fused, we need a common block/thread size across the fused operation. Welder uses virtual threads as a mechanism to overcome this: in essence, some operators simply operate on multiple tiles. That in turn introduces the thorny issue of barriers. This will also stay work in progress as I work through the kernels to see whether Triton's built-in barrier mechanism is enough, or whether something more sophisticated is needed.

My goal this week is to get a couple of well-known operations fused — for example, conv2d + batch norm + silu — and check the results manually.

## Looking ahead to RISC-V

I am due to take delivery of the Milk-V Jupiter 2 within the next couple of weeks, so I spent a couple of days this week getting up to speed on the RISC-V spec and RISC-V assembler programming. Fortunately, there are many excellent resources for this.

I also had an interesting conversation with a LinkedIn connection about potentially working with a Chinese industrial SoC manufacturer to support their new RISC-V processor.

I am looking forward to wrapping up the Anduin optimizer work within two weeks and then working full-time on RISC-V support. My goal is to make teenygrad the highest-performing inference engine on RISC-V.

## Next week

Getting a number of the most important kernels in the YOLO26 model fused and verified.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published next Monday. Stay tuned.

