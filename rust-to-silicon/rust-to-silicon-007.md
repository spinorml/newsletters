# Rust to Silicon — Issue 007: Review of Claude Code after 4 weeks of agentic coding, YOLO26 training/inference works, onward and upward!

## New newsletter: This Week in Edge AI

I have launched a second newsletter: **This Week in Edge AI**.

It is a weekly digest of edge AI, embedded ML, and silicon news for engineers building real systems every Tuesday. The first issue covers practical edge inference guidance, FPGA updates, notable events, and Rust momentum in edge deployment.

You can subscribe here: [this-week-in-edge-ai.beehiiv.com](https://this-week-in-edge-ai.beehiiv.com/)  
You can read Issue 01 here: [This Week in Edge AI: Issue 01](https://this-week-in-edge-ai.beehiiv.com/p/this-week-in-edge-ai-issue-01)

## What I promised vs. what shipped

Short version: big progress. I promised YOLO26 inference and training would work, and now they do.

Last week, I said the next move was full YOLO26 training and inference via Rust. Happy to report: done, and working well. Performance is not great yet, as this is still a naive implementation (i.e., no async, no CUDA graphs, no kernel fusion). Optimizing the CUDA pipeline is a later-in-the-quarter task; I expect it to take 1-2 weeks and get me within about 20% of TensorRT. Beating TensorRT will require profiling and hand-tuning kernels, which I genuinely enjoy (and LLMs are actually very good at this too).

![YOLO26 inference results](https://spinorml.github.io/rust-to-silicon/assets/yolo26-inference.png)

The fact that my framework can do both inference and training on the edge is a real differentiator, and it opens up huge possibilities. I will demo this with implementations of LoRA adapters (and Titans, a la Ali Behrouz's paper), both of which I am excited to build.

I finally received the Jetson Orin Nano (Super Developer Kit), which is my device of choice for all the demos. It took a while to get it running. First, I did not have a microSD card and tried USB setup, but sadly NVIDIA SDK Manager for JetPack 6.2 only supports Ubuntu 22.04, while my server was on Ubuntu 24.04. Then I tried a Docker image approach, and that seemed to work, but it got stuck at 99% while flashing the Orin Nano. Finally, I did what I should have done in the first place and ordered a microSD card. It is a two-stage process on the Jetson Orin Nano: first you update the firmware using a firmware image, then you install the Jetson software using its own image. I now have a working Jetson Orin Nano that I can access via SSH.

The next challenge is compiling and deploying my project to the Orin Nano. Claude suggested just installing the Rust toolchain on it and compiling there. But that is not the point of this project: I want to do everything on the host and then one-click deploy to the device. So I will spend the next week getting cross-compilation and SSH-based deployment working. It should be doable, as NVIDIA provides cross-compilation SDKs; the tricky bit will be integrating them with `cross`.

## Review of Claude Code after 4 weeks

Claude continues to be super impressive. I am not going to make big judgments about code quality yet, because the project was already a bit messy and I gave it no explicit code quality guidelines or pedantic reviews of what it produced.

The project is still an MVP, with a fair bit of experimentation. Right now, working code matters more than architectural cohesiveness or "abstract" notions of code quality. I have spent a lifetime on large, complex codebases, so I have a pretty good nose for things that are plainly wrong or improvable. I am confident I can bring it all together once I have a fully working 1.0 MVP.

I have noticed that when an issue arises, Claude immediately starts by looking at the nearest proximate cause. In the case of YOLO26, I asked it to compare the output of my model on a single image with the Ultralytics reference implementation. The results were starkly different, and it immediately decided the issue must be in the detection head (the last layer in the model). I did not think that was true. I was sure there were problems much earlier on (it would be a miracle if all kernels and image preprocessing had worked perfectly). Anyway, I let it do its thing. It spent a day trying this and that without succeeding. Finally, I told it: print both inputs and outputs from every layer of the model, from both my implementation and theirs. I then asked it to check them one by one from the beginning, not from the end. At that point it identified a few different issues and fixed them. I finally had a fully working forward model. The backward pass similarly had to be done layer by layer.

So my current conclusion is this: I get the best out of Claude with a TDD (test-driven development) approach. Write tests at reasonably small granularity so it gets a manageable issue it can solve, rather than a huge issue with multiple causes where it latches onto the wrong thing.

## Paper Reading: YOLO26: A Comprehensive Architecture Overview and Key Improvements - P Hidayatullah, R Tubagus

This is a great little paper that describes the architecture of YOLO26 in enough detail to implement it from scratch, and it was the basis of my implementation. I did not really fancy looking at the Ultralytics code, as my aim was to approach it with fresh eyes and identify my own ways to speed up the model. There are obvious avenues, such as async processing, which they cannot do because they are based on Python, and ONNX gives very limited control over how the model is actually compiled and run.

I will be making a presentation to the nPlan paper reading group later in the month based on this paper.

Another paper I have started to re-read is \*\*Titans: Learning to Memorize at Test Time - A. Behrouz et al.\*\*. It is something I am keen to experiment with, and hopefully I will get a chance to present it to the nPlan group once I have implemented it and have practical results.

## Safety-critical standards: MISRA C and Clippy

The weekly meeting is always interesting, and I learn something new about Rust every week. I still consider myself at a rough intermediate level in Rust, and this group continues to push me deeper.

It is my aim to make teenygrad the first safety-critical ASIL D-certified ML stack. This is still some way off, as Triton itself is not memory-safe and the project has both Rust and C/C++ components. However, I know I can integrate the project into Ferrocene (the safety-critical certified compiler from Ferrous Systems), and both Triton and the C++ surface area are small enough to certify against existing C/C++ standards.

## RustWeek and Edge Impulse AI

**RustWeek** is now very real on the calendar. If you are going to **RustWeek**, message me—I would love to grab a coffee and talk Rust, compilers, and edge ML.

I will also attend the Edge Impulse AI event in Amsterdam on 20 May (as luck would have it, I will already be in the Netherlands for RustWeek).

## Next week

Cross-compilation and deployment to Jetson Orin Nano, and prep for **RustWeek**.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published on Thursday, 21 May 2026. Stay tuned!

