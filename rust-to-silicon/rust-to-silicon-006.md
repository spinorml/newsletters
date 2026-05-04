# Rust to Silicon — Issue 006: First major milestone, reflections on “Agentic Software Engineering,” and YOLOv26 is a go!

## What I promised vs. what shipped

Short version: MNIST end-to-end training is done (thanks, Claude), and the partner manager at Ultralytics has asked me to come back with a demo.

Last week I said the next move was to get the classic **LeNet (MNIST)** model by Yann LeCun running a full forward pass. In the end I got both forward and backward working (using the Adam optimizer). Much of this code was written by Claude, which continues to be incredibly impressive. I will share my take on this new paradigm of “Agentic Software Engineering” later.

I did not go to the cybersecurity event after reviewing all the companies exhibiting. I only found two that were a partial fit with the kind of firms I wanted to speak to, so I decided my time was better spent building than on a low-yield afternoon wandering the venue.

The other highlight of the week was the ESD Tech Forum virtual event organised by Gina Roos. It brought together many industry leaders, among them Steven Tateosian (Infineon), Mike Fitton (Altera), Sam Groves (MIPS), Henrik Flodell (Alif Semiconductor), and others from Qualcomm,NXP, Synaptics, and elsewhere. It was great to see the sheer pace of innovation in edge AI (processors and NPUs). The next few years are going to be incredibly exciting.

I also had a really good conversation with François Piednoel de Normandie of Athos Silicon about the safety-critical automotive ecosystem and some of the barriers to adopting Rust (compiler certification, coding standards, tooling, and so on). We also talked about autonomous systems as their chip is designed with safety-first in mind; he is fairly pessimistic about broad approval given safety concerns over hallucinations in neural-network-based systems. I am more positive: I see autonomy in automotive as a journey, and I expect it to accelerate seriously over the next decade.

After a positive response from Ultralytics, I have committed to delivering a compelling demo of **YOLOv26** (parking management) on an NVIDIA Jetson Orin by the end of Q2 (30 June), with the full toolchain in Rust—that is, model, training, and inference.

The demo will only be compelling if performance is on par with TensorRT and deployment is much easier. Today the rough path is model export, TensorRT config, and integration into a C++ application. My aim is to show the whole thing can be done in Rust.

## Reflections on "Agentic Software Engineering"

The whole field of software engineering is changing, with some doom-laden scenarios in which developers become obsolete. I am not going to predict exactly how the industry will evolve, because so much will depend on trend-chasing, executive incentives, and a myriad of government regulations.

One thing we must accept is that tools like Claude are incredibly good at coding. I would put its skill level at senior developer or above.

That is the uncomfortable part. The encouraging part is that the solution space for any real problem is huge, which means developers will need to think more like architects. The strongest engineers will be those who can steer tools like Claude toward a solution that satisfies a myriad of functional and non-functional requirements (including budget, tech stack, and so on). We already know that asking Claude for a plan before it implements anything, and getting it to ask clarifying questions first, consistently leads to better results. Those are skills humans are still very good at.

The other thing I have noticed is that my knowledge now has to run deeper in the domains I work in. In the past, because I was also doing the coding, I could spend a lot of time “just” writing code. Today I do not have to write as much of it by hand.

As a practical example, for the YOLOv26 work I expect to be able to prompt Claude to stand up the core algorithm end-to-end in about two weeks. You might object that Ultralytics took much longer than that—but that Rust-first implementation alone will not move the market (unless you are a Rust enthusiast). The hard problems in embedded and edge software are packaging and deployment, performance, security, over-the-air updates, and the rest. Unless I can deliver on those, nobody in the industry will care. I cannot simply prompt Claude to solve them. I need to understand current pain points, brainstorm approaches with it, have it implement candidates, then test and iterate. I need expert-level judgment on kernel optimisation so I know which fusions to pursue and how the system will behave across different hardware.

Finally, in an economic sense, code is about to get a lot cheaper to produce. That was not true before: software was incredibly expensive to build well. The set of industries that can afford serious software will grow fast. That is a net positive for the profession—assuming we agree that agents cannot run the show alone.

## Paper Reading: Tiny Machine Learning: Progress and Futures

I spent most of the week reading YOLOv26 papers, and have commited to a presentation at the nPlan paper reading group. The talk will be based on this paper "YOLO26: A Comprehensive Architecture Overview and Key Improvements - Hidayatullah, et al (2026)".

## Safety-critical standards: MISRA C and Clippy

I missed this weekend’s session because it clashed with the ESD Tech Forum, but I am continuing through the specs and will be ready for the in-person session in three weeks.

## RustWeek and Edge Impulse AI

**RustWeek** is on the calendar in a more tangible way. If you are going to **RustWeek**, message me—I would love to grab a coffee and talk Rust, compilers, and edge ML.

I will also attend the Edge Impulse AI event in Amsterdam on 20 May (as luck would have it, I will already be in the Netherlands for RustWeek).

## Next week

Getting naive YOLOv26 inference and training working end-to-end on a small COCO128 dataset.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published on Monday, 11 May 2026. Stay tuned!

