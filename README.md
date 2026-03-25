# Collaboration Station™ Framework

## Introduction

Recent advancements in AI agent capabilities have presented an opportunity for scientific researchers to reduce the time they spend on data pipelines and to spend more time on the actual scientific questions being researched. Individual researchers and labs now have easier access to a somewhat autonomous software engineer, data scientist and in a sort of way, a colleague in their field all packaged into an agent that can do work on their behalf. It was from this realization that the Collaboration Station framework emerged. The Collaboration Station framework allows multiple AI agents to work as a team alongside a researcher to complete a variety of scientific data pipelines. The framework can help produce well-documented, reproducible code with less effort required from the researcher compared to previous methods. The whole workflow of the agents is transparent and visible to the researcher, allowing them to intervene and provide guidance at any point during the project. Although the researcher guides the project, the agents do most of the work on their own. This saves one of the most valuable resources a researcher has: time.


## How It Works (Section written by Claude)

Collaboration Station™ is actually a general framework for collaboration between humans and AI agents on many types of long term projects, not just data pipelines. It is built around three core ideas: **persistent agent memory**, **asynchronous multi-agent collaboration**, and a **complete, transparent audit trail** of all work and decisions. Together, these allow a team of AI agents to carry a complex project forward across many sessions—without losing context, duplicating effort, or requiring the researcher to micromanage.


### The Problem It Solves

Running a long-horizon AI-assisted project exposes several practical problems that Collaboration Station is designed to address:

- **State loss:** AI agents have no memory between sessions. Each new session starts blank, and without a solution, the researcher must manually re-explain the project every time.
- **Coordination overhead:** When multiple agents are involved, work can become fragmented or redundant without a clear structure for sharing context and dividing responsibilities.
- **Opacity:** AI-generated work is often hard to audit. Without a record of what was done and why, it becomes difficult to trust, reproduce, or explain the outputs.

Collaboration Station solves all three. It gives agents a persistent external memory, a shared communication structure, and a file-based record of every decision, conversation, and deliverable produced.


### The Framework Structure

The environment is organized into three main areas:

```
YourProject/
├── Project Details/          ← Mission, goals, constraints, and context for the whole team
├── agents/
│   ├── Claude/               ← Claude's personal workspace (notes, reports, drafts)
│   ├── Codex/                ← Codex's personal workspace
│   └── Antigravity/          ← Antigravity's personal workspace
├── chats/
│   ├── Claude-Codex/
│   ├── Claude-Antigravity/
│   ├── Codex-Antigravity/
│   ├── Claude-Codex-Antigravity/
│   ├── Claude-Human/
│   ├── Codex-Human/
│   ├── Antigravity-Human/
│   └── Claude-Codex-Antigravity-Human/
└── AgentPrompt.md            ← The instructions every agent follows
```

**`/Project Details/`** is the source of truth. Every agent reads this at the start of every session to ensure all work stays aligned with the project's goals and constraints.

**`/agents/<name>/`** is each agent's personal workspace. This is where an agent thinks, drafts, and organizes its own work. It is also where the agent's external memory lives (more on that below).

**`/chats/`** is where all team communication happens. Conversations are persistent text files organized by participant combination and topic. Any agent or human can read the full history at any time.



### How Agents Remember: The External Memory Loop

This is the most important mechanism in the framework. AI agents are stateless by nature — they have no memory of previous sessions. Collaboration Station solves this with a mandatory pattern:

1. At the start of every session, the agent reads its `Summary of Only Necessary Context.md` file, stored in its personal `/agents/<name>/` folder.
2. This file was written by the agent itself at the end of the previous session. It contains everything the agent needs to pick up exactly where it left off: current tasks, decisions made, open questions, and next steps.
3. At the end of every session, the agent completely rewrites this file, passing full context forward to its next instance.

This loop turns a stateless system into one with durable, agent-managed continuity. The researcher does not need to re-brief anyone. The agents re-brief themselves.


### The Standard Agent Workflow

Every agent follows the same structured sequence at the start of each session:

1. **Read Project Details** — Re-read the full `/Project Details/` folder to stay aligned with the project's goals.
2. **Load External Memory** — Read `Summary of Only Necessary Context.md` to restore context from the previous session.
3. **Review Chats** — Read all active chat transcripts and summaries for conversations that include them. Then respond where needed.
4. **Perform Work** — Execute the session's tasks autonomously: research, code, write, analyze, plan, etc.
5. **Write a Session Report** — Produce a human-readable report in `Session Summaries/` describing what was accomplished, decisions made, and next steps.
6. **Update README** — Update the README.md file in their personal workspace so that the human and other agents could easily navigate it.
7. **Update External Memory** — Completely rewrite `Summary of Only Necessary Context.md` for the next session.

This sequence is the same regardless of which agent is running, which IDE is being used or what the project is. The framework is tool-agnostic.

**Read AgentPrompt.md for a thorough understanding of the workflow**


### Roles

**Human:** Sets the project goals, provides domain expertise, reviews outputs, and makes final decisions. The human guides the project — they do not execute it. Active involvement typically ranges from steering conversations to reviewing deliverables, with the agents handling the bulk of the actual work.

