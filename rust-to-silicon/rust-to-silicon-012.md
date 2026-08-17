# Rust to Silicon — Issue 012: teenygrad is shipped, and optimisation work is underway

## What I promised vs. what shipped

**Short version:** Last week I promised to ship the initial release of teenygrad, and that is now up and running. I also presented the project to the Embedded Rust group — [here is the video](https://www.youtube.com/watch?v=76pawJznRM4).

I also began the performance optimisation work.

## Closing the performance gap with TensorRT (work in progress)

The next release of teenygrad will include the first version of the Anduin optimizer. It is based on a recent paper, [Welder: Scheduling Deep Learning Memory Access via Tile-graph](https://www.usenix.org/conference/osdi23/presentation/shi) by Yining Shi et al.

Machine learning models are slowed down by two main causes.

**1. Kernel launch overhead.** ML models are graphs — sometimes very large graphs. Nodes depend on each other because the output of one node is the input of others. Each node is a kernel (a GPU program), and launching them one by one takes time. YOLO26 nano, for example, has about 360 nodes. That launch cost adds up, and it can easily exceed the time spent on actual computation.

The usual fix is operator fusion: take a chain of dependent nodes and turn them into a single program. Instead of launching 360 separate kernels, you might launch 50. There are more extreme approaches that fuse the whole graph into one program — those are called mega-kernels — but that is much more advanced work.

**2. Data in the wrong place.** A second source of slowdowns is data sitting in the wrong level of the memory hierarchy — disk, host RAM, GPU global memory, and so on. Moving it to where the computation actually needs it is expensive. Getting data into the right place at the right time can improve model performance significantly.

We could also rewrite the algorithm itself, but that is a much harder task. The initial plan is to address (1) and (2) in the Anduin optimizer.

## Next week

The initial release of the Anduin optimizer, with the hope of closing some of the gap between the current compiler and TensorRT. I cannot accurately predict the exact performance improvement, but I think I can cut the current gap by 50%.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published next Monday. Stay tuned.
