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
3. Next Edit Suggestions takes into consideration what you're doing currently and thinking a couple of steps ahead - predicting what you're likely going to do beyond the current code block - as a result you'll get more than just the point solution on what you're writing and you'll get additional functions/methods etc within the given file...attempting to predict the future.  It's also a neat expereince to simply tab-ahead and accept code (after you've quickly reviewed what was generated of course ;) )

#### Documentation Links:
- [Next Edit Suggestions - VS Code Docs](https://code.visualstudio.com/blogs/2025/02/12/next-edit-suggestions#_next-edit-suggestions-nes)
- [Next Edit Suggestions - GitHub Docs](https://docs.github.com/en/copilot/concepts/completions/code-suggestions)


## Walk - Synchronous Local Development

The previous section is certainly helpful when you're working on new/novel/bespoke situations as you're normally use to.  But what if you've got repeatable type work?  Want to generate Unit tests? Want to write documentation?  Maybe you have migration type work that you have figured out a reusable prompt to use over and over again and want to share/make it available for team mates or future work for the same problem?  The following will help you structure this and detail how/when/why you'd use the following enhancement features (Prompts, Custom Instructions and Custom Chat Modes).  We're making our way towards "Spec Driven Development" with these fundamentals.

### Prompts

### Custom Instructions

#### Copilot Custom Instructions vs. AGENTS.md vs. README.md

### Custom Chat Modes

## Party Pace...heavy jogging/some running...We're now into Spec Driven Development

The previous section was quasi-manual/synchronous workflow with some "Vibing" on the work (I'm not a fan of the term or idea...but that's just me).  This is great I would say for quick prototypes and solutionining in the moment to get up and running but a larger problem especially in a larger more complex organization or perhaps a longer term iterative project would require something a bit more structured.  Arguably if "Vibe Coding" is on the "far-left" hand of AI Assisted Coding (Just "YOLO" the problem and roll the dice iteratively) we can think of Spec Driven Development as the current "far-right" hand side of AI Assisted Coding.

In other words:
- if just simply sitting down and diving into writing code without design/architectural planning is your thing - then "Vibe Coding" may be a great fit for you and your project.
- if a structured plan and following "project/product management" best practices feels better for you? Then Spec Driven Development (SDD) may be a better fit - especially in a larger team or if you go "full AI" and have a fleet of LLMs/Coding Assistants at your disposal.

The reality/truth is likely somewhere inbetween...and we've likely not seen the last evolution of this as we've gone from "Vibes" to "Spec Driven" in short order (~6 months).  Just like we saw software development evolve with waterfall/agile etc. over the years, we're likely going to see new solutions to problems at scale when AI evolves and our distributed software development lifecylce grows out of the control at human scale.

### Spec Kit 


## Run - Phase 1: Asynchronous Remote Development - "Single Agent" 

### GitHub Copilot Coding Agent (aka. SWE Agent/Project Padawan)


### Run - Phase 2: Asychronous Remote Development - "Squad of Agents"

