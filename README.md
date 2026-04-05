# 🤖 n8n Workflows

Personal collection of self-hosted n8n automation workflows.

---

## 📋 Agent Schedule Updater

### Overview
A Telegram-triggered workflow that automatically fetches the latest agent schedules via an external API, processes the data, and updates a shared Google Sheet that the team uses to view shift timings.

### Flow
```
Telegram Trigger → Read Agents Sheet → Validate → HTTP Request (Schedule API)
→ Format Data (JS) → Update Shared Sheet → Notify via Telegram
```

### What it does
1. **Triggered** by a Telegram message
2. **Reads** the agents list from a Google Sheet (name, gender, status, group, WFH/WFC)
3. **Validates** the request — sends a confirmation or error message via Telegram
4. **Fetches** the updated schedule from an external API
5. **Processes** the response using JavaScript to map agent names to their shifts
6. **Updates** the shared team Google Sheet with the new schedule (append or update)
7. **Notifies** the team via Telegram when the update is complete

### Stack
- **n8n** (self-hosted)
- **Telegram Bot API** — trigger & notifications
- **Google Sheets** — agents data source & shared schedule output
- **HTTP Request** — external schedule API
- **JavaScript** — data formatting and mapping

### Sheet Structure
| Column | Description |
|--------|-------------|
| Name | Agent full name |
| Sun–Sat | Shift times per day (e.g. `X: 07:00–16:00`) |
| OFF | Days off count |

### Error Handling
- If the Google Sheet read fails → sends a **"Sheet error"** message via Telegram
- If the request is invalid → sends a **"Request received"** acknowledgment and stops

---

## 🛠️ Setup

### Requirements
- Self-hosted n8n instance
- Telegram Bot token
- Google Sheets API credentials (OAuth2)
- Access to the schedule API endpoint

### Credentials needed in n8n
- `Telegram API` — Bot token
- `Google Sheets OAuth2` — for reading and writing sheets

---

## 📁 Files

| File | Description |
|------|-------------|
| `agent-schedule-updater.json` | Main workflow — fetches and updates agent schedules |

---

## 👤 Author
**Munther** — [@abozoz](https://github.com/abozoz)  
Self-hosted on a personal Debian server via Docker + Cloudflare Tunnel
