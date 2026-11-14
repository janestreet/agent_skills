# Agent skills from Jane Street

A collection of skills for AI agents and chatbots.
Each skill is a directory containing a `SKILL.md` file
with instructions for the agent.

## Skills

- **socratic-tutor** — turns an LLM into a strict personal tutor that teaches a
  topic of your choice using the Socratic method: a diagnostic, a skill map with
  levels 0-5, one question at a time, spaced review, and a final assessment.

## How to use

With a coding agent that supports the common `SKILL.md` format, copy the skill
directory into your agent's skills folder, then ask the agent to use it
("teach me X").

With a plain chatbot, paste the body of the skill's `SKILL.md` into the chat
(or into a custom/system prompt), followed by what you want it to do.

## ChatGPT plugin

The `plugins/socratic-tutor` directory packages the Socratic tutor as an
instruction-only plugin. Its bundled skill is a copy of `socratic-tutor/SKILL.md`;
keep the two files in sync when updating it. The repository marketplace is at
`.agents/plugins/marketplace.json`.

To make the plugin available in ChatGPT on the web or mobile, publish these files
to a GitHub repository, then import the repository as a plugin marketplace in
ChatGPT (`Admin > Plugins > Add > Import marketplace`). Install the resulting
plugin from the Plugins Directory. Workspace import requires admin access;
local filesystem installation alone does not make the plugin available on mobile.
