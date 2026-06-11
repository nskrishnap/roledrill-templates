# RoleDrill — Ops Tools

## Setup
```bash
cd stackready
pip install boto3 --break-system-packages
aws configure  # ensure us-west-2 is set
```

## Dashboard
```bash
python3 ops/dashboard.py
```
Shows:
- Active users today
- Questions answered
- JD bundles created
- Top users (flags suspicious ones)
- Banned users list
- All-time stats

## Ban a User
```bash
# Ban
python3 ops/ban_user.py ban <user_id> "reason"

# Example
python3 ops/ban_user.py ban b8e1b390-8011-7011-de4c "Scraping questions"

# Unban
python3 ops/ban_user.py unban <user_id>

# List all banned
python3 ops/ban_user.py list
```
Effect is **immediate** — next API request returns 403.
Get user_id (Cognito sub) from dashboard output.

## Limits (enforced server-side)
| Action           | Free limit  | Env var                  |
|------------------|-------------|--------------------------|
| Questions/day    | 10          | DAILY_QUESTION_LIMIT     |
| JD bundles/day   | 3           | DAILY_JD_LIMIT           |
| JD max chars     | 3000        | (hardcoded in handler)   |

## Suspicious Activity Flags
Dashboard auto-flags:
- User hitting question limit repeatedly (≥10/day)
- User creating ≥5 JD bundles in one day
- Same IP hitting rate limit (API Gateway logs)

## CloudWatch Alarms (already set up)
- `stackready-prod-bedrock-spike` — >200 invocations/5min
- `stackready-prod-question-errors` — >5 errors/min
