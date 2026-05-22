# Rust to Silicon — Issue 008: YOLO26 on NVIDIA Jetson Orin Nano, RustWeek 2026, Edge AI Amsterdam, and Claude Co-founder

## New newsletter: This Week in Edge AI

I have launched a second newsletter: **This Week in Edge AI**.

It is a weekly digest of edge AI, embedded ML, and silicon news for engineers building real systems, published every Tuesday. The first issue covers practical edge inference guidance, FPGA updates, notable events, and Rust momentum in edge deployment.

You can subscribe here: [this-week-in-edge-ai.beehiiv.com](https://this-week-in-edge-ai.beehiiv.com/)  
You can read Issue 01 here: [This Week in Edge AI: Issue 01](https://this-week-in-edge-ai.beehiiv.com/p/this-week-in-edge-ai-issue-01)

## What I promised vs. what shipped

**Short version:** YOLO26 is running natively on the Jetson Orin Nano, with one-click `cargo` deployment.

Last week, I said the next key milestone was getting YOLO26 deployed and running on the NVIDIA Jetson Orin Nano. I am happy to report that the model is now running natively on the Orin, with one-click `cargo` deployment. That is a far better workflow than the usual Python export, copy, and configure TensorRT approach.

Performance is not great yet. I have scheduled two sprints for performance tuning (there are several obvious improvements), which should significantly improve throughput on the Orin.

## RustWeek 2026

This was my first RustWeek, and I was blown away by the scale of the event and the quality of the talks. It was nerd heaven.

The conference was held in the beautiful Dutch city of Utrecht. It was also my first time in the Netherlands, and I was really taken by the beauty and charm of the place: the cycling culture (I wish we had this in the UK), the historic old town, and a day trip to Amsterdam with serious Harry Potter and Diagon Alley vibes. Maybe I have read too much Tolkien, but I half imagine he had the Dutch in mind when writing the Elvish characters.

The Dutch have a beautiful and unique culture, and I will miss it when I get back home to the UK.

## Edge Impulse: Imagine Innovators

Luckily, this year's event was in Amsterdam, so I was able to attend after RustWeek. The presentations were high quality, and I spoke with several interesting people working on edge AI hardware and software.

You can watch the livestream on the [Imagine Innovators Europe](https://www.youtube.com/watch?v=cbao6A8pr1o).

## Claude Co-founder

I am sure many of us turn to Claude for all sorts of research and brainstorming. As a solo founder who struggles with procrastination and shiny-object syndrome, I wanted more discipline in my work. So I created a dedicated chat for daily accountability and keeping to a defined strategy.

Over time that chat grew very large, and I asked Claude to summarize it with all the key points so I could start fresh. In the new chat I explained that the main tasks for Q2/Q3 are building an MVP and then customer validation before going further. It asked a few clarifying questions and set up the new thread.

The Claude in the old chat was very supportive; if I pushed back on something, it usually folded. The new one asked whether every decision had to be tested before folding, and I said yes. The new persona is a hardass: it admonishes me for every deviation from the plan, constantly criticises my decisions, and asks for justification. I do stay closer to the plan, but the tone is toxic. I think I may have to break up with it.

## Safety-critical standards: In-person event

It was great to catch up with everyone in person, having previously only seen them on Google Meet. I was mainly in listening mode and did not contribute much.

A lot of the work is starting to come together. Over the next 12 months I expect important deliverables that will make it easier for Rust to be taken seriously in safety-critical systems. C/C++ will probably still be the first choice, but I hope Rust will not remain a distant second, as it often is today.

I had a quick chat with someone from the Ferrous Systems team about their safety-critical certified compiler, Ferrocene, as a potential front-end for my project in safety-critical machine learning use cases. It is a long road: it would require defining the semantics of Triton as has been done for Rust with FLS, and then certifying backends such as NVGPU and NVCC. But a path is starting to appear for when I am ready to take that seriously.

## Next week

Now that YOLO26 is working on the Orin Nano, the next step is to get the full parking garage demo running on the device.

The next sprint is dedicated to that. For this use case, the current model performance is already adequate (about 100 images/s). I also hope to show how Rust async can make the whole application simpler to write while keeping strong performance.

---

This is my weekly newsletter, sharing my journey building a high-performance Rust compiler stack for edge AI.  
Follow along for technical updates, lessons, and honest insights from the front lines.

If you are building compilers, ML infra, or edge AI systems, I would love to hear how you balance rapid AI-assisted coding with long-term code quality.

**Note:** The next edition of this newsletter will be published on Thursday, 21 May 2026. Stay tuned!

