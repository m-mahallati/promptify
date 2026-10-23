# Prompt Refiner

A portable skill for **Codex** and **Claude Code** that turns rough prompts into clear, accurate, explanatory requests aimed at the intended outcome.

It preserves your intent and constraints, adds relevant context and completion criteria, and asks focused questions when missing details would change the request. It works for coding, writing, research, planning, and other tasks. The skill refines prompts; it carries out the resulting task only if you also ask it to.

## Install

Clone this repository:

```sh
git clone https://github.com/m-mahallati/prompt-refiner.git
cd prompt-refiner
```

Copy the skill into the appropriate personal skills directory. These commands work in a POSIX shell on Linux, macOS, or WSL and stop if a destination already exists, so your existing skill is preserved.

**Codex**

```sh
mkdir -p "$HOME/.agents/skills"
test ! -e "$HOME/.agents/skills/prompt-refiner" && cp -R skills/prompt-refiner "$HOME/.agents/skills/"
```

**Claude Code**

```sh
mkdir -p "$HOME/.claude/skills"
test ! -e "$HOME/.claude/skills/prompt-refiner" && cp -R skills/prompt-refiner "$HOME/.claude/skills/"
```

Start a new session after installation. For a repository-only install, copy `skills/prompt-refiner` into that project's `.agents/skills/` for Codex or `.claude/skills/` for Claude Code instead. Copy the whole skill folder, not the repository root. If a destination exists, review it before replacing or updating it.

The shared `SKILL.md` uses the common name/description frontmatter. `agents/openai.yaml` supplies optional Codex UI metadata; Claude Code uses `SKILL.md`. No API keys, dependencies, hooks, or MCP servers are required by this skill; your coding assistant still needs its normal setup.

## Use

In Codex:

```text
$prompt-refiner Make this more precise: Fix the login bug where submitting an expired session shows a blank page. Keep the current auth flow.
```

In Claude Code:

```text
/prompt-refiner Make this more precise: Fix the login bug where submitting an expired session shows a blank page. Keep the current auth flow.
```

Both assistants can also select the skill when you explicitly ask to improve a prompt in natural language.

Illustrative refined prompt:

```text
Fix the login bug where submitting an expired session displays a blank page.
Preserve the current authentication flow. Identify the cause and update the
expired-session handling so the user receives the appropriate response within
that flow. Verify that expired-session submission no longer produces a blank
page and that valid-session login still works. Summarize the change and how
you verified it.
```

Useful instructions to append:

- “Return only the refined prompt.”
- “Do not ask questions; use explicit placeholders for missing information.”
- “Keep it under 100 words.”
- “Keep the prompt in Persian.”
- “Refine the prompt, then execute it.”

If you supply “make it faster” with no context, the skill asks what should be faster and what result you need. It does not invent a target, benchmark, or technology stack.

## Review and validation

The skill is instruction-only. See [behavioral review cases](evals/cases.md) for realistic inputs and expected outcomes. These cases are a manual evaluation rubric, not a claim of automated behavioral test coverage. Model outputs and automatic selection can vary by assistant and version.

The package format and installation paths follow the official [Codex skill documentation](https://developers.openai.com/codex/skills/) and [Claude Code skill documentation](https://code.claude.com/docs/en/skills).

## License

[MIT](LICENSE)
