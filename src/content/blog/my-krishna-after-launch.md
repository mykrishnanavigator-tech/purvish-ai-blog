---
title: "I Built My First iOS App. Here's What Happened After Launch."
description: "From chasing downloads to listening to users, rethinking My Krishna, and applying those lessons to enterprise AI."
date: 2026-10-26T05:00:00Z
image: "/images/beyond-the-launch-my-krishna-app.png"
author: "Purvish Shah"
categories: ["My Krishna"]
---

*From chasing downloads to listening to users, rethinking My Krishna, and applying those lessons to enterprise AI.*

When I started building my first iOS app, I had a pretty optimistic picture of what would happen after launch. I imagined publishing it on the App Store, sharing it with a few people, and watching the downloads grow. Maybe hundreds of users within the first few days.

After all, I had spent months learning, experimenting with AI, figuring out the architecture, fixing issues, and finally getting the app published. Surely, the hardest part was behind me.

I was wrong about that.

Building the app was challenging, but getting people to discover it turned out to be an entirely different problem. What surprised me even more was how feedback from a small consumer app began influencing the way I think about enterprise AI solutions.

## I Thought Launching Was the Finish Line

On August 8, I launched [My Krishna](https://apps.apple.com/us/app/my-krishna/id6782722854), my first iOS app. It's a personal growth and reflection application inspired by the wisdom of Lord Krishna. My goal was to create a space where people could ask questions, reflect on challenges, and find thoughtful guidance.

<div class="not-prose my-10 flex snap-x snap-mandatory gap-6 overflow-x-auto pb-4 md:grid md:grid-cols-3 md:gap-8" role="region" aria-label="My Krishna app screenshots" tabindex="0">
  <figure class="m-0 w-3/4 shrink-0 snap-center text-center md:w-auto">
    <img src="/images/loadingscreen.png" alt="My Krishna loading screen" class="mx-auto h-auto w-full max-w-60 rounded-2xl shadow-lg" loading="lazy" />
    <figcaption class="mt-4 text-sm text-text-light dark:text-darkmode-text-light">Loading screen</figcaption>
  </figure>
  <figure class="m-0 w-3/4 shrink-0 snap-center text-center md:w-auto">
    <img src="/images/welcomescreen.png" alt="My Krishna welcome screen" class="mx-auto h-auto w-full max-w-60 rounded-2xl shadow-lg" loading="lazy" />
    <figcaption class="mt-4 text-sm text-text-light dark:text-darkmode-text-light">Welcome screen</figcaption>
  </figure>
  <figure class="m-0 w-3/4 shrink-0 snap-center text-center md:w-auto">
    <img src="/images/sampleprompts.png" alt="My Krishna sample prompts" class="mx-auto h-auto w-full max-w-60 rounded-2xl shadow-lg" loading="lazy" />
    <figcaption class="mt-4 text-sm text-text-light dark:text-darkmode-text-light">Sample prompts</figcaption>
  </figure>
</div>

Getting the app approved and published felt like a huge achievement, especially after spending almost three weeks working through App Store rejections. Initially, I had only implemented Sign in with Google. During the review process, Apple recommended adding another sign-in option, so I added Sign in with Apple.

I had taken an idea and turned it into something people could download. I had already shared the development journey in [From AI Anxiety to Shipping My First iOS App](https://www.wisehoots.ai/blog/from-ai-anxiety-to-shipping-my-first-ios-app), so seeing the app live was a milestone I wanted to celebrate.

Naturally, I shared it with friends and family. A few people downloaded it, and I kept checking the numbers. Every new download was exciting because someone was actually trying something I had built from scratch.

Then the initial activity slowed down. I realized I had spent so much time figuring out how to build the app that I hadn't thought enough about how people would find it. I knew how to build software, but distribution, positioning, and attracting an audience were new territory.

## I Stopped Promoting and Started Sharing

I started exploring Reddit, watched YouTube videos to understand how people approached promotion, and experimented with Google NotebookLM to help create content about the app.

At first, my approach was straightforward: explain what My Krishna does, share the App Store link, and hope people would download it. But I began to see the problem. People encounter new apps and AI tools constantly. Why would someone stop scrolling just because I had built another one?

That question made me rethink what I was sharing. My Krishna hadn't started as a business plan. It started with my anxiety about how quickly AI was changing software development. Rather than continuing to worry, I decided to learn by building something real. The journey involved unfamiliar tools, architectural decisions, mistakes, and plenty of trial and error.

Maybe the story behind the app was more interesting than another announcement about its features.

So I wrote [From AI Anxiety to Shipping My First iOS App](https://www.wisehoots.ai/blog/from-ai-anxiety-to-shipping-my-first-ios-app). Initially, I published my writing through Notion, but it wasn't reaching many people. That led me to another idea: I was already experimenting with consumer apps and enterprise AI projects, so why not create a place to document what I was learning?

One of my Reddit posts about reaching 101 downloads received around **10,000 views**. That was encouraging, but what stayed with me were the conversations it sparked. People asked about Android support, questioned the login requirement, and shared their first impressions. Those responses helped me see the app through their eyes—and gave me a clearer sense of what to improve next.

![Reddit post about My Krishna reaching 101 downloads](/images/reditscreenshot.png)

[Visit my Reddit profile: u/ThoughtfulVoyager8](https://www.reddit.com/user/ThoughtfulVoyager8/)

That's how **WiseHoots.ai** started taking shape. I wanted it to be a home for the things I'm building, the decisions I'm making, and the lessons I discover along the way. I also shared [My Krishna Is Live](https://www.wisehoots.ai/blog/my-krishna-is-live), explaining more about the application itself.

As I began sharing the story on Reddit and publishing articles, I noticed more interest and additional downloads. I can't attribute each download to a particular post or channel, but the experience changed how I thought about reaching people.

**Instead of simply asking someone to try my app, I was giving them a reason to understand why I built it.**

## What My First 101 Downloads Taught Me

> **101 downloads.** Not a viral launch or thousands of users—just my first meaningful milestone as an indie app developer.

When My Krishna reached 101 downloads, I shared the milestone on Reddit and asked other indie developers how they had found their first 100 users. The number mattered to me, but the feedback I started receiving was even more useful.

Some people asked why they needed to log in before asking a question. Others wanted an Android version. A few assumed, from the name, that My Krishna was exclusively a religious app, even though I had intended it as a broader personal growth and reflection experience inspired by Krishna's wisdom.

These weren't the kinds of observations I had focused on while developing the app. I was thinking about architecture, functionality, and getting everything to work. Users were asking simpler questions: Can I try it immediately? Is it available on my phone? Is this app meant for someone like me?

The feedback showed me how easily a developer's assumptions can become part of the product without ever being tested. More importantly, it gave me concrete ideas for what to change next.

## What's Next for My Krishna: RAG, Memory, and a More Personal Experience

The first version of My Krishna was about learning how to build and ship an AI-powered iOS application. The next version I'm working on is about making the experience more accessible, more grounded in knowledge, and more meaningful over time.

- **Let People Ask Questions Before Asking Them to Log In**

  The login feedback stayed with me because, from my perspective, authentication had seemed like a natural part of the design. I was thinking ahead to personalization, saved interactions, and experiences that build on previous conversations. But a first-time user doesn't know whether the app will be useful yet. Asking them to create an account before they can explore it adds friction at exactly the wrong moment.

  In the next version, **users will be able to ask questions without logging in**. Authentication will still be required for features that depend on an ongoing, user-specific experience, including **persistent memory** and a **deeper-thinking agentic feature**.

  That feels like a better balance. People can experience the basic value first, while features that need continuity and personal context remain tied to an account. I'm not removing authentication entirely; I'm being more deliberate about where it belongs.

- **Build for Android and iOS**

  I initially chose iOS because I wanted to keep the scope manageable and actually finish the project. For a first release, that was a practical decision. But Android requests made me think about the people I might be leaving out.

  The next version is planned for **both Android and iOS**. India is an important potential audience for My Krishna given the inspiration behind it, and Android is widely used there and in many other countries. Supporting both platforms should make the application accessible to more people, although I'll still need real usage data to understand where demand is strongest.

  This is one of those moments where user feedback is helping me move beyond the decisions I made for my own development convenience.

- **Ground Answers in Hindu Knowledge Using RAG**

  The biggest technical change I'm exploring is **Retrieval-Augmented Generation (RAG)**. I want My Krishna to draw on a curated knowledge base of Hindu scriptures, philosophical teachings, and related source material rather than depending only on a language model's general knowledge.

  The approach I'm planning is to process and organize source material into meaningful passages, generate embeddings, and index those passages in a vector database. When someone asks a question, the retrieval layer would identify relevant passages, and an OpenAI model would use that context to help generate an answer.

  The goal isn't to make the response sound more authoritative simply because it mentions scripture. It's to make the guidance **more grounded and verifiable**, with appropriate references to the source material. That also means being careful about context, translation, interpretation, and differences among traditions. A useful system should distinguish what a source says from how an AI model interprets it.

- **Use Memory to Make Guidance More Meaningful**

  I'm also exploring persistent memory for authenticated users. Someone may return to the app over time with related questions about stress, focus, relationships, or personal goals. If they choose to use memory, the application could retain relevant context from earlier interactions so future responses don't always start from zero.

  But memory creates design responsibilities, not just technical opportunities. I need to think about what should be remembered, how users can review or remove that information, how long it should be retained, and how to avoid making assumptions based on old conversations. Personalization should help people feel understood without becoming intrusive or overly confident about their circumstances.

  The deeper-thinking agentic experience is another area I'm exploring. For more complex questions, I want the system to be able to retrieve relevant knowledge, consider permitted user context, and work through the question more deliberately before responding. I still need to evaluate how much additional complexity actually improves the experience—and whether the latency and cost are justified.

  These are **features in development and architectural plans**, not capabilities I'm claiming are already available in the current App Store release. The challenge is to build them thoughtfully without turning a simple question-and-answer experience into something complicated for the user.

## How My Krishna Is Changing My Enterprise AI Thinking

When I was building My Krishna, I spent most of my time thinking about how the application would work—the architecture, authentication, AI responses, and getting it onto the App Store. After launch, users asked questions that had little to do with those technical decisions. Why did they need to log in before trying it? Could they use it on Android? Was the app meant for them?

Those questions made me pause. I had spent months making the application work, but I hadn’t given the same attention to how someone would discover it, try it, and decide whether to return. That realization followed me back into my enterprise work. Before choosing an architecture or adding an AI capability, I need to understand what people are trying to accomplish and what makes their work difficult.

In my **shared-mailbox AI agent project**, for example, the business needed a better way to manage incoming requests. Emails had to become trackable tasks, with enough information for the right team to take ownership. One specific requirement was identifying the region associated with each request. We used the country code in the sender’s email signature to help determine the region and tag the task automatically. It was a small part of the solution, but it removed a manual step the business wanted addressed.

Building My Krishna gave me a more personal appreciation of that distinction. As a developer, I can become absorbed in what I’m able to build. The person using it is thinking about whether it helps them get something done. I’m carrying that lesson into the next version of My Krishna too. RAG, memory, and agentic capabilities interest me technically, but each needs a clear purpose. I still need to test whether they make the guidance more useful and whether that improvement justifies the extra complexity.

**I’m learning to spend more time understanding the problem before deciding how sophisticated the solution needs to be.**

## Lesson Learned

**I started this journey thinking the biggest challenge was learning how to build with AI. Now I'm realizing that understanding people is just as important as understanding the technology.**

And that's a lesson I want to carry into every application I build next.

---

## The App That Started This Journey

If you're curious about the current version, you can explore [My Krishna on the Apple App Store](https://apps.apple.com/us/app/my-krishna/id6782722854). I'm still learning from the people who try it, and I appreciate thoughtful feedback.

If you're building an application or working on enterprise AI, I'd love to hear your experience: **What's one thing you learned only after putting your software in front of real users?**

### More From My Journey

**Building My Krishna**

- [From AI Anxiety to Shipping My First iOS App](https://www.wisehoots.ai/blog/from-ai-anxiety-to-shipping-my-first-ios-app)
- [My Krishna Is Live](https://www.wisehoots.ai/blog/my-krishna-is-live)

