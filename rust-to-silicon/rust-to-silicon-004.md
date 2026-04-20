# Rust to Silicon — Issue 004: First partner call, Megakernels, Claude is damn good!

## What I promised vs. what shipped

Last week I said the next move was **activation kernels and Conv2D** for the YOLOv26 path. Initial versions of those kernels are now done, with some testing. More thorough testing is needed.

I also looked at various approaches to kernel fusion and mega kernels. A full mega-kernel implementation is still the long-term goal, but it will probably slip to Q3 or 2027/Q1 (the main issue being efficiently mapping kernels to hardware, i.e. threads/warps and tensor cores). I have some ideas, but realistically this is a research project rather than a concrete implementation proposal.

## Partner meeting: Meeting the partner manager at Ultralytics

I was grateful for the opportunity to speak with the Partner Manager at Ultralytics (and one of their senior devs). They are the team behind YOLOv26 and one of the most popular vision SDKs on the market, and they have recently raised a Series A.

It was a really useful conversation for me to speak with people who are so plugged into their customers and their needs, whereas I, as a founder, spend my days pumped on caffeine and a bold vision! It hit me how hard it is to sell AI adoption with a new, untested technology.

They agreed to help me with my development and testing by providing the appropriate permissions. They are also happy to look at a demo when I have it ready (semi-firm commitment to 8-12 weeks).

## Compiler work: Complex kernels (such as MLP, AvgPool2D and Conv2D)

Since Claude had done a pretty good job last week, I set it the task of implementing and testing these more complex kernels (non-trivial, since more features of the Rust compiler needed to be implemented), as well as mapping to the Triton IR. It took a long time to do the first kernel (Linear), approx. 2 days, and I had to prompt it a couple of times. Basically, Triton assumes that kernels use structured control flow (i.e. for, if-else, and no jumps). In contrast, the Rust compiler removes loops and conditionals in favour of jumps (and phi-nodes). When I told it this was what was happening, it happily reverse-engineered the for-loop and eventually did the same for the if-else. I still need to check the final IR emitted, but I was impressed.

This is great news, because most ML frameworks have a fairly large surface. There are a LOT of operations that are table stakes to be taken seriously. Quite honestly, I don't really enjoy implementing stuff like that.

I would rather be reading papers and understanding a new approach, and then integrating that. So I am probably going to delegate a lot more coding to Claude.

I also moved away from `beads` to `Linear` since it is cloud-friendly and lets me keep an eye on things from home. Setting up an automated workflow from Linear to Claude is a task for this week.

## Paper Reading: Tiny Machine Learning: Progress and Futures

I spent a bit of time each day reading this survey paper on the challenges and opportunities of TinyML. Once I have had a chance to fully digest it, I hope to create a presentation that I will share on LinkedIn.

## Safety-critical standards: MISRA C and Clippy

Nothing new to report, more reading of the spec. The weekly meetings have been a good forcing function to engage with content, because otherwise the week has been so hectic.

## RustWeek and Trade Shows

**RustWeek** is on the calendar in a more tangible way. If you’re going to **RustWeek**, message me—I’d love to grab a coffee and talk Rust, compilers, and edge ML.

I will also be attending a major manufacturing automation trade show this week (luckily, the city I am in is one of the biggest venues for trade shows outside London). Two other trade shows are coming in the next 2 months that I will also be attending. The main purpose is to get to know some of the vendors in the automation and edge AI space.

## Next week

The focus next week is on getting the classic **LeNet** model of Yann LeCun forward pass working (training will be next week).

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

**Note:** The next edition of this newsletter will be published on Monday, 27 April 2026. Stay tuned!

