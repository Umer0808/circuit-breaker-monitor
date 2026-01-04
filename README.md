# n8n Workflow Circuit Breaker

> Automated error monitoring and self-healing system for n8n workflows

## What It Does

This workflow automatically monitors errors from your n8n workflows and disables them if they fail too many times. Think of it as a safety switch that prevents runaway errors from wasting your execution quota.

## How It Works

1. **Error Webhook** - Receives errors from your workflows
2. **Workflow Configuration** - Set your threshold (e.g., 5 errors = disable)
3. **Extract Error Details** - Pulls relevant info from the error
4. **Track Error Count** - Counts how many times each workflow has failed
5. **Check Threshold** - Decides if it's safe or critical
   - **Safe Path** → Sends a standard Slack alert
   - **Critical Path** → Disables the workflow AND sends an emergency alert

## Setup

### 1. Get Your Credentials

- **n8n API Key**: Settings → API → Create API Key
- **Slack Webhook**: Create an incoming webhook for your channel

### 2. Configure the Workflow

- Add your n8n API key to the "Disable Source Workflow" node
- Add your Slack webhook to both Slack alert nodes
- Adjust the error threshold in "Workflow Configuration" (default: 5 errors)

### 3. Connect Your Workflows

In any workflow you want to monitor:
- Go to Workflow Settings
- Set "Error Workflow" to this Circuit Breaker workflow
- Save

## Configuration

Edit the **Workflow Configuration** node:

```javascript
{
  "maxErrors": 5,           // Disable after X errors
  "timeWindow": 10          // Within X minutes
}
```

## That's It!

Now your workflows are protected. When one fails too many times, it automatically shuts down and alerts your team.

---