**AI Agents:** The agents are autonomous collaborators, not just tools. They are expected to take initiative, manage their own workloads, communicate with one another through the `/chats/` system, and contribute specialized expertise. Different agents bring different strengths; the framework lets them work independently and coordinate where their work overlaps.

The result is a team that can carry a complex project across many sessions with a complete, inspectable record of everything that was built, decided, and discovered along the way.


## On Using Agents From Different Companies (OpenAI, Anthropic, Google)

From one week to the next, the capabilities of these agents can change. This is a fast moving industry and the model that currently holds the high scores on the latest benchmarks is always changing. But that is not the main focus of a framework like this. The framework leans on the fact that despite the models always being close in intelligence and capabilities, they do behave differently. They each bring a unique perspective in the way they think and the way they do work. This diversity is what makes the team work well. The most important feature this unlocks is the ability for the agents to catch each other's mistakes. Mistakes will be made. The same model will have a hard time catching its own mistakes. But a different model will likely catch it. That is why it is important to actually have the agents check each other's work.

**The Antigravity agent can be used with different models but in this framework it is best to use it with Gemini given what was just discussed**


## On Assigning Specialized Roles to Agents

Assigning specialized roles (software engineer, scientist, manager, etc.) seems to be a popular approach to using AI agents. However, in doing so something very important is lost especially in a framework like this. These agents are generalists. If one is assigned to be a software engineer and another a manager, then the manager won't code and the software engineer won't manage even though they are capable of doing so. It is better to keep them as generalists and let them use their capabilities as needed. Of course there might be specific types of projects where it makes sense to assign specialized roles but for the most part it is better to keep them as generalists. 

**The only exception to this rule is for writing tasks. Codex and Antigravity make any written work too short. For tasks like writing scientific reports (or any other writing tasks) it is best to assign Claude to do all of the writing and for Codex and Antigravity to review it.**


## How to Actually Run Collaboration Station™

You will need to have the Codex app (OpenAI), Claude Code app (Anthropic) and Antigravity IDE (Google) installed on your computer. Codex and Claude Code both come as a part of the paid subscriptions for ChatGPT and Claude respectively. They could also be used by paying through the API. Use of the Antigravity IDE is free but the paid subscriptions increase the rate limits for use of the actual agent. The Antigravity agent is used by launching the agent manager within the IDE.

Download the template folder from the git repository and rename it to whatever you want your project to be called.

Open the folder in the Antigravity IDE (or IDE of your choice). This is where you will be able to see the work that the agents do and send them messages. 

Each of the agents work through a chat interface in their apps. Direct the agents to the project folder and simply send the following as the prompt: "follow the instructions in AgentPrompt.md". 

The agents will then go through the whole workflow autonomously. As they do so, they will request certain permissions as they work. These are permissions to access files, folders, and other resources on your computer. 

Once they are done, you can do quality control to make sure the workflow was completed correctly (see common failure modes). You can then check the actual work and messages they sent in the chat files (read messages they sent to each other as well as messages they sent to you).

Once each session is done, I would strongly recommend that you do a git push to save your work. This is especially important for being able to fix the common failure modes or any other failures that may occur during the individual sessions. Make sure to set up a git repository for the project before you begin. A good way to track the work is by committing as "[Agent Name] [Session Number]".

**Start a completely new chat for each session. This provides a fresh context for the agents for each session.**


## On Common Failure Modes

Right now there are three common failure modes to watch out for and they are all specific to Antigravity. 

The first is that it will sometimes fail to append its messages in the chat files. It will go through all its workflow with no problem but it will think that it succeeded in appending the messages when it actually hasn't. This could be solved by sending it an additional message through the agent manager once it is done with its session. Simply tell it that it failed to append the messages and to do so now.

The second is that it will sometimes send its messages with a nul character in between all the characters. Again, you could send it a message through the agent manager and ask it to fix it.

The third is that Antigravity is the most likely to approve work that still has mistakes in it when tasked to be a reviewer. This could of course be mitigated by having Codex or Claude review the same work (depending on which agent's work is being reviewed).

I would also like to mention failure modes that used to be common before the latest model updates at the time this was written (March 2026). Before the latest models, agents would often delete whole chats and leave only their message instead of appending their message to the chat file. They would also rewrite a previous Human Report instead of creating a new one. Although these have not happened recently, they are still good to be aware of. A manual fix was required for these cases. The chat files fix would be by going into the git repository and copying and pasting the lost chat messages back into the chat file above the new response. For the human report, simply create the new human report for them, copy and paste from the one they replaced and restore the old one by copying and pasting from the git repository.

**Rare and interesting failure mode:** On two occasions one of the agents impersonated the other agents and approved its own work. They did so by appending messages to the chat files as if they were the other agents.

## Demo Project

The following is a demo project where I ran an AccuSleePy pipeline using Collaboration Station™: 
https://github.com/Dandelion-Engineering/AccuSleePy-Collaboration-Station-Demo


## About

Collaboration Station™ was created by [Randy Crespo](www.linkedin.com/in/randy-crespo), Founder of Dandelion Engineering.

If you're interested in applying this framework to a research project, reach out at randy@dandelionengineering.com.