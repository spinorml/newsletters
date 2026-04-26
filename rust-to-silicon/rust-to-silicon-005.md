# Rust to Silicon — Issue 005: Trade Show Learnings, Kernel Progress, and a Growing Code Quality Concern

## What I promised vs. what shipped

Short version: strong progress, but the highest-priority milestone slipped by one week.

Last week I said the next move was to get the classic **LeNet (MNIST)** model by Yann LeCun running a full forward pass. I got really close: the model graph builds and kernels compile, but actually running the forward pass slipped to next week.

This week was busy with the trade show visit. I also spent some time building a Claude-driven company analysis tool (it analyzes companies for fit, identifies areas of alignment, and finds principals on LinkedIn). This was incredibly useful because the trade show was huge (more details in the report below).

In terms of research, I also investigated the open-source model RF-DETR, which is very competitive with YOLO26 and fully open source. The final decision between RF-DETR and YOLO26 will happen this week, depending on how things go with Ultralytics.

## Trade show report: MACH2026 (leading manufacturing and engineering show)

The show was **HUGE**, spanning three halls and featuring some of the biggest companies in Europe. As you can imagine, there was a **LOT** of robotics, but mostly the very traditional CNC variety. It reminded me how old this technology is, and how long industry adoption takes.

There was not a huge amount of modern AI (i.e., foundation models, deep learning). Virtually everything was very traditional: a camera takes an image, a system analyzes it, and then generates a plan to execute. But the analysis system is usually handcrafted and tailored to specific setups.

I mainly focused on startups and smaller companies. The larger companies were mostly staffed by sales people, with engineering teams tucked away somewhere in Germany or Ireland. I had an interesting conversation with one of the engineers at **Matta**. Their system is very closed, but still innovative (their own foundation model, or at least claimed to be).

The most interesting conversation I had was with Gio from **Foundry Robotics**. They are very early stage and still validating their hypothesis in some sense. He has been a stellar engineer who is passionate about **Rust** and **Zig**, and is using Nvidia **Isaac** to build their robotics platform. It is always great to talk to passionate people, and this was definitely the case here. I wish them the best of luck.

I went into the trade show hoping for broad industry insight, but came away feeling that the most worthwhile conversation was serendipitous.

I am always excited to see hardware and robotics, and I came away with a real buzz. The energy in the room definitely recharged my batteries.

## Compiler work: Claude writes kernels with tests, but I am watching quality closely

Claude once again impressed this week. One of my tasks was to cover as much of the PyTorch surface area as possible and verify my implementation against it.

I set up Claude to first refactor all the tests to use PyTorch as a reference rather than `ndarray`, and it did a pretty good job.

Then I asked it to implement all the activation functions, pooling, and padding layers from PyTorch. It took a couple of days because of bugs in my original compiler implementation, but once those were fixed (it actually fixed them), all kernel integration tests against an actual GPU went green.

This has been great progress and gives me more time to think about the truly innovative things I want to build. However, I am concerned the codebase is starting to get messy.
Claude did most of the code this week, but without strong guardrails and a coherent architecture, the whole thing could become an almighty mess. This is a serious problem. My bet is that within five years, my compiler and SDK will be integrated into an agent that does a lot of coding for end customers, so the SDK needs to be opinionated and well designed so agents can understand and navigate it easily. If it becomes an unholy mess, they will get confused, fail to solve problems efficiently and simply, and generally be less helpful.

This means that once the initial MNIST training and validation are done, I will likely spend a full sprint reviewing the code, identifying the tech debt I have accumulated, and paying it down. The phase after this (full RF-DETR or YOLO26) is far more complex, and if things are not in good shape now, I cannot imagine what the result will be.

My immediate quality plan:

- tighten architecture and naming consistency
- reduce accidental complexity in kernels and tests
- pay down current debt before moving to the next model phase

## Paper Reading: Tiny Machine Learning: Progress and Futures

I spent a bit of time each day reading this survey paper on the challenges and opportunities in TinyML. I still have not finished it, but I am making steady progress.

## Safety-critical standards: MISRA C and Clippy

The weekly meeting was useful, and I also signed up for the C++ guidelines group and documentation work.
The group has a meeting after RustWeek, so I want to prepare properly by getting fully up to speed. I am thinking of spending two to three full days to get through all my to-dos for this group.

## RustWeek and Trade Shows

**RustWeek** is on the calendar in a more tangible way. If you’re going to **RustWeek**, message me—I’d love to grab a coffee and talk Rust, compilers, and edge ML.

I will be attending the cybersecurity show this week (half day) with a friend. There is a lot of AI there, but it is mainly cloud and threat analysis, so nothing directly relevant to my work. I do not expect many meaningful conversations, but it is still a chance to hang out with a friend at an interesting event.

## Next week

The focus next week is getting the classic **LeNet** model by Yann LeCun through forward pass and training.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published on Monday, 3 May 2026. Stay tuned!

