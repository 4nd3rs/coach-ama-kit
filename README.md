# Your own AI endurance coach

An AI coach for cycling, running, triathlon and HYROX that runs on your own
computer in **Claude Code** (Anthropic) or **Codex** (OpenAI). Both are AI
assistants that read files in a folder and can run small commands. This folder
is the coach: its instructions, its training science, your athlete file, and a
small tool that talks to your [intervals.icu](https://intervals.icu) calendar.

It builds and maintains a periodized plan around your goal and your week. It
writes structured workouts straight to intervals.icu, and from there to Garmin,
Wahoo or Zwift. It also does readiness checks, debriefs, 10-day plan upkeep,
weekly and monthly reviews, race planning and strength sessions.

It started as [Coach AMA](https://coach-ama.com), a coaching service that ran
in Discord. As the service closes, its coaching is opened up here as a kit.
Anyone can use it, and you don't need to have been a Coach AMA athlete. If you
were, you can bring your history along (see "Coming from Coach AMA" below).

**What you need:**
- A free [intervals.icu](https://intervals.icu) account with your training
  synced to it, from Garmin, Wahoo, Zwift, COROS, Polar or Suunto.
- Claude Code or Codex (below).
- A Mac or Linux computer. On Windows, use WSL: run `wsl --install` in
  PowerShell, restart, open **Ubuntu** from the Start menu, and follow the
  Linux instructions in that window from then on.

**How it works:** you open the coach when you want it, for example "morning"
over coffee or "debrief" after a ride. It doesn't message you on its own.

**Cost:** Claude Code needs a Claude Pro or Max plan. Codex comes with
ChatGPT plans; check [OpenAI's pricing](https://chatgpt.com/pricing) for which
plans include it. There are no separate API keys and no per-message billing.
Coaching use is light, so the entry-level plan is usually enough.

**Time to set up:** about 10 minutes, and the AI does most of it.

---

## Quick setup: let the AI do it

1. **Install Claude Code or Codex** and sign in.
   - Claude Code: on a Mac, the Claude desktop app's **Code** tab works.
     Otherwise run `curl -fsSL https://claude.ai/install.sh | bash` in a terminal.
   - Codex: on a Mac, the Codex app works. Otherwise run
     `curl -fsSL https://chatgpt.com/codex/install.sh | sh` in a terminal.
   - Windows: use the terminal commands, inside WSL's Ubuntu window.
2. **Make an empty folder called `coach`** (in your home folder, for example).
   Open it in the app (Mac), or in a terminal:
   `mkdir -p ~/coach && cd ~/coach && claude` (or `codex`).
3. **Paste this message:**

   > Set up my endurance coach. Download the coach kit from
   > https://github.com/4nd3rs/coach-ama-kit into this folder, then read
   > AGENTS.md and follow routines/setup.md step by step. Do the technical
   > work yourself and only ask me for what you need.

The AI downloads the kit, checks that everything works and offers to run your
first session. In that session it gets to know you, reads your training
history from intervals.icu and books your first 10 days. You do two things
yourself, because they need your logins:

- copy your intervals.icu API key when it asks
- approve the commands it wants to run

Already have the kit? Open its folder and type `/setup` (Claude Code) or say
"set me up" (Codex).

The rest of this README is the manual route, plus reference for later.

---

## 1. Get your intervals.icu API key

1. Open <https://intervals.icu/settings>.
2. Scroll to **Developer Settings** near the bottom and generate an **API key**.
3. Copy it. Treat it like a password: anyone with it can read and edit your
   training calendar.

## 2. Get the kit

Download this folder (or `git clone` it) somewhere you'll find again, e.g.
`~/coach`. Then, in a terminal:

```bash
cd ~/coach
cp .env.example .env
```

Open `.env` in any text editor and paste your key after `INTERVALS_API_KEY=`.
Leave `INTERVALS_ATHLETE_ID=0`, which means "the athlete who owns this key".

Check that it works:

```bash
bin/icu check         # should say "ok: connected to intervals.icu as <you>"
```

(Windows: run all of this inside WSL; the helper is a bash script.)

## 3. Coming from Coach AMA (optional)

Former Coach AMA athletes only. Everyone else can skip this step.

While coach-ama.com is still up, sign in at <https://coach-ama.com/dashboard>
and use **Download your coaching data**. You get `coach-ama-data.zip`, which holds:

| File | What it is |
|------|------------|
| `USER.md` | your athlete profile, as the coach knew you |
| `PLAN.md` | your training plan and the reasoning behind it |
| `LEARNINGS.md` | what the coach learned works (and doesn't) for you |
| `history_chat.md`, `history_agreements.md`, `history_session-feedback.md`, `history_tests.md` | your chat history, agreements, session feedback and test results (only the ones you have) |

Import it into the kit:

```bash
bin/import-data                      # finds the newest coach-ama-data*.zip in ~/Downloads
bin/import-data ~/path/to/coach-ama-data.zip
```

It copies only those files into `athlete/` and backs up anything it replaces.
Your new coach then starts where Coach AMA left off: your goals, your plan,
what works for you. The download stays available for a while after Coach AMA
closes, then everything is deleted, so grab it in time.

During AI setup, the coach asks about this and imports the zip for you.

## 4a. Run it with Claude Code

Install (macOS / Linux / WSL):

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

On Windows, run it inside WSL (see "What you need"). On a Mac you can also use
the Claude desktop app's **Code** tab and open the coach folder there.

Start it inside the kit folder and sign in with your Claude account:

```bash
cd ~/coach
claude
```

Claude Code reads `CLAUDE.md`, which loads the coach instructions. The kit
pre-approves reading your intervals.icu data, so it won't ask about that. Any
calendar change (create, update, delete) still shows you a permission prompt.
That prompt is your final OK. Type commands, or just talk:

| Type | What happens |
|------|-------------|
| `/setup` | Check the connection and get started (and import Coach AMA data, if you have it) |
| `/first-session` | Onboarding: the coach gets to know you and books your first 10 days |
| `/morning` | Readiness check plus today's session, adjusted if needed |
| `/debrief` | Review of your latest session (add a note: `/debrief legs felt heavy`) |
| `/plan` | Keep the next 10 days booked and aligned with your plan |
| `/weekly` | Sunday review of the week |
| `/monthly` | Honest 4–5 week audit and what changes |
| anything else | "Can I move Thursday's intervals to Friday?", "I'm sick", "I signed up for Vätternrundan" |

## 4b. Run it with Codex

Install (macOS / Linux):

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh     # or: npm install -g @openai/codex
```

Codex's sandbox blocks network access by default, and the coach needs it to
reach intervals.icu. Allow it once in `~/.codex/config.toml`:

```toml
[sandbox_workspace_write]
network_access = true
```

Then start it in the kit folder and sign in with your ChatGPT account:

```bash
cd ~/coach
codex
```

Codex reads `AGENTS.md` (the coach instructions) automatically. It has no
slash commands for the routines, so just say what you want: *"run the morning
check"*, *"debrief yesterday's ride"*, *"plan the next 10 days"*, *"weekly
review"*, *"let's do the first session"*, *"set me up"*. The coach finds the matching file in
`routines/`. Approve the `bin/icu` commands when Codex asks.

## 5. How to use it well

- **Talk to it like a coach.** Short messages work. Tell it
  how sessions felt, when life gets busy, when something hurts.
- **It shows changes before writing them.** Before creating, moving or deleting
  calendar workouts, the coach lists the change and waits for your OK. "Go ahead"
  is enough. It only edits its own workouts (named `[Coach] …`, or `[AMA] …`
  if you came from Coach AMA), never your club rides or your own entries, unless you ask.
- **Its memory is the `athlete/` folder.** `USER.md` (you), `PLAN.md` (the
  plan and why), `LEARNINGS.md` (what works for you). They're plain text, so read
  and correct them whenever you like. Back the folder up; if you lose it, the
  coach forgets you.
- **Start a fresh session now and then.** Each session starts by reading your
  files, so nothing is lost. Long sessions just get slower.

### Optional: a morning note without opening the app

Both tools can run one-off, non-interactive commands, so you can schedule them
(cron, or launchd on macOS). For example, every morning at 07:30:

```cron
30 7 * * * cd ~/coach && claude -p "/morning" > ~/coach/morning.txt 2>&1
30 7 * * * cd ~/coach && codex exec "run the morning check from routines/morning.md" > ~/coach/morning.txt 2>&1
```

Use one line, not both. Open the coach interactively once first (and accept the
folder-trust prompt), or the scheduled run won't get its pre-approved permissions.
Scheduled runs can't ask for your OK, so the coach
proposes calendar changes in the note instead of writing them. Read the note,
then open the coach to apply anything.

## Your data and privacy

- Your training data goes from intervals.icu to Anthropic or OpenAI under
  **your own** account and their terms. Nobody else is in the loop.
- Your API key stays in `.env` on your machine. The coach is told never to read
  that file, and Claude Code also blocks its file reader from opening it. Only
  `bin/icu` uses the key. During setup you can paste the key into the chat (it's then in that
  chat's history) or into `.env` yourself. The coach offers both.
- To revoke access, delete the API key in intervals.icu → Settings → Developer
  Settings.

## What's in the box

```
AGENTS.md           the coach: persona, rules, how to use intervals.icu (Codex reads this)
CLAUDE.md           tells Claude Code to load AGENTS.md
athlete/            YOUR files: USER.md, PLAN.md, LEARNINGS.md (+ history_*.md if imported from Coach AMA)
reference/          training science per sport, the pro-coach playbooks, the strength library
routines/           setup, morning, debrief, plan, weekly, monthly, first-session
bin/icu             tiny intervals.icu API helper (bash + curl); `bin/icu check` tests the setup
bin/import-data     imports a Coach AMA download into athlete/ (former Coach AMA athletes)
workouts/           where the coach drafts workouts before posting them (+ format examples)
.claude/            slash commands and permissions for Claude Code
```

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Anything in setup | Ask the coach: "run the setup check". It runs `bin/icu check` and walks you through the fix. |
| `bin/icu profile` says 401 / 403 | Wrong or revoked key. Generate a new one and paste it into `.env`. |
| `INTERVALS_API_KEY: Set …` | `.env` is missing or not in the kit folder. Redo step 2. |
| Codex says the network is blocked | Add the `network_access = true` block from step 4b and restart Codex. |
| Workouts show up as plain text, not steps | Ask the coach to re-write the workout as structured steps. The step syntax is in AGENTS.md. |
| A workout's zone or pace looks wrong | Usually the label trap: a bare "Z2" or "60%" in a step label. Ask the coach to check the label rules. |
| Workouts don't reach Garmin, Wahoo or Zwift | intervals.icu → Settings → Connections → your device → enable **Upload planned workouts**. |
| Activities have no power or HR | They came from Strava, which intervals.icu can't share. Connect your head unit directly in intervals.icu → Connections. |
| `python3: command not found` | `bin/icu days` and `bin/import-data` need it. macOS: `xcode-select --install`. Ubuntu/WSL: `sudo apt install python3`. |

The coaching here comes from Coach AMA. Train well.
