---
name: skill-advisor
description: Clarifies a new project or research with targeted questions, then builds a phase-by-phase plan of which of the user's installed skills to use. Use it automatically when the user describes a new project, research or multi-step goal at the start of a chat, and also on request with /skill-advisor or when the user asks "which skill should I use?", "what can I use for this?", or doesn't know where to start (in any language).
---

# Skill Advisor

Purpose: when a user describes what they want to do, first make the request clear, specific and unambiguous with a few targeted questions, then show which of their already-installed skills fit each stage, so they know from the start what to use and when.

Main context of use: the Claude app (web, desktop, mobile). It also works in the terminal.

Always reply in the user's language, in simple words and without technical jargon. The tone is that of a patient guide: explain why you recommend each skill.

## When to use it

- **Automatically**, when the user describes a new project, research or multi-step goal of any kind at the start of a chat (e.g. "I want to write a report on X and turn it into slides"), even if they did not call the skill.
- **On request**, with `/skill-advisor` or phrases like "which skill should I use?" or "what can I use for this?", at any point in the chat.
- Run it once per project. Do not repeat it on follow-up messages, and do not run it again unless the user asks or starts a clearly different project.
- Do not run it for quick questions or single-step tasks that need no planning.

## Procedure

1. **Understand the project.**
   - Base yourself on the user's description, the conversation and the attachments they uploaded.
   - If you are in an environment with working folders (e.g. the terminal) and there are relevant files, you may look at those too. If there are none, skip this point.

2. **Clarify the request.**
   - First decide whether the request is already clear and specific. It is if the user has already given the goal, the scope, the expected result or format, and any constraint that matters (audience, level of detail, language, deadline). If so, skip to step 3: do not ask useless questions.
   - Otherwise, ask clarifying questions in rounds:
     - Each round has up to 4 questions. Use the interface's question tool if one is available (e.g. AskUserQuestion), otherwise number the questions in the text.
     - Make the questions multiple choice, with your recommended answer first, worded so that "yes" accepts it. The user can always answer in their own words.
     - Put in the same round only questions that do not depend on each other. A question whose answer depends on another open question goes in the next round.
     - Never ask what you can find out yourself (for example from the attachments or the session context).
   - Keep going, round after round, until nothing is left ambiguous: goal, scope, expected result or format, audience, level of detail, language, constraints. Do not fill gaps with silent assumptions.
   - When everything is clear, restate the project in one to three lines so the user can correct it, then continue.

3. **Retrieve the list of installed skills.**
   - Use first the list of skills already present in the session context.
   - If ListSkills or SearchSkills are available (they may be deferred: load them with ToolSearch), use them to complete the list.
   - Consider every skill you can see in the session, including plugin, project and personal skills.
   - Never invent skills that do not appear in the list.
   - **If you cannot read the list**: say so clearly, tell the user they can see their skills in the app's skill settings, and ask them to paste the names. Do not guess.

4. **Split the project into phases.**
   - Identify 2 to 5 phases in the natural order of the work (e.g. research, first draft, refinement, final file).
   - Give each phase a short name and a one-line goal.

5. **Choose the skills for each phase.**
   - Read each skill's description and judge how relevant it is to that phase.
   - Priority criterion: relevance to the phase first; if relevance is equal, the more specific skill beats the generic one.
   - Pick at most 3 skills per phase, ordered from the most useful.
   - If a skill fits more than one phase, describe it in the first and only mention it by name in the others.
   - If no installed skill fits a phase, say that the phase needs no skill and can be done directly in the chat.

6. **Check that each skill is actually usable.**
   - If a relevant skill is installed but not active (not enabled, or missing from the list of enabled ones), flag it with the label "to enable" and explain in one sentence how to enable it (the app's skill settings).
   - Do not present as ready to use a skill that you cannot verify as active.

7. **Answer in this format.** For each phase:
   - **Phase N: name** and its one-line goal
   - For each recommended skill:
     - **Skill name** (with the label "to enable" if it is not active)
     - Why it fits here: one concrete sentence tied to the user's project
     - How to use it: the command (e.g. `/skill-name`) or an example sentence to copy and paste

8. **If no skill fits the project at all, or none is installed**:
   - Say so openly, without forcing a recommendation.
   - Offer ONCE to search for new ones (with SuggestSkills or SearchSkills, if available).
   - If the user declines or does not answer, do nothing else and do not insist: keep helping directly in the chat, now that the request is clear.

9. **Close** by asking whether to start with Phase 1 and which skill to use. Recommend only: do not launch any skill and do not start the work until the user confirms.

## Rules

- Clarify before planning: never build the plan on an ambiguous request.
- At most 4 questions per round. Keep going until the request is clear, but never ask what is already clear.
- At most 5 phases and at most 3 skills per phase. Keep the plan short and easy to scan.
- Do not explain what a skill is: go straight to the questions or the plan.
- Explain the practical benefit, not how the skill works internally.
- Stay generic: do not assume the user has any specific skill, recommend only the ones you actually see in their list.
- Never recommend skills that do not appear in the verified list.
