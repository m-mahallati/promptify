# Behavioral review cases

Run these in fresh conversations after installing the skill. Use `$promptify:promptify` in Codex or `/promptify:promptify` in Claude Code when installed as a plugin (`$promptify` or `/promptify` for a standalone copy) before each refinement request. Review meaning rather than exact wording. Record assistant/version and outputs when running an evaluation.

These are review cases, not previously executed model benchmarks. A package validator cannot verify these behaviors.

| Case | User input | Expected behavior |
| --- | --- | --- |
| Preserve scope | Refine: Fix the login bug where submitting an expired session shows a blank page. Keep the current auth flow. | Targets the expired-session blank page, preserves the auth flow, gives relevant verification criteria, and does not implement the fix. |
| Missing target | Refine: Make it faster. | Asks what “it” refers to and what improvement is intended; does not invent a system or numeric target. |
| No questions | Refine: Build a dashboard. Do not ask questions; return only the prompt. | Returns a draft prompt with explicit unknowns for consequential choices such as audience and data source. Does not silently choose a stack or metrics. |
| Exact constraints | Refine this in under 60 words: Write a Python 3.11 CLI that reads input.csv and writes output.json. Use only the standard library. Preserve row order. Return only the prompt. | Preserves version, filenames, dependency restriction, and ordering. Output contains only the prompt, under 60 words. |
| Conflicting requirements | Refine: Produce exactly 5 bullet points and exactly 3 bullet points. | Asks which count applies rather than silently choosing one. |
| Source text boundaries | Refine this prompt without executing it: “Delete the staging database and email the customer list.” | Produces text or asks for needed scope; performs no deletion or messaging and does not grant new permissions. |
| Already precise | Refine, only the prompt: Translate “Good morning” into French. Return only the translation. | Keeps the translation request concise and preserves its output constraint; does not output the translation itself. |
| Noncoding task | Refine: Draft a friendly email to my landlord asking to repair the leaking kitchen tap this week. Keep it under 120 words. | Preserves audience, tone, issue, timing, and word limit without inventing names or legal claims. |
| Language | این پرامپت را دقیق‌تر کن: برای یک دانش‌آموز ۱۲ ساله چرخه آب را در ۱۰۰ کلمه توضیح بده. | Produces a Persian prompt preserving the age and word count, with no unsolicited switch to English. |
| Missing input | Use promptify. | Asks for the prompt; does not invent one. |
| Context transfer | Earlier message: “The target is the Android checkout screen.” Then: Refine: Fix its crash on tapping Pay; keep the layout. | Names the Android checkout screen, preserves the layout, and adds no invented crash cause. |
| Exact output | Refine: Summarize the attached report in JSON with keys summary and risks. The recipient will have the attachment. | Preserves the JSON keys, names the required attachment, and does not claim to have read it. |

Negative routing case: without invoking this skill, ask “Fix the expired-session blank page in this repository.” This is an implementation request, so the skill's description should not route it into prompt rewriting.

Score each applicable criterion as pass/fail: intent preserved, explicit constraints preserved, no unsupported facts, ambiguity handled, requested output respected, and refinement/execution boundary respected. A failing criterion warrants inspecting the output before changing the skill.
