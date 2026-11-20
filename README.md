# skill-advisor

A Claude skill that, at the start of a project or research, asks you a few targeted questions to make the request clear, and then builds a phase-by-phase plan of which of your already-installed skills to use, and when.

It is built for people who are new to Claude and don't know which of their installed skills to use, or where to start.

## What it does

When you describe a new project or research (or when you call it), `skill-advisor`:

1. Reads your description, the conversation and any attachments to understand what you want to achieve (and, in a terminal environment, relevant files in the working folder).
2. **Clarifies the request.** If something is ambiguous, it asks multiple-choice questions, up to 4 per round, with its recommended answer first. It keeps going round after round until the goal, scope, expected result, audience, level of detail, language and constraints are clear. If your request is already clear and specific, it skips the questions.
3. Restates the project in one to three lines so you can correct it.
4. Reads the list of skills available in your session.
5. Splits the project into **2 to 5 phases** in their natural order (for example: research, first draft, refinement, final file).
6. Recommends **at most 3 skills per phase**, ranked by relevance. If two fit equally well, the more specific one wins over the generic one.
7. For each skill, tells you why it fits and gives you a command or a ready-to-paste sentence to start.
8. Flags skills that are installed but not enabled as **"to enable"**, with a one-line hint on how to turn them on.
9. Stops and asks whether to start with Phase 1. It never launches a skill on its own.

## Example

> **You:** I want to write a report on the electric car market and turn it into a presentation.
>
> **Claude:** *(round of questions)*
> 1. **Scope:** Which market? Global, Europe, or a single country? *(recommended: Europe)*
> 2. **Depth:** A one-page overview or a detailed report? *(recommended: detailed report)*
> 3. **Audience:** Who will read it? *(recommended: non-experts)*
> 4. **Language:** Report and slides in English? *(recommended: yes)*
>
> **You:** Europe, detailed, non-experts, yes.
>
> **Claude:** To confirm: a detailed report on the European electric car market for non-experts, in English, then a short presentation based on it. Here is the plan.
>
> **Phase 1: Research.** Gather current data on the European market.
> - **deep-research**: it searches multiple sources and compiles a structured summary. Try: "Research the European electric car market and summarize the main findings."
>
> **Phase 2: Report.** Write the report from the findings.
> - **report-writer** *(to enable)*: it turns notes into a structured document. Enable it in the skill settings, then try: "Write a detailed report from this summary."
>
> **Phase 3: Presentation.** Turn the report into slides.
> - **slide-maker**: it builds a deck from the report content. Try: "Make a short presentation from this report."
>
> Do you want to start with Phase 1 using **deep-research**?

The skill names above are illustrative. `skill-advisor` only ever recommends skills it can actually see in your session.

## Installation

### Claude app (web, desktop, mobile)

1. Download or clone this repository.
2. Zip the `skill-advisor/` folder so that the archive contains the folder with `SKILL.md` inside it.
3. In the app's skill settings, upload the ZIP file and enable the skill.

The exact menu names can differ between plans and app versions. If you can't find the upload option, check the settings of your account or organization.

### Claude Code (terminal)

Copy the skill folder into your personal skills directory:

```bash
mkdir -p ~/.claude/skills
cp -r skill-advisor ~/.claude/skills/
```

Or, to make it available only inside one project, copy it into that project's `.claude/skills/` folder instead.

## Usage

There are two ways to trigger it.

- **Automatically:** at the start of a chat, describe what you want to do ("I want to write a report on X and turn it into slides", "I need to research Y"). The skill detects a new project or research, asks its questions if needed and proposes the plan, even if you didn't call it.
- **On request:** at any point, type `/skill-advisor` or ask in your own words: "Which skill should I use?", "What can I use for this work?", "I don't know where to start."

It replies in the language you write in.

Automatic triggering depends on Claude deciding that your message describes a new project or research, so it can occasionally miss. Calling `/skill-advisor` always works.

## Behavior at a glance

| Situation | What `skill-advisor` does |
| --- | --- |
| You describe a new project or research at the start of a chat | Clarifies it if needed, then proposes a phase-by-phase plan, once |
| Your request is already clear and specific | Skips the questions and goes straight to the plan |
| Your request is ambiguous | Asks rounds of up to 4 multiple-choice questions until nothing is left unclear |
| You ask a quick question or a single-step task | Stays quiet |
| You send follow-up messages in the same project | Does not repeat the questions or the plan |
| It can't read your skill list | Says so, points you to the app's skill settings, and asks you to paste the names |
| A relevant skill is installed but not enabled | Recommends it with the label "to enable" and a one-line hint |
| A phase has no matching skill | Says the phase can be done directly in the chat |
| No skill fits, or none is installed | Says so, offers **once** to search for new ones, and drops the subject if you decline |
| You haven't chosen yet | Does nothing: it recommends only, never launches a skill |

## Design principles

- **Clear before planned.** It never builds a plan on an ambiguous request, and never asks what is already clear.
- **Plan at the start.** It helps when you describe the project, so you know from the beginning what to use and when.
- **Once per project.** It does not interrupt you on every message.
- **Recommend, don't execute.** You always choose.
- **Generic by design.** It assumes nothing about which skills you own and never names a skill it can't verify.
- **Short and practical.** At most 4 questions per round, 5 phases and 3 skills per phase, each with a concrete reason and a way to start.
- **No jargon.** It does not explain what a skill is: it goes straight to the questions or the plan.

## Repository structure

```
.
├── README.md
├── LICENSE
└── skill-advisor/
    └── SKILL.md
```

`SKILL.md` contains the skill's metadata (name and description, used by Claude to decide when to trigger it) and the full instructions.

## Customization

You can adapt the skill by editing `skill-advisor/SKILL.md`:

- **Amount of questions:** change "up to 4 questions" and the "keep going, round after round" rule in step 2 and in the Rules section. For example, limit it to a single round.
- **Size of the plan:** change "at most 5 phases and at most 3 skills per phase" in step 4, step 5 and the Rules section.
- **Trigger behavior:** edit the `description` in the frontmatter and the "When to use it" section. For example, remove the automatic trigger if you want it to run only on request.
- **Tone:** adjust the third paragraph under the title.

After changing the `description`, re-upload or re-copy the skill so the new trigger text takes effect.

## Contributing

Issues and pull requests are welcome. Good contributions include:

- Edge cases where the questions or the plan were wrong or missing.
- Cases where the automatic trigger fired when it shouldn't have, or didn't fire when it should have.
- Cases where it asked too many questions, or too few.
- Wording improvements that make the skill clearer for beginners.
- Translations of `SKILL.md` and this README.

When you propose a change, please include the scenario you tested (what you described, which skills were installed) and what you expected to see.

## License

Released under the [MIT License](LICENSE).
