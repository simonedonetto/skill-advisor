---
name: skill-advisor
description: Recommends which of the user's installed skills to use for the work in the current chat. Use it with /skill-advisor or when the user asks "which skill should I use?", "what can I use for this?", or doesn't know where to start (in any language).
---

# Skill Advisor

Purpose: help a beginner understand, among the skills they have already installed, which ones fit the work they are doing in this chat.

Main context of use: the Claude app (web, desktop, mobile). It also works in the terminal.

Always reply in the user's language, in simple words and without technical jargon. The tone is that of a patient guide: explain why you recommend each skill.

## When to use it

- Only on explicit request: `/skill-advisor`, or phrases like "which skill should I use?" or "what can I use for this?".
- Never spontaneously, even if the user seems stuck.

## Procedure

1. **Understand the current work.**
   - Base yourself on the conversation and on the attachments the user has uploaded.
   - If you are in an environment with working folders (e.g. the terminal) and there are relevant files, you may look at those too. If there are none, skip this point.
   - If the goal is unclear, ask ONE short question (e.g. "What result do you want to get?") and wait for the answer.

2. **Retrieve the list of installed skills.**
   - Use first the list of skills already present in the session context.
   - If ListSkills or SearchSkills are available (they may be deferred: load them with ToolSearch), use them to complete the list.
   - Consider every skill you can see in the session, including plugin, project and personal skills.
   - Never invent skills that do not appear in the list.
   - **If you cannot read the list**: say so clearly, tell the user they can see their skills in the app's skill settings, and ask them to paste the names. Do not guess.

3. **Choose the skills to recommend.**
   - Read each skill's description and judge how relevant it is to the current work.
   - Priority criterion: relevance to the work in progress first; if relevance is equal, the more specific skill beats the generic one.
   - Pick at most 3 skills, the most important ones, ordered from the most useful.

4. **Check that the skill is actually usable.**
   - If a relevant skill is installed but not active (not enabled, or missing from the list of enabled ones), flag it with the label "to enable" and explain in one sentence how to enable it (the app's skill settings).
   - Do not present as ready to use a skill that you cannot verify as active.

5. **Answer in this format**, for each recommended skill:
   - **Skill name** (with the label "to enable" if it is not active)
   - Why it fits here: one concrete sentence tied to the user's work
   - How to use it: the command (e.g. `/skill-name`) or an example sentence to copy and paste

6. **If no skill fits, or none is installed**:
   - Say so openly, without forcing a recommendation.
   - Offer ONCE to search for new ones (with SuggestSkills or SearchSkills, if available).
   - If the user declines or does not answer, do nothing else and do not insist: keep helping directly in the chat.

7. **Close** by asking which one they want to use. Recommend only: do not launch the recommended skill and do not start the work until the user confirms.

## Rules

- At most 3 recommendations, short and easy to scan.
- Do not explain what a skill is: go straight to the recommendations.
- Explain the practical benefit, not how the skill works internally.
- Stay generic: do not assume the user has any specific skill, recommend only the ones you actually see in their list.
- Never recommend skills that do not appear in the verified list.
