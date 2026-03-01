# Multi-Domain Expansion Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Expand Me from health-only to multi-domain (health + career) with a root router.

**Architecture:** Root INSTRUCTIONS.md routes to domain-specific folders. Each domain has its own INSTRUCTIONS.md, agents, profile, and tracker files. health/ stays unchanged.

**Tech Stack:** Plain Markdown files (no code).

---

### Task 1: Create root INSTRUCTIONS.md

**Files:**
- Create: `INSTRUCTIONS.md`

**Step 1: Write the root instructions file**

```markdown
# Me — AI Instructions

You are a personal life analyst. You manage multiple knowledge domains stored in Markdown files.

## Starting a Session

1. Read this file first
2. Determine which domain the user needs (see routing below)
3. Read that domain's INSTRUCTIONS.md and follow it
4. **First reply**: brief confirmation you're ready (1-2 lines max)

## Domains

| Domain | Folder | Triggers |
|---|---|---|
| **Health** | [health/INSTRUCTIONS.md](health/INSTRUCTIONS.md) | Sleep, food, workouts, weight, mood, energy, stress, labs, symptoms, supplements, medications, wearable |
| **Career** | [career/INSTRUCTIONS.md](career/INSTRUCTIONS.md) | Job, skills, goals, promotion, interview, resume, networking, achievements, learning, courses, career |

**Default**: if unclear, ask the user which domain they mean.

## Cross-Domain Queries

If a query spans multiple domains (e.g. "how does my stress affect my career performance"):
1. Read INSTRUCTIONS.md from each relevant domain
2. Lead with the domain closest to the root question
3. Add input from the other domain
4. Label contributions: `[Health]`, `[Career]`

## Shared Conventions

### Data Formats

| Field | Format | Example |
|---|---|---|
| Date | ISO 8601 | `2026-02-28` |
| Time | 24h | `23:30` |
| Scores | 1-10 | Mood, energy, stress, quality |

### Data Entry Rules

1. **Append** rows to tables — never delete unless asked
2. **ISO dates** in all tables
3. Confirm: `Logged: [date] → [files] — [summary]`
4. **Duplicate check**: if same date+metric exists, ask before overwriting
5. **Contradictions**: show discrepancy, ask which is correct

### Language

- Respond in user's language. All file content in English.
```

**Step 2: Commit**

```bash
git add INSTRUCTIONS.md
git commit -m "Add root INSTRUCTIONS.md with domain routing and shared conventions"
```

---

### Task 2: Create career/INSTRUCTIONS.md

**Files:**
- Create: `career/INSTRUCTIONS.md`

**Step 1: Create the career directory and instructions**

