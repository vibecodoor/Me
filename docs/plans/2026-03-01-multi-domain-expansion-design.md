# Multi-Domain Expansion Design

## Summary

Expand Me from a single-domain health tracker to a multi-domain personal life tracker. Add `career/` as the second domain alongside existing `health/`. Introduce a root `INSTRUCTIONS.md` for routing and shared conventions.

## Architecture: Root Router (Approach A)

```
Me/
├── INSTRUCTIONS.md          # Root: routing + shared formats
├── health/
│   ├── INSTRUCTIONS.md      # Health-specific (unchanged)
│   └── ...                  # All existing files unchanged
└── career/
    ├── INSTRUCTIONS.md      # Career-specific instructions
    ├── CAREER.md            # Navigation hub
    ├── agents.md            # 3 specialist personas
    ├── profile.md           # Current position, experience, goals
    ├── goals.md             # Career goals with progress tracking
    ├── skills.md            # Skills, courses, certifications
    ├── network.md           # Contacts, mentors, references
    ├── interviews.md        # Interview prep and history
    ├── achievements.md      # Projects, wins, resume items
    ├── journal.md           # Reflection: what done, learned, next
    └── logs/YYYY/MM.md      # Weekly reviews
```

## Root INSTRUCTIONS.md

Lightweight file with 3 responsibilities:

1. **Domain routing** — detect domain from query keywords, load the right domain INSTRUCTIONS.md
2. **Shared conventions** — date formats (ISO 8601), 1-10 scales, quick entry syntax, language rules (respond in user's language, files in English), correction/duplicate handling
3. **Cross-domain logic** — when a query spans domains (stress ↔ career pressure), read both domain INSTRUCTIONS

Entry point changes from "Read health/INSTRUCTIONS.md" to "Read INSTRUCTIONS.md and follow it."

## Career Domain

### Agents (3)

| Agent | Triggers | Role |
|---|---|---|
| Career Strategist | Goals, development plan, promotion, job change | Long-term strategy, action plans |
| Skills Coach | Skills, learning, courses, certifications | What to learn, priorities, progress |
| Interview Prep | Interviews, resume, preparation | Interview prep, question analysis |

### Commands

| Say | AI does |
|---|---|
| "interview me" | Fills career profile (position, experience, goals) |
| "weekly review" | Week summary, goal progress |
| "what should I focus on?" | Priorities based on goals and current progress |
| "prepare for interview at [company]" | Preparation plan |
| "add achievement: [description]" | Adds to achievements.md |

### Career INSTRUCTIONS.md scope

- Role definition: career analyst and advisor
- Session startup: read CAREER.md, check recent logs, check goals progress
- Data entry rules: append rows, ISO dates, confirm logged
- Agent routing table
- Analysis rules: compare against goals, track skill gaps, flag stagnation
- Weekly review format
- Smart suggestions ("what should I focus on?")
- Onboarding interview: current role, experience, skills, career goals, industry
- Scope: stay within career tracking, redirect health questions to health domain

## Changes to Existing Files

### health/INSTRUCTIONS.md — NO CHANGES

Stays exactly as is. The root INSTRUCTIONS.md wraps it without modifying it.

### README.md — UPDATE

- Title: "Me - Personal Life Tracker" (from "Health Tracker")
- Description: multi-domain (health, career, expandable)
- File structure: show both folders + root INSTRUCTIONS.md
- First Message: "Read INSTRUCTIONS.md and follow it"
- Add "Domains" section describing health and career
- Keep all existing health documentation

### PROJECT.md — UPDATE

- Title and description: multi-domain
- Structure: add career/ and root INSTRUCTIONS.md
- Status: add career tasks to Done/To Do

## Design Decisions

1. **Don't refactor health/** — it works, don't break it
2. **Root file is thin** — routing + formats only, no domain logic
3. **Each domain is self-contained** — can work independently if loaded directly
4. **Career mirrors health patterns** — same file naming (INSTRUCTIONS, agents, profile, logs), same conventions
5. **Future domains** (finance, learning) follow the same pattern — add folder + register in root INSTRUCTIONS
