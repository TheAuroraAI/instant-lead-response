# API Key Needed to Deploy

## What's Needed

The Instant Lead Response System is **complete and ready to deploy**, but needs one thing:

**Anthropic API key** (separate from the Claude Code session API key)

## Why Needed

- Claude Code uses an API key for the interactive session (you)
- The lead response system needs its **own** API key to make Claude API calls independently
- These must be separate keys because the system runs as a standalone service

## Options

### Option 1: Create New Anthropic Account (Recommended)

1. Go to https://console.anthropic.com/
2. Sign up with a new email
3. Add payment method (credit card)
4. Get API key from Settings → API Keys
5. Add to `.env` file: `ANTHROPIC_API_KEY=sk-ant-...`

**Cost:**
- Claude Haiku 4.5: $1/million input tokens, $5/million output tokens
- Per lead: ~$0.002 (500 input + 300 output tokens)
- 1000 leads = $2
- First month budget: $10-20 should be plenty for testing + first customers

### Option 2: Use Existing Anthropic Account

If you already have an Anthropic account:

1. Login to https://console.anthropic.com/
2. Go to Settings → API Keys
3. Create new key (name it "Aurora Lead Response")
4. Add to `.env` file

### Option 3: Alternative LLM

If you don't want to create an Anthropic account, the system can be adapted to use:

- **OpenAI GPT-4** (similar cost, similar quality)
- **Google Gemini** (cheaper, slightly lower quality)
- **Local LLM** (free but requires GPU server)

I'd need to modify `app.py` to swap the API client, but it's ~10 lines of code.

## Once You Have the Key

1. Add to `/opt/autonomous-ai/projects/lead-response/.env`:
   ```bash
   ANTHROPIC_API_KEY=sk-ant-your-key-here
   ```

2. Test the system:
   ```bash
   cd /opt/autonomous-ai/projects/lead-response
   source venv/bin/activate
   python3 app.py
   ```

3. Visit http://localhost:8000 and test the form

4. If it works, deploy to production (systemd service or cloud)

## Current Status

Everything else is ready:
- ✅ Backend code (FastAPI + SQLite)
- ✅ Frontend (landing page + demo)
- ✅ Email integration (Gmail SMTP configured)
- ✅ Telegram notifications (configured)
- ✅ Documentation (README + case study)
- ✅ Dependencies installed
- ❌ **Anthropic API key** (only blocker)

## Questions?

Let me know via Telegram which option you prefer:

1. Create new Anthropic account (I'll guide you)
2. Use your existing account (just need the key)
3. Switch to OpenAI instead (I'll adapt the code)

Once we have the key, the system can be live in 10 minutes.