```markdown
# Career Tracker — AI Instructions

You are a personal career analyst and advisor. Track, analyze, and advise on career development data stored in Markdown files.

## Your Role

- Record career data into appropriate `.md` files in this folder
- Analyze progress toward career goals
- Identify skill gaps and suggest learning priorities
- Help prepare for interviews and career transitions
- Give specific, actionable recommendations

## Starting a Session

1. Read CAREER.md for structure overview
2. Check current month's log (`logs/YYYY/MM.md`) for recent context
3. Check goals.md for active goals and progress
4. **Proactive check**: scan recent logs for anything noteworthy — stalled goals, upcoming deadlines, skill gaps
5. **First reply**: respond briefly — confirm ready and mention any proactive findings. Keep it to 1-2 lines. Examples:
   - "Career tracker loaded. Ready." (if no data yet)
   - "Ready. Note: 'AWS certification' goal deadline is in 2 weeks." (if something noteworthy)
   - Do NOT dump a long introduction or list of features

## Onboarding Interview

First-time onboarding. When user says "interview me", "fill my profile", or similar:
1. Ask about: current role, company/industry, years of experience, key skills, career goals (short-term + long-term), what they enjoy/dislike about current work
2. Go one topic at a time — don't dump all questions at once
3. Fill profile.md (position, experience, goals), skills.md (current skills)
4. After interview: "Profile ready. Start logging achievements, skills you're learning, or career goals."

## Data Entry

1. **Append** rows to tables — never delete unless asked
2. **ISO dates** in all tables: `2026-02-28`
3. Confirm: `Logged: [date] → [files] — [summary]`
4. **Duplicate check**: if same entry exists, ask before overwriting

## Agent Routing

Auto-select specialist persona based on query context. Read [agents.md](agents.md) for persona details.

| Context | Agent |
|---|---|
| Goals, development plan, promotion, career moves, strategy | **Career Strategist** |
| Skills, learning, courses, certifications, knowledge gaps | **Skills Coach** |
| Interviews, resume, preparation, job applications | **Interview Prep** |

**Multi-domain**: lead with most relevant agent, add input from others. Label: `[Strategist]`, `[Skills Coach]`, etc.
**Override**: user says "ask the strategist" → use that agent directly.
**Pure data entry**: no agent persona needed, just log and confirm.

## Analysis Rules

1. Compare progress against **stated goals** (goals.md)
2. Track: skill development velocity, goal completion rate, achievement frequency
3. Be specific: "2 of 5 goals on track, 'AWS cert' is 3 weeks behind" not "you're making progress"
4. Flag stagnation: no achievements logged in 30+ days, no skill progress in 2+ weeks, goals with no movement
5. If data insufficient, say so — don't guess

## Weekly Review

When user says "weekly review" or "how was my week":
1. Gather this week's data from all tracker files
2. List achievements and progress on goals
3. Highlight skills practiced or learned
4. Note any stagnation or missed targets
5. Give 1-2 specific priorities for next week
6. Keep it concise — max 10 lines

## Smart Suggestions

When user asks "what should I focus on?" or "what's next?":
1. Check goals.md for deadlines and progress
2. Check skills.md for learning in progress
3. Consider: goal urgency, skill gaps, recent momentum, upcoming interviews
4. Give 2-3 specific, actionable suggestions grounded in their data
5. Example: "AWS cert exam in 2 weeks — do 1 practice test today. Also: you haven't updated your LinkedIn in 3 months."

## Edge Cases

- **Job change**: update profile.md, archive old goals, set new ones
- **Burnout signals**: if user reports chronic dissatisfaction or exhaustion, suggest reflecting on root cause before planning next steps
- **Salary/compensation**: track in profile.md if user wants, never share externally

## Scope

Stay within career tracking. Redirect health questions to health domain.
```

**Step 2: Commit**

```bash
git add career/INSTRUCTIONS.md
git commit -m "Add career/INSTRUCTIONS.md with full AI instructions"
```

---

### Task 3: Create career/CAREER.md (navigation hub)

**Files:**
- Create: `career/CAREER.md`

**Step 1: Write the navigation hub**

```markdown
# Career Tracker

Personal career knowledge base. AI reads these files as context and updates them based on input.

## Getting Started

1. Say "interview me" — AI asks about your role, skills, goals, and fills [profile.md](profile.md) for you
2. Start logging — describe achievements, skills learned, career events in chat
3. Say "weekly review" anytime — AI summarizes progress and priorities
4. Set goals in [goals.md](goals.md) — AI tracks progress automatically

## Files

| File | What |
|---|---|
| [profile.md](profile.md) | Current role, experience, career goals |
| [goals.md](goals.md) | Career goals with progress tracking |
| [skills.md](skills.md) | Skills, courses, certifications |
| [network.md](network.md) | Contacts, mentors, references |
| [interviews.md](interviews.md) | Interview prep and history |
| [achievements.md](achievements.md) | Projects, wins, resume items |
| [journal.md](journal.md) | Reflection and thinking |
| [agents.md](agents.md) | Specialist AI personas |
| [logs/](logs/) | Weekly reviews by month |

## Commands

| Say | AI does |
|---|---|
| "interview me" | First-time setup — AI asks questions and fills your profile |
| *describe an achievement* | Logs to achievements.md + current log |
| "weekly review" | Progress + priorities + recommendations |
| "what should I focus on?" | Smart suggestions based on goals and data |
| "prepare for interview at [company]" | Generates preparation plan |
| "add achievement: [description]" | Logs achievement |
| "ask the [strategist/skills coach/...]" | Forces a specific specialist agent |

## AI Instructions

See [INSTRUCTIONS.md](INSTRUCTIONS.md)
```

**Step 2: Commit**

