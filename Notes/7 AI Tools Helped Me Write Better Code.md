---
tags:
- editors
---
## **7 AI Tools Helped Me Write Better Code

Coding can be hard sometimes, especially with bugs that are tough to fix.

I tried a lot of AI tools in 2024 but only 7 of those made sense for my developer workflow. The ones that actually helped me write better code.

Right now, I'm only using a couple of those but each tool on this list is worth it.

Let's understand how they helped me and how they can do the same for you.

___

## [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#1-qodo)1\. [Qodo](https://www.qodo.ai/)

[![[fa5eb0921ebc5371d8d5252e9bdff2ca_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fxaiyy0hqn49483w6mvto.png)

I've always heard that testing should be the main focus and any code that is not tested is unreliable.

I believe a little knowledge of the codebase and automating the testing part is important because it might be overkill in other cases as there are different thresholds for people to ensure that the app works correctly.

That is where I came across [Qodo (previously known as CodiumAI)](https://www.qodo.ai/) and it was damn useful.

It's a developer AI tool that generates meaningful tests for code. It analyzes your code, docstring, comments and then suggests tests as you code.

It's super handy for properly testing complex stuff. It mainly provides:

\-→ `Qodo Gen` : Define the coverage goal and qodo generates the tests accordingly. Detect bugs and document them.

\-→ `Qodo Merge` : Make PRs less painful by providing reviewers a simple walkthrough and giving code suggestions ranked by severity.

Watch this quick 1-minute demo of how Qodo helps you get zero bugs!

<iframe width="710" height="399" src="https://www.youtube.com/embed/FYy9jtDudLo" allowfullscreen="" loading="lazy"></iframe>

You can download it from [VSCode Marketplace](https://marketplace.visualstudio.com/items?itemName=Codium.codium) and [JetBrains extension](https://plugins.jetbrains.com/plugin/21206-codiumai--meaningful-tests-in-python-powered-by-testgpt).

You would have heard about popular tools like PR Agent (for reviewing PRs) and Codiumate, they were made by the same team.

[![[8b9bc770d992e3989af21a128c611077_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fbd21sbjod01o4zkyz79v.png)

Check the [official docs](https://docs.codium.ai/) and read the difference between [CodiumAI vs ChatGPT](https://www.codium.ai/codiumai-vs-chatgpt-4/) by comparing the power to generate unit tests.

### [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#right-now-what-am-i-using-qodo-for)🎯 Right now, what am I using Qodo for?

I'm mainly using it to validate the code by generating the tests since it's easy with context awareness. I haven't used it for every project but it's easier to use Qodo whenever I work with a new codebase (open source project).

Qodo is completely open source with all of its tools. You can check the repo below!

[Star Qodo ⭐](https://github.com/Codium-ai)

___

## [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#2-cursor)2\. [Cursor](https://www.cursor.com/)

[![[315dbd109d6ca21408032fac29d4edf7_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fozl4568027b86ib1dg2r.png)

I have used VSCode for years and avoided AI editors due to a perception that AI-written code would take longer to debug. I assumed that it would just cancel the productivity but I gradually realized how wrong I was.

The problem is there are so many choices for AI-based editors like [Cursor](https://www.cursor.com/), [Continue](https://www.continue.dev/), [Zed](https://zed.dev/), [Void](https://voideditor.com/), [PearAI](https://trypear.ai/) and I'm sure there are many more out there.

I was skeptical at first, but I chose Cursor because many developers on Twitter were talking about it (maybe the hype got to me).

In my experience, Cursor actually understands your project, unlike other editors who just say it for the sake of saying it.

It gets your coding style, knows your project structure and even picks up on your team's best practices. It's just that good.

It's a fork of VS Code so you can just import the settings, themes, keybindings and extensions to maintain the same experience. The switch is very easy which is why developers started using it.

[![[67d89280a6e7b24c21600faed9e09e1c_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F37ch0513k3p5hwosijq4.png)

developers using cursor every second

I've used almost all of the features and was stunned. Let's briefly outline a few features with demo examples.

⚡ Tab

Traditional auto-complete doesn't work that well, the Tab feature in Cursor is constantly working behind the scenes, analyzing your existing code and predicting your next move.

It's very accurate because it tracks your recent changes and the overall context of your project.

![[3bf0e8d38aa3d152f54ea0519b1289d7_MD5.gif]]

next level code generation

![[890dbbe5858716873dd04491240125cd_MD5.gif]]

Intuitive cursor prediction (super accurate)

⚡ ⌘ K

This command shortcut puts the full power of AI-assisted coding which can help you achieve code generation, refactoring a big chunk of code and so much more.

![[f780293eafa73cb49edfaf7e84405359_MD5.gif]]

code generation on demand

![[2f654ffb6882162dfe97139968e9facf_MD5.gif]]

quick questions to get fast answers

⚡ Terminal

The editor extends to the terminal and you just have to use ⌘ K in the terminal.

For example, instead of trying to remember the exact `find` command syntax, you could just type `Find all files added in the last 24 hours` and let Cursor do the heavy lifting.

![[ef9b58b5dbb0edce57bbc533d2323243_MD5.gif]]

terminal

⚡ Chat

The cursor understands what file you're in and where your cursor is. It's like chatting with a dev who's looking at your screen. These conversations are context-aware which makes them far better.

![[32161a05430381c966cfeeb6b77a7c99_MD5.gif]]

context aware conversations

![[8f9cd83056f9806ad09357bdf00aefd1_MD5.gif]]

visual context with image support

⚡ Composer

This is one of the most crazy features and can help generate an entire app from scratch. Yes, complete the functional codebase in minutes with all the necessary imports and boilerplate code.

![[ec87ead8bbd5a036339e40923943ceb9_MD5.gif]]

generating entire app using composer

If you're curious to know more features, models and terminologies like context or AI review, you can explore on the [official docs](https://docs.cursor.com/get-started/migrate-from-vscode).

When I was starting, I just read the blog [The Ultimate Introduction to Cursor for Developers](https://www.builder.io/blog/cursor-ai-for-developers) by the Builder.io team. This is a complete guide and is highly recommended!

### [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#right-now-what-am-i-using-cursor-for)🎯 Right now, what am I using Cursor for?

I'm building my portfolio and using it to fix small bugs mainly for complex frontend work. Cursor is now my default editor and I believe that it improves productivity. I just might take the pro plan as well :)

[Star Cursor ⭐️](https://github.com/getcursor/cursor)

___

## [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#3-chatgpt)3\. [ChatGPT](https://chatgpt.com/chat)

[![[fc1330abb1058953f95fd5fd2c5df2f1_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fef6sig7uib1h3piabt58.png)

I remember a time in my project when I was stuck on a problem. I went through 50+ Stack Overflow threads and even asked senior developers. That’s how frustrating it was!

Then ChatGPT came along, making it easier to find information. It could’ve solved that issue much faster. Of course, when ChatGPT first launched, it wasn’t great at writing code. It took a few tries to get useful answers.

With new models like GPT-4o and GPT-4o mini, it has become much better and now has a memory with context to provide more accurate answers.

At first, I used ChatGPT and DevGPT (which now limits you to 10 requests) to cross-check answers. But I eventually stopped using DevGPT.

Today, ChatGPT is way more advanced, with plugins and agents making them even more powerful.

[![[3c36a42792af3ec8cee6eb971e3db924_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F48hjtmqxx1l3uwzoqakh.png)

For instance, you can use DALL・E to generate a cover image based on your prompt. You can find all the agents at [chatgpt.com/gpts](https://chatgpt.com/gpts).

[![[39d7a3d6746501353c0f1f41391d3696_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fu3igmrmvbsmx2gryxhst.png)

### [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#right-now-what-am-i-using-chatgpt-for)🎯 Right now, what am I using ChatGPT for?

To be honest, I mainly use it for usual tasks like understanding code or quickly finding new information. I used it a lot in the beginning, especially for coding and manual work, when it was first released. But now, I don’t use it as much for coding.

[Visit ChatGPT 🔥](https://chatgpt.com/)

___

## [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#4-perplexity)4\. [Perplexity](https://www.perplexity.ai/)

[![[5f89c4eac0e2bb56f6fdefeb63b15b4a_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F1b8rb3snuvutbo8vggxb.png)

Whenever I'm stuck with a coding problem, Perplexity is usually my first stop. It’s like a smarter, faster search engine that gives clear answers without making me sift through a bunch of links.

I prefer Perplexity over other search engines like Bing or Google because those are often filled with ads. On Perplexity, every answer feels direct and backed up with sources.

[![[95e697f3f1af0ad0eb2f227654b1dbb6_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F5k23uwx13ymlegzypkxn.png)

starting dashboard looks like this

This briefly outlines a few features:

⚡ There are six modes to accomplish different needs.

[![[b2e251f6979cd277f8787ffa10e3b130_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Feguu9m0kw83rgb4ccnpc.png)

[![[2758b905d0d2a4c41911860647b3b752_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fsgy1tnzjutwvek7xuqv4.png)

response through video mode

⚡ You can also fill up basic info to get better personalized answers.

[![[7d2fdca1a0330cf868911fc963489a20_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fztydhvpmhh7jghydvcjs.png)

⚡ You can create a custom space where you can organize information in a much better way. You can later upload files (ppt, pdf, word, excel) as a source for your knowledge database. Then you can invite collaborators to brainstorm and work together on cool ideas.

[![[47ceba24cedf19686e807cd30d193275_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F4tf2n5jrmohabypaw48h.png)

[![[ca82f62875f9ef05029f0b327d180996_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fi00zvqh76tn36lo3cbnq.png)

⚡ You can discover new stuff to remain updated (don't really use it) and bookmark it for later.

[![[e89d8f1540e10e604c68d7602c5e7bac_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fivrrd8yxxf81ek1bheia.png)

⚡ With any query, you can search for images and videos (on the right side). You can also check all the sources and see which ones are used for each point individually.

[![[0e94436350b05d7486d332d5af37aa05_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fjaao0wa49jzs52mz7c1g.png)

all the sources

[![[861988f548e1682a638329d04bdd0862_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fkqseowlxh3jh5ydz6ff1.png)

points summarized from which sources are clearly shown

I started using it because the user interface is very easy to pick on and the features just back that simplicity.

There is also an open source alternative of Perplexity which goes by the name of [Perplexica](https://github.com/ItzCrazyKns/Perplexica/). It uses advanced machine learning algorithms like similarity searching and embeddings to refine results and provides clear answers with sources cited.

They use SearxNG to stay current and has also 6 focus modes. You can definitely learn a bunch of stuff from the codebase.

### [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#right-now-what-am-i-using-perplexity-for)🎯 Right now, what am I using Perplexity for?

Using it to get clear, direct answers rather than sifting through multiple Google links. Plus, endless follow-ups make it convenient for complex queries.

[Visit Perplexity 🔥](https://www.perplexity.ai/)

___

## [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#5-pieces)5\. [Pieces](https://github.com/pieces-app)

[![[f2ba3b605af5cebbdead7441c2478b99_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fefl75wryto4poto0zdbe.png)

A few months ago, I saw all the hype about Pieces on Twitter and decided to try it out.

It's an AI productivity tool designed to help developers organize their chaotic workflow. What sets it apart is its completely offline approach to AI, which gives a strong sense of privacy.

The best part is their full ecosystem, which includes a powerful desktop app called Pieces OS, a Chrome extension for transferring snippets, and a VSCode extension. When used together, they make a really powerful setup.

Pieces OS uses local LLMs, so everything runs 100% locally on your machine, though you can connect to the cloud for backups, sharing and using cloud-based LLMs for code generation.

[![[1b0be62dc110faf17faba6088d39854e_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fgh090r1ajdltjwtdhky8.png)

✅ I tried it for the live context which is basically hyper-aware assistance to guide you right back to where you left off. Like you can ask, `What was I working on an hour ago?` and it will give you all the details.

✅ You can even browse docs (web browser) and let the AI learn from them. Then you can ask questions and it will answer using those docs.

You can see the complete [list of features](https://pieces.app/features/) that is available with Pieces.

I even covered a lot of interesting use cases with demo examples in the blog about how [Pieces is the only AI tool you need to be a 10x developer🤯](https://dev.to/anmolbaranwal/pieces-is-the-only-ai-tool-you-need-to-be-a-10x-developer-13le).

<iframe width="710" height="399" src="https://www.youtube.com/embed/aP8u95RTCGE" allowfullscreen="" loading="lazy"></iframe>

### [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#right-now-what-am-i-using-pieces-for)🎯 Right now, what am I using Pieces for?

I'm not using it right now, but I used it for a few months when working on many projects. As I said earlier, it's more powerful when you use the full ecosystem (browser extension + desktop app + VS Code extension).

Pieces is open source with all some of its tools.

[Star Pieces ⭐️](https://github.com/pieces-app/)

___

## [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#6-mintlify)6\. [Mintlify](https://github.com/mintlify/writer)

[![[f5f253d2f80674c2956fe8fdf4ad5fc4_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fgvk07kmn8p48cpssogov.png)

I understood the importance of documentation as a developer. But it's a lengthy process and things can get messy sometimes.

I was looking for a solution and came across Mintlify which uses AI to help you document the code in just a few seconds.

You can watch this video for the complete walkthrough!

As you can see, you just have to highlight the code or place the cursor on the line you want to document. Then click on the `Write Docs` button (or hit ⌘ + .)

It supports more than 10 major programming languages and a lot of docstring formats like JSDoc, reST, NumPy and more.

It was simple and automatically documents the code as you write so it was quite handy.

[![[1399802cf9bbd030bb8433b73d3a8fc3_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fo1kxyvzei1afkr8n37m2.png)

You can install the [VSCode extension](https://marketplace.visualstudio.com/items?itemName=mintlify.document) or find it on [IntelliJ](https://plugins.jetbrains.com/plugin/18606-mintlify-doc-writer). You can read more on their [website](https://writer.mintlify.com/).

### [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#right-now-what-am-i-using-mintlify-for)🎯 Right now, what am I using Mintlify for?

I mainly use it to document code for open source projects. I skip it when working solo on a codebase (unless it's complex) since I don’t see the need for documentation in that case. Overall, it’s much faster than starting from scratch.

Mintlify is open source.

[Star Mintlify ⭐️](https://github.com/mintlify/writer)

___

## [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#7-continue)7\. [Continue](https://github.com/continuedev/continue)

[![[3f29c9b5b768963fe85e7aab10b4e756_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fo5x02ly3eahicb5kmdk1.png)

I didn’t have a specific reason, just decided to try Continue as an AI coding assistant while working on a blog. It didn’t disappoint for sure.

The main reason might have been working with local LLMs to save some bucks. Plus, it can take context in the form of codebase, issues, docs and even files.

[![[affd6b86fbfb8296c73d7367b7b23484_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Ftnpql9mhwvfq622wawhl.png)

You can connect any models and any context to build custom autocomplete and chat experiences inside [VS Code](https://marketplace.visualstudio.com/items?itemName=Continue.continue) and [JetBrains](https://plugins.jetbrains.com/plugin/22707-continue-extension).

You can easily set Ollama with Continue, here are the snapshots of when I was installing it.

[![[7ad162e59df1fe3cc70d7ddedc8c235a_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Frq5ld2djixiv5pmz8zzx.png)

Step 1

[![[30449c5545f3260e4f85c1047f677ca5_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fj9u0lan7koa5sjtysykw.png)

run it through terminal

[![[67b041a50f18e5a3f0ebfef17fcdf138_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fduhhgmg2eqr1tk1r2ecy.png)

step2 complete

[![[e4ffee8a404e1026865298ab51ebe588_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fwzufhvtre8o97wq3zqlr.png)

run it through terminal

[![[0c6a408777fb9285176679c6fe92ef3f_MD5.jpg]]](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fnd4lu8r0shiah1v7odq0.png)

step3 complete

It's that simple. After you have configured it, you can use all the amazing concepts like:

⚡ Tab feature to autocomplete code suggestions.

⚡ Asking questions about your codebase.

⚡ To understand terminal errors immediately.

⚡ Kicking off actions with slash commands.

⚡ Refactor functions where you are coding.

If you're still curious, you can watch this [YouTube video](https://www.youtube.com/watch?v=V3Yq6w9QaxI) and find all the info on the [docs](https://docs.continue.dev/intro).

### [](https://dev.to/nozibul_islam_113b1d5334f/must-know-algorithms-3735#right-now-what-am-i-using-continue-for)🎯 Right now, what am I using Continue for?

I switched to Cursor since it covers most of my needs. Still, Continue is a good option if you want to avoid cloud subscription costs and rely on local LLMs (it might be slower but it's worth it).

[Star Continue ⭐️](https://github.com/continuedev/continue)

___

These tools made coding feel less like work (we all know coding can get tough) and more like magic. Qodo and Cursor are my favorites on the list.

Did you use any other AI tools? Let us know in the comments.

Have a great day! Till next time.

You can join my community for developers and tech writers at [dub.sh/opensouls](https://dub.sh/opensouls).

![[74b5af76c33b2e3d2f5e28612f683add_MD5.gif]]

[[Code Editor]]  [[GPT]]