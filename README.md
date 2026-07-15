# TriMate（三途）Endurance Coach Capabilities

TriMate is an endurance-coaching capability package for runners, cyclists, swimmers, triathletes, and trail-running athletes.

This public repository contains only the coach-facing capability definitions:

- Agent behavior rules.
- Endurance coaching skills.
- Skill reference material and evaluation examples.
- Public safety and license notes.

It does not include internal implementation files, storage schemas, user data, deployment scripts, private integrations, Garmin tokens, or project history.

## What TriMate Can Help With

TriMate is designed for ongoing endurance training support rather than one-off generic fitness advice.

- Record and interpret running, cycling, swimming, strength, triathlon, and trail-running sessions.
- Track body status such as fatigue, sleep, stress, soreness, pain, recovery, and mood.
- Analyze single workouts using recent training and recovery context.
- Review weekly and monthly trends.
- Estimate training load, acute load, chronic load, and ACWR-style risk signals.
- Identify injury-risk warning signs and suggest conservative next steps.
- Generate periodic training summaries for a week, four-week block, month, quarter, or year.
- Create long-term training plans only when the user explicitly asks for one.

## Included Skills

- `runner-assessment`: builds the athlete profile progressively.
- `body-assessment`: evaluates progress, plateau, regression, fatigue, and possible overload.
- `training-memory`: records training, body status, goals, preferences, and constraints.
- `workout-feedback`: gives context-aware feedback on a single workout.
- `training-load`: estimates training load and risk signals.
- `injury-risk`: handles pain and safety-related signals.
- `periodic-training-summary`: creates formal period summaries and share-card requirements.
- `weekly-review`: summarizes weekly or monthly trends.
- `training-plan`: creates or adjusts a long-term plan after explicit user request.

## Repository Layout

```text
agent-package/
  agent.md
  docs/
  skills/
LICENSE
SECURITY.md
README.md
```

## How To Use

Use `agent-package/agent.md` as the base coach instruction, then load the relevant skill under `agent-package/skills/` according to the user's request.

Examples:

- User sends a workout: use `training-memory` and `workout-feedback`.
- User asks whether they can increase training: use `body-assessment` and `training-load`.
- User reports pain: use `injury-risk`.
- User asks for a week or month summary: use `periodic-training-summary` or `weekly-review`.
- User asks for a race plan: use `training-plan`.

## Privacy Boundary

This repository is intentionally capability-only. Real users' training data, body status, conversations, account identifiers, private runtime configuration, and third-party tokens must stay outside this repository.

## Medical Safety

TriMate is not a medical device and does not diagnose disease or injury. If pain persists, worsens, changes movement form, or includes urgent symptoms such as chest discomfort, fainting, severe breathing difficulty, or neurological symptoms, users should reduce training load and seek qualified professional help.

## License

Apache License 2.0. See [LICENSE](LICENSE).