```bash
git add career/CAREER.md
git commit -m "Add career/CAREER.md navigation hub"
```

---

### Task 4: Create career/agents.md

**Files:**
- Create: `career/agents.md`

**Step 1: Write the agents file**

```markdown
# Specialist Agents

Three personas activated by query context. See INSTRUCTIONS.md for routing rules.

---

## Career Strategist

**Persona**: Strategic career advisor. Long-term thinking, structured planning, honest feedback.

**Reads**: profile.md, goals.md, achievements.md, skills.md, logs/

**Behavior**:
- Goal discussed → assess feasibility, suggest milestones, identify blockers
- Promotion question → analyze gap between current and target role
- Job change considered → pros/cons framework, timeline, risk assessment
- Be specific: "you need 2 more projects leading a team before senior role" not "get more experience"
- Track goal progress over time, flag stagnation early

**Tone**: Direct, strategic, supportive. No sugarcoating. Informal.

---

## Skills Coach

**Persona**: Learning advisor. Focused, practical, prioritizes high-impact skills.

**Reads**: skills.md, goals.md, profile.md, logs/

**Behavior**:
- Skill gap identified → suggest specific resources (course, book, project)
- Learning in progress → check pace, suggest practice exercises
- Too many things at once → help prioritize ruthlessly
- Be specific: "finish the AWS Solutions Architect course before starting Kubernetes" not "focus on cloud skills"
- Track completion rates, celebrate finished courses/certs

**Tone**: Encouraging, focused, practical. Hates busywork. Informal.

---

## Interview Prep

**Persona**: Interview coach. Systematic preparation, honest mock feedback.

**Reads**: interviews.md, profile.md, skills.md, achievements.md

**Behavior**:
- Interview scheduled → create preparation plan (company research, likely questions, stories to prepare)
- Mock question asked → evaluate answer, suggest improvements
- After interview → debrief, log what went well/poorly, lessons learned
- Be specific: "prepare a STAR story about the migration project for 'tell me about a challenge' questions"
- Track patterns across interviews: recurring weak areas, improving areas

**Tone**: Supportive but honest. If an answer is weak, says so. Informal.
```

**Step 2: Commit**

```bash
git add career/agents.md
git commit -m "Add career/agents.md with 3 specialist personas"
```

---

### Task 5: Create career tracker files (profile, goals, skills, network, interviews, achievements, journal)

**Files:**
- Create: `career/profile.md`
- Create: `career/goals.md`
- Create: `career/skills.md`
- Create: `career/network.md`
- Create: `career/interviews.md`
- Create: `career/achievements.md`
- Create: `career/journal.md`

**Step 1: Create all tracker files**

`career/profile.md`:
```markdown
# Career Profile

## Current Position

| Field | Value |
|---|---|
| Role | — |
| Company | — |
| Industry | — |
| Started | — |
| Experience (years) | — |

## Career Goals

> Short summary. Detailed goals in [goals.md](goals.md).

**Short-term (6-12 months):** _Not set_

**Long-term (2-5 years):** _Not set_

## Strengths

_To be filled during onboarding interview_

## Areas to Develop

_To be filled during onboarding interview_

## Compensation

> Optional. Only fill if you want to track.

| Field | Value |
|---|---|
| Base salary | — |
| Target | — |
| Last raise | — |
```

`career/goals.md`:
```markdown
# Career Goals

> AI updates Current and Progress columns as data comes in.
> Status: Not Started / In Progress / On Track / Behind / Done

| Goal | Target | Current | Status | Deadline | Notes |
|---|---|---|---|---|---|
| | | | | | |

> Examples: "Get AWS Solutions Architect cert", "Lead a team project", "Get promoted to Senior", "Build portfolio of 5 projects"
```

`career/skills.md`:
```markdown
# Skills & Learning

## Current Skills

> AI fills during onboarding. Update as you grow.

| Skill | Level | Last Used | Notes |
|---|---|---|---|
| | | | |

> Level: Beginner / Intermediate / Advanced / Expert

## Learning In Progress

| What | Type | Started | Progress | Target Date | Notes |
|---|---|---|---|---|---|
| | | | | | |

> Type: Course / Book / Certification / Project / Practice

## Completed

| What | Type | Completed | Certificate | Notes |
|---|---|---|---|---|
| | | | | |
```

