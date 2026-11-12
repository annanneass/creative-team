# Creative Team

A Claude Code skill that gives Claude a full video creative team: a Creative Director runs specialist roles (producer, writer, director, art director, motion designer, editor, sound designer, brand guardian, QA and more), each owning its own decisions and writing one short file.

It has two modes:

- **make**: brief → research → concept → script, style and sound in parallel → beat sheet → brand and QA checks → storyboard (stops for your approval) → build → review → render.
- **review**: up to seven independent reviewers judge a beat sheet, script, project or finished video without seeing each other's notes, then their problems are merged into one ranked fix list.

## Install

**As a plugin (recommended)**, inside Claude Code:

```
/plugin marketplace add annanneass/creative-team
/plugin install creative-team@creative-team
```

**Or copy the skill by hand:**

```bash
git clone https://github.com/annanneass/creative-team.git
cp -r creative-team/skills/creative-team ~/.claude/skills/
cp -r creative-team/skills/client-template ~/.claude/skills/client-yourclient
```

## Set up a client

The team never stores client facts. They live in a separate client skill so the team stays reusable:

1. Copy `skills/client-template` to `~/.claude/skills/client-<name>/`.
2. Change `name:` in its frontmatter to `client-<name>`.
3. Fill in the brand guide, tone, claims and off-limits lists. Leave gaps as "not on file"; the Brand Guardian will ask for them rather than guess.

## Use it

```
/creative-team make a 30s launch reel for our new app, 9:16, for Instagram
/creative-team review ./renders/draft-v2.mp4
/creative-team quick ./beat-sheet.md
```

Work goes in `.creative-team/<date>-<slug>/` inside your project, one file per stage (`00-brief.md`, `01-concept.md`, `02-script.md` …), plus `REVIEW.md` and `FIXES.md` after a review.

`quick` runs only the technical screen, Cold Viewer, Creative Director and Brand Guardian (4 sub-agent calls). A full review is about 8 calls and a full make about 9 to 11, which count toward your plan's usage.

## The team

| Role | Tier | Owns |
|---|---|---|
| Creative Director | core | the concept, the final call, orchestration |
| Producer | core | brief, scope, time, cost, approvals |
| Brand and Compliance Guardian | core | brand, claims, consent, rights |
| QA and Platform | core | safe zones, legibility, specs, accessibility |
| Researcher | per job | facts with sources, references, claims check |
| Writer | per job | hook, script, on-screen words, share copy |
| Director | per job | beat sheet, pacing, transitions |
| Art Director | per job | style, look spec, storyboard, static design |
| Motion Designer | per job | how it moves, the build |
| Editor | per job | cuts, rhythm, footage, captions |
| Sound Designer | per job | music, SFX, mix, silence |
| Strategist | on-call | goals, channels, pillars, cadence |
| Trend and Format Analyst | on-call | what's working now, turned into original ideas |
| Social Manager | on-call | channel packs and captions (never posts) |
| Field Producer | on-call | shoot prep, interview questions, consent |
| Asset Librarian | on-call | footage index and rights ledger |
| Finisher | on-call | colour, audio clean-up, export, handoff |
| Cold Viewer | review only | a stranger seeing it for the first time |

Each role's brief is in [`skills/creative-team/roles/`](skills/creative-team/roles/).

## Works well with

None of these are required; the team uses them when they're installed.

- A **style catalog** skill, so the Art Director picks from named styles with look specs.
- **HyperFrames** (or another code-to-video tool) for building motion graphics.
- A **footage-editing** skill set for talking-head and real-footage cuts.
- `ffmpeg` / `ffprobe` on your PATH, used by the review mode to make contact sheets and measure loudness.

## Ground rules the team follows

- No invented claims, numbers, testimonials or real brand logos.
- A storyboard is shared and approved before anything is rendered.
- Nothing is posted, scheduled or sent without your explicit OK.
- Reviews are second opinions from language models, not a guarantee of results.

## License

MIT
