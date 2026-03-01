# Health Tracker

Personal health knowledge base. AI reads these files as context and updates them based on input.

## Getting Started

1. Say "interview me" — AI asks about your health, goals, and fills [profile.md](profile.md) for you
2. Upload medical documents (lab results, exams) — AI parses and organizes them
3. Start logging — describe your day in chat, AI handles the rest
4. Say "daily review" anytime — AI summarizes your day + Health Score (1-100)
5. After 2 weeks — AI calculates personal baselines and detects patterns

### Quick entry format

```
S:8h Q9 bed:23:00 wake:07:00 E:8/7/6 M:8 St:2 W:78kg Water:2000ml
```

## Files

| File | What |
|---|---|
| [profile.md](profile.md) | Goals, baselines, conditions |
| [sleep.md](sleep.md) | Sleep duration, quality |
| [nutrition.md](nutrition.md) | Meals, water |
| [workouts.md](workouts.md) | Training sessions |
| [body.md](body.md) | Weight, BP, resting HR |
| [mood.md](mood.md) | Mood, energy, stress |
| [supplements.md](supplements.md) | Supplements, medications |
| [symptoms.md](symptoms.md) | Headaches, pain, etc. |
| [wearable.md](wearable.md) | Wearable data |
| [agents.md](agents.md) | Specialist AI personas |
| [logs/](logs/) | Daily summaries by month |
| [labs/](labs/) | Lab results |
| [exams/](exams/) | MRI, ultrasound, X-ray |
| [reports/](reports/) | AI-generated reports |

## Commands

| Say | AI does |
|---|---|
| "interview me" | First-time setup — AI asks questions and fills your profile |
| *describe your day* | Logs data to tracker files + daily log |
| `S:8h Q9 E:7/6/5 M:7 St:3 W:78kg` | Quick entry — parsed automatically |
| "daily review" | Score + trends + recommendations |
| "what should I eat/do today?" | Smart suggestions based on your data |
| "weekly report" | Generates weekly health report |
| "doctor summary" | One-page summary for doctor visits |
| "ask the coach" | Forces a specific specialist agent |

## AI Instructions

See [HEALTH-INSTRUCTIONS.md](HEALTH-INSTRUCTIONS.md)