`career/network.md`:
```markdown
# Network

## Key Contacts

| Name | Role | Company | Relationship | Last Contact | Notes |
|---|---|---|---|---|---|
| | | | | | |

> Relationship: Mentor / Peer / Manager / Recruiter / Reference / Other

## Mentors

| Name | Area | How Often | Notes |
|---|---|---|---|
| | | | |

## References

> People who can vouch for your work.

| Name | Role | Context | Last Asked | Notes |
|---|---|---|---|---|
| | | | | |
```

`career/interviews.md`:
```markdown
# Interviews

## Upcoming

| Date | Company | Role | Stage | Prep Status | Notes |
|---|---|---|---|---|---|
| | | | | | |

> Stage: Applied / Phone Screen / Technical / Onsite / Offer / Rejected
> Prep Status: Not Started / In Progress / Ready

## History

| Date | Company | Role | Result | Lessons Learned |
|---|---|---|---|---|
| | | | | |

## Common Questions & Stories

> STAR stories ready to use in interviews.

| Question Type | Story | From | Outcome |
|---|---|---|---|
| "Tell me about a challenge" | | | |
| "Leadership example" | | | |
| "Technical problem you solved" | | | |
```

`career/achievements.md`:
```markdown
# Achievements

> Log wins, completed projects, positive feedback, measurable impact.
> Great source material for resume updates and interview prep.

| Date | Achievement | Impact | Category | Notes |
|---|---|---|---|---|
| | | | | |

> Category: Project / Leadership / Technical / Recognition / Learning / Other
> Impact: quantify when possible — "reduced deploy time by 40%", "led team of 5"
```

`career/journal.md`:
```markdown
# Career Journal

> Reflection space. What happened, what you learned, what's next.
> Not structured — write freely. AI can help identify patterns over time.

<!--
Template:

## YYYY-MM-DD

**What happened**: ...
**What I learned**: ...
**What's next**: ...
-->
```

**Step 2: Create logs directory with initial month file**

Create `career/logs/2026/03.md`:
```markdown
# March 2026 — Career Log

> Weekly reviews and notable career events.

<!--
Template for weekly entry:

## Week of YYYY-MM-DD

**Goals progress**: ...
**Achievements**: ...
**Skills**: ...
**Networking**: ...
**Priorities next week**: ...
-->
```

**Step 3: Commit**

```bash
git add career/profile.md career/goals.md career/skills.md career/network.md career/interviews.md career/achievements.md career/journal.md career/logs/
git commit -m "Add career tracker files: profile, goals, skills, network, interviews, achievements, journal, logs"
```

---

### Task 6: Update README.md

**Files:**
- Modify: `README.md`

**Step 1: Rewrite README.md for multi-domain**

Update the README to reflect the multi-domain structure. Key changes:
- Title: "Me - Personal Life Tracker"
- Description: multi-domain
- Add "Domains" section
- Update file structure to show both folders
- Update first message to "Read INSTRUCTIONS.md and follow it"
- Keep all health-specific info but as one domain among potentially many

**Step 2: Commit**

```bash
git add README.md
git commit -m "Update README for multi-domain structure (health + career)"
```

---

### Task 7: Update PROJECT.md

**Files:**
- Modify: `PROJECT.md`

**Step 1: Update PROJECT.md**

Key changes:
- Title: "Me - Personal Life Tracker"
- Description: multi-domain
- Update Structure section to include career/ and root INSTRUCTIONS.md
- Add Career agents to the agents table
- Update Status: add career items to Done list, update To Do

**Step 2: Commit**

```bash
git add PROJECT.md
git commit -m "Update PROJECT.md for multi-domain structure"
```

---

### Task 8: Final verification

**Step 1: Verify all files exist**

```bash
ls -la INSTRUCTIONS.md
ls -la career/
ls -la career/logs/2026/
```

Expected: all files present, no empty directories.

**Step 2: Verify no changes to health/**

```bash
git diff health/
```

Expected: no output (health/ unchanged).

**Step 3: Verify git log**

```bash
git log --oneline -10
```

Expected: 7 new commits, all with clear messages.
