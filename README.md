# Me - Personal Life Tracker

AI-powered life tracking using plain Markdown files. No app, no code, no dependencies - just `.md` files and any AI assistant.

## How It Works

```
You describe anything in chat
        ↓
AI reads your files for context
        ↓
AI updates tracker files + logs
        ↓
AI spots patterns, correlations, and anomalies
```

**You talk. AI tracks.** Describe your meals, sleep, workouts, career wins, skills you're learning — in any format. AI parses it, logs it to the right files, and over time builds a picture of your life with insights you'd never spot yourself.

## Why This Exists

Most tracking apps lock your data in proprietary formats, require subscriptions, and work with one platform. This is different:

- **100% local** - your data never leaves your machine (except AI API calls)
- **Works with any AI** - Claude, GPT, Gemini, or any LLM that can read files
- **Works with any editor** - any AI editor or chatbot, zero config
- **Plain text** - grep it, git it, own it forever
- **Zero setup** - clone, open in your editor, start talking

## Domains

| Domain | What it tracks |
|---|---|
| **[Health](health/)** | Sleep, nutrition, workouts, mood, energy, weight, labs, symptoms, supplements, wearable data |
| **[Career](career/)** | Goals, skills, achievements, interviews, networking, career journal |

Each domain has its own AI instructions, specialist agents, and tracker files. More domains coming.

## First Message

After opening the project in any AI editor or chatbot, send this as your first message:

> **Read INSTRUCTIONS.md and follow it.**

That's it. AI loads the instructions, detects which domain you need, and becomes your tracker. Works with Claude, GPT, Gemini, Cursor, Windsurf, or any other AI that can read files.

## Quick Start

1. **Download**: click the green `Code` button → `Download ZIP`, or clone with `git clone`
2. **Open** the project folder in any AI editor or chatbot
3. **Send**: *"Read INSTRUCTIONS.md and follow it."*
4. **First time only**: *"Interview me"*. AI will ask about your goals, background, and fill your profile
5. **Start talking**: *"I slept 7 hours, had oatmeal for breakfast, ran 5km"* or *"I finished the AWS course today"*

## Health Features

| Feature | What it does |
|---|---|
| **4 Specialist Agents** | Nutritionist, Coach, Medical Analyst, Recovery Coach — auto-selected by context |
| **Health Score** | Daily score (1-100) calculated from sleep, energy, mood, stress, activity |
| **Correlations** | Short-term (days) and long-term (weeks/months) pattern detection |
| **Early Warnings** | Flags symptom combinations that may need medical attention |
| **Smart Suggestions** | "What should I eat?" → AI checks your data and gives specific advice |
| **Daily Review** | Say "daily review" → score, trends, anomalies, recommendations |
| **Lab Import** | Drop a photo/PDF → AI extracts markers, flags out-of-range values |
| **Baselines** | After 2 weeks, AI calculates your personal norms and tracks deviations |
| **Goal Tracking** | Measurable goals with progress updated automatically |
| **Doctor Summary** | "Prepare for doctor visit" → one-page summary of meds, symptoms, labs, trends |

## Career Features

| Feature | What it does |
|---|---|
| **3 Specialist Agents** | Career Strategist, Skills Coach, Interview Prep — auto-selected by context |
| **Goal Tracking** | Career goals with progress, deadlines, and stagnation alerts |
| **Skills & Learning** | Track courses, certifications, skill development |
| **Interview Prep** | Preparation plans, STAR stories, post-interview debrief |
| **Achievements** | Log wins and impact for resume and interview prep |
| **Weekly Review** | Say "weekly review" → progress, priorities, recommendations |
| **Smart Suggestions** | "What should I focus on?" → priorities based on goals and data |

## Commands

| Say | AI does |
|---|---|
| "interview me" | First-time setup — AI asks questions and fills your profile |
| *describe your day* | Logs data to tracker files + daily log |
| "daily review" | Health score + trends + recommendations |
| "weekly review" | Career progress + priorities |
| "what should I eat/do today?" | Smart suggestions based on your health data |
| "what should I focus on?" | Career priorities based on goals and data |
| "doctor summary" | One-page health summary for doctor visits |
| "prepare for interview at [company]" | Interview preparation plan |
| "ask the [coach/nutritionist/strategist/...]" | Forces a specific specialist agent |

## Quick Entry (Health)

Instead of writing full sentences, you can use shorthand:

```
S:8h Q9 E:8/7/6 M:8 St:2 W:78kg BP:120/80 HR:65 Water:2000ml
```

| Code | Meaning |
|---|---|
| S | Sleep hours |
| Q | Sleep quality (1-10) |
| E | Energy: morning/afternoon/evening (1-10) |
| M | Mood (1-10) |
| St | Stress (1-10) |
| W | Weight |
| BP | Blood pressure |
| HR | Resting heart rate |

All fields are optional. Just send what you have.

## Example Interactions

**Health:**
> "Yesterday slept from 11pm to 7am, quality was great. Had chicken and rice for lunch, ran 5km in 40 min."
>
> AI: `Logged: 2026-02-28 → sleep.md, nutrition.md, workouts.md` / `Score: 82/100`

**Career:**
> "I finished the AWS Solutions Architect course and passed the practice exam."
>
> AI: `Logged: 2026-03-01 → skills.md, achievements.md` / `Goal 'AWS cert' → 80% complete`

## File Structure

```
├── INSTRUCTIONS.md          # AI instructions + domain routing
├── health/
│   ├── HEALTH-INSTRUCTIONS.md # Health AI instructions
│   ├── HEALTH.md            # Navigation hub
│   ├── agents.md            # 4 specialist personas
│   ├── profile.md           # Goals, baselines, conditions
│   ├── sleep.md             # Sleep tracker
│   ├── nutrition.md         # Meals + water
│   ├── workouts.md          # Training log
│   ├── body.md              # Weight, BP, resting HR
│   ├── mood.md              # Mood, energy, stress
│   ├── supplements.md       # Supplements + medications
│   ├── symptoms.md          # Symptoms tracker
│   ├── wearable.md          # Wearable device data
│   ├── logs/                # Daily summaries by month
│   ├── labs/                # Lab results
│   ├── exams/               # MRI, ultrasound, X-ray
│   └── reports/             # AI-generated reports
└── career/
    ├── CAREER-INSTRUCTIONS.md # Career AI instructions
    ├── CAREER.md            # Navigation hub
    ├── agents.md            # 3 specialist personas
    ├── profile.md           # Current role, experience, goals
    ├── goals.md             # Career goals with progress
    ├── skills.md            # Skills, courses, certifications
    ├── network.md           # Contacts, mentors, references
    ├── interviews.md        # Interview prep and history
    ├── achievements.md      # Projects, wins, resume items
    ├── journal.md           # Reflection and thinking
    └── logs/                # Weekly reviews by month
```

## Importing Data

| Data | How |
|---|---|
| **Lab results** | Drop a photo or PDF in chat → AI extracts markers into `health/labs/` |
| **Exam results** | Drop MRI, ultrasound, X-ray report → AI saves to `health/exams/` |
| **Wearable data** | Export JSON/CSV from your fitness app → drop in chat → AI parses into tables |

AI handles any format. Just drop the file and it figures out the rest.

## Privacy

All data stays on your machine as plain `.md` files. The only external calls are to the AI API when you interact, and even that can be local with Ollama or LM Studio.

## License

MIT
