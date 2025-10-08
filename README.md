# Visual Studio Code and GitHub Copilot Starter Kit

A repo to demo ways to enhance your Visual Studio Code + GitHub Copilot developer experience.  

We aim to show how a developer can progress back and forth from "Vibe Coding" to "Spec Driven Development" - by taking advantage of different modes of work in the age of AI Assisted Development. 

## Long Term Resources:

- [Full GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [Github Copilot in VS Code Docs](https://code.visualstudio.com/docs/copilot/overview)
- [VS Code Release Notes (August)](https://code.visualstudio.com/updates/v1_104)


## Crawl

### Chat/Ask Mode

If you're familiar with something like OpenAI's ChatGPT, Claude or Microsoft Copilot experience - then you're already in the beginning phase of AI Assisted Work.  Chat Mode (or "Ask" mode in VS Code) is exactly as it is named - it's the ability to converse with the coding Assistant (e.g. GitHub Copilot) in a Q&A like format - where you can ask it information about your codebase, general/advanced coding "best practices" or use it as a sounding board or advisor to anything you may have in mind.  It has the capability to generate code, but it's in the chat window in a codeblock but you must manually copy/paste or use the UI element to inject it into your current cursor position in the highlighted code editor tab.  Nice...but not super convenient depending on how you like to work.

### Inline Edit/Code Completions/Next Edit Suggestions (NES)

Next up is the Inline Edit/Code Completions and Next Edit Suggestion Modes.  I'm going to to generalize them into one experience - in that it stems primarily from direct interaction with copilot in your code editing tab (current working file).  In these modes there are essentially 3 ways to interact with it:
1. an inline chat box where you can ask it similar things like in the separate side chat box, except code can/will be directly injected into your file, while also providng potentially multiple solutions to the ask (multiple code blocks and you can choose which style you prefer). 
2. A "code a head" inline experience where it can suggest on the current line or block of code you're working on and the presumed completion of that code you're currently trying to write.  You can also (with good habits) write inline comments or block comments to describe what you're trying to achive - think of it as inline documentation - which then GitHub Copilot can leverage that natural language definition as well as existing code in the file and your style in that project as the basis for creating a code completion.  This is great if you want to still write code manually but want a bit of a streamlined bump.
3. Next Edit Suggestions takes into consideration what you're doing currently and thinking a couple of steps ahead - predicting what you're likely going to do beyond the current code block - as a result you'll get more than just the point solution on what you're writing and you'll get additional functions/methods etc within the given file...attempting to predict the future.  It's also a neat expereince to simply tab-ahead and accept code (after you've quickly reviewed what was generated of course ;) 

Helpful links/docs:

- [Next Edit Suggestions - VS Code Docs](https://code.visualstudio.com/blogs/2025/02/12/next-edit-suggestions#_next-edit-suggestions-nes)
- [Next Edit Suggestions - GitHub Docs](https://docs.github.com/en/copilot/concepts/completions/code-suggestions)


## Walk - Synchronous Local Development

The previous section is certainly helpful when you're working on new/novel/bespoke situations as you're normally use to.  But what if you've got repeatable type work?  Want to generate Unit tests? Want to write documentation?  Maybe you have migration type work that you have figured out a reusable prompt to use over and over again and want to share/make it available for team mates or future work for the same problem?  The following will help you structure this and detail how/when/why you'd use the following enhancement features (Prompts, Custom Instructions and Custom Chat Modes).  We're making our way towards "Spec Driven Development" with these fundamentals.

### Prompts

Reusable [prompt files](https://code.visualstudio.com/docs/copilot/customization/prompt-files) are the fundamental building blocks for success.  They're nothing magical - they're just Markdown files...but they are a great way to have easy access to "commands" that can be used over and over again to interact with GitHub Copilot (or any AI assistant for that matter).  The true magic of a prompt file in VS Code are:

1. "Slash Commands" - by following the file/folder convention of ```%repo-root%/.github/prompts/<some-file-name>.prompt.md``` you can gain access to invoking the prompt in the GitHub Copilot Chat interface buy typing ```/<some-file-name>``` before or after by any additional info you want to provide. Take for example one of our "starter prompts" for writing a Product Requirements Doc (PRD) in [.github/prompts/prd.prompt.md](.github/prompts/prd.prompt.md).  It is a quick way to ensure that the LLM follows your/your team's way of writing a PRD - presuming you have a defined way of doing it today.  This ensures that you have consistency and clear identifable and repeatable way of generating these docs (which you may have avoided writing) going forward with the AI doing the true heavy lift.  Should you not provide sufficient information the AI/Coding Assistant/LLM can ask you more questions in order to create a better doc...pretty slick if you ask me...

2. Well defined meta parameters/config in it's Markdown file format.  A GHCP prompt file has a well defined [file format](https://code.visualstudio.com/docs/copilot/customization/prompt-files#_prompt-file-format) which consissts of:
- an optional Header that has 4 config properties: [Description, mode (ask, edit or agent), model (language modle you prefer for this prompt), tools (MCP tools or local VS Code extensions exposed as tools that GHCP is allowed access to)]
- a required Body which is the natural lanaguage prompt/markdown magic that the LLM is instructed to follow.

This allows you to create reusable patterns and keep GHCP grounded to a specific task/action.  

Prompts (and Custom Chat Modes) is the early base precursor to broader "Agents" or "Custom Agentic Capabilities" you can define in the future with GitHub Copilot and in general terms - but isn't available YET as of this projects' publish data (October 6th, 2025).  We will however discuss ["Continuous AI"](https://githubnext.com/projects/continuous-ai/) and "[Agentic Workflows](https://githubnext.com/projects/agentic-workflows/)" in a later section from the good folks at "[GitHub Next](https://githubnext.com)".

Examine the [.github/prompts/prd.prompt.md](.github/prompts/prd.prompt.md) file for it's structure - note that we've defined the base model (Claude Sonnet 4) it's mode (Agent - which is default if left out) as well as a description of what the prompt does in general to "prime" GHCP.  Note we've left of which tools it has to use - but we could/should scope it down to "edit" only - such that it can only write to our local file system (create the new PRD markdown file).  Without this tool - it will generate the PRD but only within the chat history - even though we've defined it to be in "Agent Mode" within the config itself.  Give it a try :)

> [!Note] 
> The Prompt File is added as part of the User Prompt in a chat - meaning it's auto appended/filled into the prompt sent to GHCP on the given request.  This contrasts to how "Custom chat modes" work...which we'll discuss later.

### Custom Instructions

You may find that you always want certain outcomes or rules to be applied.  This is where [GitHub Copilot custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions) come into play.  These custom instructions are ALWAYS sent as part of the interaction with GitHub Copilot in your given workspace (repo).  There are two levels of custom instructions:
- ```%repo-root%/.github/copilot-instructions.md``` file - which is the top level instructions file, sent with each and every request to GHCP.  Use this file when you want rules to always be atomatically applied to all chat requests in the given workspace
- ```%repo-root$/.github/instructions/*.instructions.md``` this is an instruction file scoped via the ```applyTo``` yaml header frontmatter config of the markdown file wihch is a list of file extensions that the rule applies to.  Let's say you always have a rule for writing Terraform or maybe a given programming language like Typescript - this could be style/coding syntax - it could be rules around testing - but it's only applicable to that file format (*.tf or *.ts) then you can write multiple files in there and they'd only apply if you/GHCP are working on those formats.

In general I would say that if you have strong opinions on the tech stack for your given project/repo/workspace - Custom Instructions are the best place to put them as they are implicitly sent on your behalf - you do not need to explicitly invoke these rules...they're a great passive skill :D

> [!Note] 
> There currently isn't any additional configuraiton settings for custom instructions beyond the "```applyTo```" setting and of course the body of your markdown prompt. Unlike custom prompts and custom chat modes

Take a look at the custom instructions in the starter kit:
- [Copilot Instructions](.github/copilot-instructions.md)
- [Terraform Custom Instructions](.github/instructions/terraform.instructions.md)

#### Copilot Custom Instructions vs. AGENTS.md vs. README.md

You'll find that as the industry evolves - good folks will get together and start to formalize and standardize on their implementations to help improve the developer experience/ergonomics.  The emergence of [Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro) (MCP) as an open community/standard to extend LLMs/Agents is one example.  The "[AGENTS.md](https://agents.md)" is another example of this.

What you'll find is that AGENTS.md is an attempt to unify the various "rules" or "custom instructions" formats that are out there in the vendor specific implementation of coding assistants/agents.  Today both [GitHub Copilot Coding Agent](https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent) and Github Copiot in VS Code (as of VS Code v. 1.104) support the AGENTS.md file in addition to the copilot specific format.  This helps to allow you to write a single rules file across your various coding agent environments going forward...

But how does tihs differ from a project/repo ```README.md``` file?  In short...a ```README.md``` is meant for a human to read - it can be long...it can be more detailed...but really the intended audience is humanz.  An LLM can still take advantage of it (it will inevitably) but an ```AGENTS.md``` file along with other prompts is a shortcut and always picked up by the agents/llms going forwad as part of each vendor platform.  You can make things more terse and put it in a structure/format that is more computer friendly as a result.

### Custom Chat Modes

I would argue that custom chat modes are truly the precursor to "Custom Agents" in GHCP - but this is like...my opinon <insert big lebowski gif>.

The biggest differences vs. custom prompts is as follows:

1. "Agent" mode is already implied...there's no other mode to operate in - meaning you couldn't choose "ask" or "edit" even if you wanted to
2. You explicitly switch into this mode just like you would with the built-in modes - "Ask", "Edit" and "Agent" for the duration of your chat session/until you swithc out of this mode.  This ensures you're not explicitly/manually having to invoke a command over and over again - but really - and more importantly you'll be grounding GHCP into a specific persona/workflow.  Meaning a custom chat mode is meant to tell GHCP that "YOU ARE A PLATFORM ENGINEER...." or "YOU ARE A DOTNET DEVELOPER" and follow it with more details on how to do that type of work
3. You can configure a description for the chat mode, tools and the model to use...and that's it


Just like a custom prompt file - there's a file/folder convention ```.github/chatmodes/<some-chat-mode-name>.chatmode.md```.  Once you've set that up you can pick from the chat mode drop down your new custom chat mode.

Further to this - in my opinion - the chat mode is like a "meta mode" which you can use to define/curate/combine with prompts.  Since custom Prompts are like "executables" for one off actions, you could/should combine them for a type of work.

Let me explain some more with the example of a Platform Engineer vs. a DotNet Developer.

You may have prompt files (aka slash commands) for doing certain types of actions.  As a Platform Engineer you may want to deploy to Azure or AKS within Azure as an example.  You could have a ```/deploy``` slash command that only is used when in "platform mode".  This command/prompt is pretty useless when you're writing code - so you're not going to include it in your "DotNet Mode" (this can be argued but for this example we're jsut going to stick to our silos).  You may however have a ```/devops``` command which is universal - which includes how you push to a repo and kick off CI/CD.  As a result this command is reusable across workload personas and could be referenced in both the "Platform Mode" and the "DotNet Mode" custom chat modes.

This way we have consistency by writing these prompts/commands in one place that both GHCP and a human can invoke, and we have a way to assemble/curate them into custom work/chat modes to group like activities/skills in one format.

In the future - when we discuss "Continuous AI" or "Agentic Workflows" - these chat modes will be important - as we wont' be asking our LLMs to do a single task, but a grouping of tasks/skills for a given phase of our project.  Having custom chat modes/agents allows us to keep our context windows and skill set (including MCP tool calls) orgnaized and sane.  We don't want to just give all powers to the LLM/coding assistant as that may confuse it or us given a scoped task.

We've got two custom chat modes to examine:
- [devops](.github/chatmodes/devops-engineer.chatmode.md)
- [platform arcihtect](.github/chatmodes/platform-architect.chatmode.md)

note that they share one common prompt/command (```/terraform```) but have other non-overlapping/distinct commands at their disposal.  the roles are similar but may not have exactly the same types of tasks/skills to execute. (for the same of this starter I've left out the other slash commands/prompts in the ```.github/prompts``` directory that those sections refer to - but you can imagine that each slash command would correspond to a specific file just like the ```/terrform``` file matches to the ```.github/prompts/terraform.prompt.md``` file)

## "Party Pace"...heavy jogging/some running...We're now into Spec Driven Development (SDD)

The previous section was quasi-manual/synchronous workflow with some "Vibing" on the work (I'm not a fan of the term or idea...but that's just me).  This is great I would say for quick prototypes and solutionining in the moment to get up and running but a larger problem especially in a larger more complex organization or perhaps a longer term iterative project would require something a bit more structured.  Arguably if "Vibe Coding" is on the "far-left" hand of AI Assisted Coding (Just "YOLO" the problem and roll the dice iteratively) we can think of Spec Driven Development as the current "far-right" hand side of AI Assisted Coding.

In other words:
- if just simply sitting down and diving into writing code without design/architectural planning is your thing - then "Vibe Coding" may be a great fit for you and your project.
- if a structured plan and following "project/product management" best practices feels better for you? Then Spec Driven Development (SDD) may be a better fit - especially in a larger team or if you go "full AI" and have a fleet of LLMs/Coding Assistants at your disposal.

The reality/truth is likely somewhere inbetween...and we've likely not seen the last evolution of this as we've gone from "Vibes" to "Spec Driven" in short order (~6 months).  Just like we saw software development evolve with waterfall/agile etc. over the years, we're likely going to see new solutions to problems at scale when AI evolves and our distributed software development lifecylce grows out of the control at human scale.

### Spec Kit

From a GitHub/Microsoft POV we've released and Open Sourced [Spec Kit](https://speckit.org/).  I personally see it like a scafolding generator similar to "rails generate" or other type tools for defining what your specification driven development would look like for your team.  Taking advantage of the features we have today in AI Assisted Coding Agents like GitHub Copilot (GHCP) we can help structure, reuse and call upon prompts that are at our disposal to accomplish our work.  Recall in the eariler ["Walk"](#walk---synchronous-local-development) section we were able to take advantage of custom prompts, custom instructions and custom chat modes?  Well [Spec Kit](https://speckit.org) allows us to leverage these these building blocks to help guide us and GHCP (or any other AI Coding Assistant you prefer) to develop what our project/product goals are for the current repo.

To find out more about Spec Kit - I highly suggest giving Den Delimarsky a follow on [linkedin](https://www.linkedin.com/in/dendeli/) and on [YouTube](https://www.youtube.com/channel/UCNHIUc6KE64sUe5G0eP70aQ) if you want to keep up to date on Spec Kit as well as MCP (especially Authentication/Authorization for MCP).

> [!Note]
> There are more than one approach/framework for Spec Driven Development (SDD) - Spec Kit is one flavour/implementation but there are others like [BMAD Method](https://github.com/bmad-code-org/BMAD-METHOD) and [Agent-OS](https://github.com/buildermethods/agent-os).  Just like debates around language models (GPT vs. Claude vs. Qwen etc.) Your personal preference and style is most important as an individual as well as a team.  They're all "just prompts" so it's not hard to adjust, evolve and move between them - just make sure you're creating some standards and structures to guide yourselves as humans and as human-like LLMs...good luck!

### So What, Who Cares?

You're probably asking yourself "So what, who cares?" - well what you'll learn if you haven't already, is that if you set an LLM/Coding Assistant out on a poorly defined task - your results are varied to say the least.  SDD will help to keep it on track by providing (in general) your coding/tech standards (usually in the form of a custom instruction file like ```copilot-instructions.md``` or ```AGETNS.md```) as well as some repeatable "commands"/prompts that are general purpose enough but guided so that you have some type of quasi-near-deterministic work output...of course the exact output is not going to be 100% the same - but you're generally guaranteed that it'll be in very close ball park of what you want to achieve.

One exterme of vibe coding would be "make me a social network platform to manage my kid's soccer league"...okay...that might work sorta...but the LLM need to do a ton of work with not much defined in the way for it to track what needs to be done, what your preferred tech implementation would be etc.  So it'll guess.  What if it or your computer stops mid "vibe"?? How do you recover?  How do you track and make sure you've completed the landing page before moving on.

Again - this is an exterme case but the point is clear - if you're working on something simple and qiuck this may work well.  If you're building something larger like a social network you're likely going to get more organized before you or the AI starts to engineer a solution.

Here's where SDD comes in.

With SDD - and if you're using one of the SDD "frameworks" or "engines" - you start off with the why/who and start to generate the higher level non-coding related documents needed to keep us all sane (people and robots).  You may have heard or Product Requirement Docs, Spec Docs etc. etc.  Whatever you prefer, whatever you want to call them - they're the foundation of work that we all knew were "best practices" but avoided as it was in our way of just jumping into code...or maybe that's just me.

In general the SDD frameworks provide guidance and structure to how to plan out your project and often have built in prompts to employ "memory" and "task" techniques to keep your AI Assistants on track.

Often you're limited by context/token limits (how much of the current generated conversation input/output) you have access to.  Some models are limited to ~128K Tokens/Context Window Sizes - some are in the order of 1M...regardless it's not infinite and even if it were you'll find that they generally perform better at the lower end of (~30K Tokens) or so - your mileage may vary.

Employing chat compaction, memory, task lists/todos etc. etc are extremly important to keep your AI on task.  It can refer back to these things as needed or not at all depending on the type of work it needs to do in the given moment.  Some functions are in isolation of another...some reqiure a larger view of the entire codebase so having things like ```AGENTS.md``` to provide the agent (e.g. GitHub Copilot) a view of the project structure without having to crawl/regenerate it is very helpful.

Having a coding standard/tech stack document ensures that the AI doesn't arbitrarily decide to use a different MVC framework or Database type mid project.

Using one of the SDD frameworks helps you abstract some of this out and "DRY" up your process when structuring your various types of prompts.

## Running with GitHub Copilot Asynchronously

In the Crawl/Walk phase we're primarily focused on how GitHub Copilot can help enhance our work in our local/inner development loop as a human.  Meaning, we were primarily focused on how to take advantage of AI Assisted coding as an augmentation to our own work and skillset at direct human scale and speed.  

In this Run Phase, we'll be looking at how we can offload work to an Agent asynchronously - meaning how can we assign work to Agent(s) without the need for our IDE/Local Development environment to be always on - we can walk away or close our computer while work is being done on our behalf in the cloud. 

## Run - Phase 1: Asynchronous Remote Development - "Single Agent" 

### GitHub Copilot Coding Agent (aka. SWE Agent/Project Padawan)

WIP - DEMO GHCP Coding Agent - Assign it work

GitHub Copilot "Coding Agent"...not to be confused with GitHub Copilot "Agent Mode" (local in IDE synchronous work agent) - is a version of GitHub Copilot that you full interact with remotely - meaning it is an entity that lives completely in the cloud.  The environment in wihch it runs is entirely remote and it runs within the context of GitHub Actions - meaning the environment is ephemeral and is built upon the fundamental building block that is GitHub Actions.

In some literature you'll find that this mode of operation is often referred to as a "Copilot Coding Agent (CCA)", "Software Engineering Agent" or "SWE Agent".  In some official GitHub blog articles it was referred to as "Project Padawan".  The name isn't as important as the fact that it is essentially a bot to which you can assign work to.

Today (Timestamp: October 7th 2025), the GitHub Copilot Coding Agent is given work primarily by assigning it to a GitHub issue as an "assignee" just as you would yourself or another teammate in GitHub.  This automatically triggers an even to which GitHub Copilot Coding Agent can then pick up and start creating a PR and a new git branch to work from.

The most valuable piece of this - beyond the task output (i.e. written code) from Copilot - is the fact that you can "view session" which is the ability to observe Copilot's thought and working processs.  More invaluable than its code output is learning how it approaches work and its thought process (however flawed/imperfect it may be).  

If during the PR Code Review process you find that it needs to improve on what was accomplished, you can simply "```@copilot```" in the comments and even inline in code review comments as well.  This triggers a new session within the PR and allows it to fix its mistakes just like a human team mate would.

> [!Note]
> Since the primary interface is via a GitHub Issue - you should treat the Issue Body as the "user prompt" you would normally provide GitHub Copilot in your IDE - meaning you should give it good context and a defined task and description of the work to be done.  You can also provide it images (e.g. Screenshots) as part of the Issue Body, and since the the model has Vision capabilities, it can "see" and make sense of the visual requirements you have as well.

The GitHub Copilot Coding Agent has access to both the GitHub MCP server and the Playwright MCP server by default, so if you need more context from the git repo, or need it to generate a screenshot of your web app or create Playwrite interaction/integration tests via your web UI it can do so.  Extending from this you can add any arbitrary MCP server (presuming your organization allows this) to further extend the capabilities that Copilot can perform, similar to how you can add MCP severs to VS Code such that GitHub Copilot in "Agent Mode" (remmeber there's a difference) to extend its capabilities.  There are some limitations based on the networking/security model but there's also facility to create allow/deny list rules. 

My example here why this Asynchronous mode matters: You are likely attending more meetings than you have time to actually sit down and write code...but assigning it to GitHub Copilot Coding Agent allows you to come back and review the work and keep the ball moving.

In the next section we'll start to discuss the future state of having a fleet of these agents working for us and how/why we might possibly implement this in our day-to-day activities.

## Run - Phase 2: Asychronous Remote Development - "Squad of Agents"

What does critical scale look like when 
