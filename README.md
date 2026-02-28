# Me - Personal Health Tracker

AI-powered health tracking using plain Markdown files. No app, no code, no dependencies - just `.md` files and any AI assistant.

## How It Works

```
You describe anything in chat
        ↓
AI reads your health files for context
        ↓
AI updates tracker files + daily log
        ↓
AI spots patterns, correlations, and anomalies
```

**You talk. AI tracks.** Describe your meals, sleep, workouts, mood, in any format. AI parses it, logs it to the right files, and over time builds a picture of your health with insights you'd never spot yourself.

## Why This Exists

Most health apps lock your data in proprietary formats, require subscriptions, and work with one platform. This is different:

- **100% local** - your data never leaves your machine (except AI API calls)
- **Works with any AI** - Claude, GPT, Gemini, or any LLM that can read files
- **Works with any editor** - preconfigured for 7 AI editors (see below)
- **Plain text** - grep it, git it, own it forever
- **Zero setup** - clone, open in your editor, start talking

## Features

| Feature | What it does |
|---|---|
| **4 Specialist Agents** | Nutritionist, Coach, Medical Analyst, Recovery Coach, auto-selected by context |
| **Health Score** | Daily score (1-100) calculated from sleep, energy, mood, stress, activity |
| **Correlations** | Short-term (days) and long-term (weeks/months) pattern detection |
| **Early Warnings** | Flags symptom combinations that may need medical attention |
| **Smart Suggestions** | "What should I eat?" → AI checks your data and gives specific advice |
| **Daily Review** | Say "daily review" → score, trends, anomalies, recommendations |
| **Lab Import** | Drop a photo/PDF → AI extracts markers, flags out-of-range values |
| **Baselines** | After 2 weeks, AI calculates your personal norms and tracks deviations |
| **Goal Tracking** | Measurable goals with progress updated automatically |
| **Doctor Summary** | "Prepare for doctor visit" → one-page summary of meds, symptoms, labs, trends |

## Recommended Editors

The repo includes preconfigured instruction files — open the project and AI already knows what to do:

| Editor | Config file | Status |
|---|---|---|
| [Cursor](https://cursor.com) | `.cursor/rules/health-tracker.mdc` | ✅ Ready |
| [Antigravity](https://antigravity.dev) | `.antigravity/rules.md` | ✅ Ready |
| [Claude Code](https://claude.ai) | `CLAUDE.md` | ✅ Ready |
| [Windsurf](https://codeium.com/windsurf) | `.windsurfrules` | ✅ Ready |
| [GitHub Copilot](https://github.com/features/copilot) | `.github/copilot-instructions.md` | ✅ Ready |
| [ChatGPT](https://openai.com) | `chatgpt.md` | ✅ Ready |
| [Cline](https://cline.bot) | `.clinerules` | ✅ Ready |

Any other AI editor that can read files will also work — just point it to `health/INSTRUCTIONS.md`.

## Quick Start

1. **Download**: click the green `Code` button → `Download ZIP`, or clone with `git clone`
2. **Open** the project root folder in any editor from the list above — AI picks up instructions automatically
3. **Say**: *"Interview me to fill out my health profile"*. AI will ask about your goals, conditions, lifestyle, and fill in `profile.md` for you
4. **Upload** any medical documents you have (lab results, exam reports). AI will parse and organize them
5. **Start talking**: *"I slept 7 hours, had oatmeal for breakfast, ran 5km"*

That's it. AI reads the instructions and knows what to do. Your key info lives in `HEALTH.md` (navigation) and `profile.md` (your goals, conditions, baselines).

## Commands

| Say | AI does |
|---|---|
| "interview me" | First-time setup, AI asks questions and fills your profile |
| *describe your day* | Logs data to tracker files + daily log |
| "daily review" | Score + trends + recommendations |
| "what should I eat/do today?" | Smart suggestions based on your data |
| "weekly report" | Generates weekly health report |
| "doctor summary" | One-page summary for doctor visits |
| "ask the [coach/nutritionist/...]" | Forces a specific specialist agent |

## Quick Entry

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

## Example Interaction

**You:** "Yesterday slept from 11pm to 7am, quality was great. Had chicken and rice for lunch, ran 5km in 40 min. Feeling good, energy 8/7/6, mood 8, stress 2."

**AI:** `Logged: 2026-02-28 → sleep.md, nutrition.md, workouts.md, mood.md, logs/02.md`
`Score: 82/100`
`Insight: 3rd day in a row with 7+ hours sleep → energy trending up`

## Importing Data

| Data | How |
|---|---|
| **Lab results** | Drop a photo or PDF in chat → AI extracts markers into `labs/` |
| **Exam results** | Drop MRI, ultrasound, X-ray report → AI saves to `exams/` |
| **Wearable data** | Export JSON/CSV from your fitness app → drop in chat → AI parses into tables |

AI handles any format. Just drop the file and it figures out the rest.

## File Structure

```
health/
├── INSTRUCTIONS.md     # AI instructions + routing rules
├── HEALTH.md           # Navigation hub
├── agents.md           # 4 specialist personas
├── profile.md          # Goals, baselines, conditions
├── sleep.md            # Sleep tracker
├── nutrition.md        # Meals + water
├── workouts.md         # Training log
├── body.md             # Weight, BP, resting HR
├── mood.md             # Mood, energy, stress
├── supplements.md      # Supplements + medications
├── symptoms.md         # Symptoms tracker
├── wearable.md         # Wearable device data
├── logs/               # Daily summaries by month
├── labs/               # Lab results
├── exams/              # MRI, ultrasound, X-ray
└── reports/            # AI-generated reports
```

## Tracked Metrics

Sleep, energy, mood, stress, weight, blood pressure, heart rate, nutrition, workouts, supplements, medications, symptoms, lab results, examinations, wearable data.

## Privacy

All data stays on your machine as plain `.md` files. The only external calls are to the AI API when you interact, and even that can be local with Ollama or LM Studio.

## License

MIT
