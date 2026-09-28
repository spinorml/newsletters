# Rust to Silicon — Issue 016: Anduin progress, and the Milk-V Jupiter 2 arrives

## What I promised vs. what shipped

**Short version:** This is going to be a short update. Anduin optimizer work is in progress, but progress has been slower because of an illness I am just getting over. The Milk-V Jupiter 2 arrived a couple of days ago, and I plan to get it set up for development this week.

## Anduin optimizer work

Progress has been much slower than I planned, due to a number of issues. The first has been a short illness — kids going back to school sadly means virus mass-spreading events. I am working through the declarative metadata required by the different types of kernels. The metadata essentially tells the optimizer the iteration space of the kernel, which allows it to optimize the tiling.

The simplest cases have been implemented, and I will be working on the more complicated ones, of which there are quite a few variants. I know this description is somewhat vague, but the details are rather complex and probably not of interest to most people. I had Claude break the work down into a set of 11 subtasks, and I need to study each one and get my head around the appropriate solution.

## Milk-V Jupiter 2 has arrived!

The Milk-V Jupiter 2 arrived a couple of days ago. After a couple of months on pre-order, it is finally here, and I am incredibly excited to start working with it. This week I plan to get it set up for development.

## Papers I am reading this week

Polyhedral analysis of computations is something I want to learn more about, so in that vein this is the paper I will be reading, and following up on any interesting threads.

1. [A Performance Vocabulary for Affine Loop Transformations](https://arxiv.org/abs/1811.06043)

## Next week

The plan remains the same as the last two weeks: making real progress on the Anduin optimizer, including some of the more complex kernels, and getting the Milk-V Jupiter 2 booted and SSH-able for further development.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published next Monday. Stay tuned.

