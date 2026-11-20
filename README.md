# skill-advisor

A Claude skill that looks at what you are working on in the current chat and recommends, among the skills you have already installed, the ones that can help you most.

It is built for people who are new to Claude and don't know which of their installed skills to use, or where to start.

## What it does

When you call it, `skill-advisor`:

1. Reads the conversation and any attachments to understand your current work (and, in a terminal environment, relevant files in the working folder).
2. Reads the list of skills available in your session.
3. Recommends **at most 3** skills, ranked by relevance to your task. If two fit equally well, the more specific one wins over the generic one.
4. For each skill, tells you why it fits and gives you a command or a ready-to-paste sentence to start.
5. Flags skills that are installed but not enabled as **"to enable"**, with a one-line hint on how to turn them on.
6. Stops and asks which one you want. It never launches a skill on its own.

## Example

> **You:** `/skill-advisor`
> *(in a chat where you attached a PDF and asked for a summary)*
>
> **Claude:**
> **1. pdf-reader**: you attached a PDF, and this skill extracts its text and tables reliably. Try: "Read the attached PDF and summarize it."
>
> **2. report-writer** *(to enable)*: it would turn the summary into a structured document. Enable it in the skill settings, then try: "Write a one-page report from this summary."
>
> Which one do you want to use?

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

Call it explicitly. It never runs on its own.

- Type `/skill-advisor`
- Or ask in your own words: "Which skill should I use?", "What can I use for this work?", "I don't know where to start."

It replies in the language you write in.

## Behavior at a glance

| Situation | What `skill-advisor` does |
| --- | --- |
| Your goal is unclear | Asks **one** short question, then waits |
| It can't read your skill list | Says so, points you to the app's skill settings, and asks you to paste the names |
| A relevant skill is installed but not enabled | Recommends it with the label "to enable" and a one-line hint |
| No skill fits, or none is installed | Says so, offers **once** to search for new ones, and drops the subject if you decline |
| You haven't chosen yet | Does nothing: it recommends only, never launches a skill |

## Design principles

- **On request only.** It never interrupts you, even if you seem stuck.
- **Recommend, don't execute.** You always choose.
- **Generic by design.** It assumes nothing about which skills you own and never names a skill it can't verify.
- **Short and practical.** Maximum 3 suggestions, each with a concrete reason and a way to start.
- **No jargon.** It does not explain what a skill is: it goes straight to the recommendations.

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

- **Number of recommendations:** change "at most 3" in step 3 and in the Rules section.
- **Trigger phrases:** edit the `description` in the frontmatter to add the phrases your users are likely to type.
- **Tone:** adjust the second paragraph under the title.

After changing the `description`, re-upload or re-copy the skill so the new trigger text takes effect.

## Contributing

Issues and pull requests are welcome. Good contributions include:

- Edge cases where the recommendations were wrong or missing.
- Wording improvements that make the skill clearer for beginners.
- Translations of `SKILL.md` and this README.

When you propose a change, please include the scenario you tested (what you were working on, which skills were installed) and what you expected to see.

## License

Released under the [MIT License](LICENSE).
