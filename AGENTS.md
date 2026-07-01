# Codex Entry — claudecode_learnword

This project generates the user's daily learning posts. It has two independent tracks: technical knowledge and humanities/general knowledge.

## Technical Daily Knowledge

Use the `daily-knowledge` skill when the user asks for today's technical post, daily knowledge, diffusion/systematic CV learning, or scheduled technical push.

Read first:
1. `STATE.md`
2. `ROADMAP.md`
3. `INDEX.md`
4. Recent files in `daily/`
5. Legacy rule file if needed: `.claude/skills/daily-knowledge/SKILL.md`

Current remembered state as of 2026-06-29:
- Stage B, controlled generation / diffusion systematization.
- Done: B1 DDPM, B2 DDIM.
- Next main topic: B3 Score-based / SDE unified framework.
- Style: intuition plus complete derivation, no skipped steps, Chinese explanation, English terms/code.

## Humanities Daily

Use the `daily-humanities` skill when the user asks for humanities, 通识, 地缘, 历史, 政治, 文明, or scheduled humanities push.

Read first:
1. `humanities/STATE.md`
2. `humanities/ROADMAP.md`
3. `humanities/INDEX.md`
4. Recent files in `humanities/posts/`
5. Legacy rule file if needed: `.claude/skills/daily-humanities/SKILL.md`

Style: clear, neutral, causality-first, no forced jokes. Political topics must present facts and multiple incentives without preaching.

## Write Rules

- Use the real current date `YYYY-MM-DD`.
- Technical posts go to `daily/YYYY-MM-DD.md`.
- Humanities posts go to `humanities/posts/YYYY-MM-DD.md`.
- After generation, update the matching `ROADMAP.md`, `STATE.md`, and `INDEX.md`.
- If today's file already exists, read it first and do not overwrite unless regeneration is requested or the file is incomplete.
