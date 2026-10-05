# Rust to Silicon — Issue 017: Anduin core progress, and the Jupiter 2 is up and running

## What I promised vs. what shipped

**Short version:** Last week I promised Anduin progress and getting the Milk-V Jupiter 2 booted. The board is set up and running. Anduin made good progress, though most of the coding was done by Claude and still needs a thorough review.

## Anduin optimizer work

Good progress with the core of the optimizer this week, although most of the actual coding was done by Claude. I know this leaves me with a large body of work that will need a thorough review, and perhaps some major changes.

But I am keen to see the Welder-based approach working in principle this week, and without Claude it would have taken a lot longer.

## Milk-V Jupiter 2 is up and running

The setup of the Milk-V Jupiter 2 was a breeze — at least once I worked out how to power it. It is a shame it does not ship with a power on/off switch and LED. I cannot fathom why they skimped on this; it would probably only cost a couple of dollars extra.

On the other hand, the actual setup was incredibly simple compared to the NVIDIA Jetson Orin Nano, which required me to purchase an SD card, flash it with a JetPack image that I had to download from the internet (non-trivial itself, given how many different models of the hardware there are), then connect pins on the board and find a DisplayPort adapter. For the Jupiter 2, all I needed was a USB-C to HDMI adaptor with power, and voila — I had a running system in five minutes (the OS is pre-installed on the system).

I decided to get the more powerful 32GB RAM variant, so I can test different sizes of models and LLMs. The performance of the Jupiter 2 is very impressive, although I have not run any benchmarks on it yet.

Once the optimizer work is in (about two to three weeks), I will be getting back to the RISC-V RVV 1.0 port, and having some decent hardware to test it on. I am pretty excited for the journey.

## Papers I am reading this week

I am continuing to read this paper, and its references. I hope to do a presentation on it soon, which I will share.

1. [A Performance Vocabulary for Affine Loop Transformations](https://arxiv.org/abs/1811.06043)

## Next week

The plan is to get the core of the Anduin optimizer working, so that I can put everything together and start integration testing the week after.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published next Monday. Stay tuned.

