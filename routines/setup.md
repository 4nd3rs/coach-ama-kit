# Setup (first run)

The athlete should get a working coach without touching a terminal. Do every
step you can yourself. Ask them only for what needs them: signing in to a
website, copying a key, approving a command. One step at a time, short
messages, plain words. Many athletes have never used a terminal, so never
tell them to type a command you can run yourself.

1. **Check the tools:** `python3 --version` and `curl --version`. If one is missing,
   help them install it:
   - macOS: run `xcode-select --install`, which brings `python3`, and they
     click Install.
   - Ubuntu or WSL: `sudo apt install python3 curl`.

   Then **check the connection:** `bin/icu check`.
   - `ok: connected … as <name>`: greet them by first name and go to step 2b.
   - `not set up` or `key rejected`: step 2.
   - `can't reach intervals.icu`: a network problem, not a key problem.
     - In Codex, the sandbox blocks network access by default. Re-run the
       command with network access, which Codex asks the athlete to approve.
     - If Codex can't do that, offer to add this to `~/.codex/config.toml`.
       That file is outside this folder, so ask first. Then tell them to
       restart Codex in this folder:
       ```toml
       [sandbox_workspace_write]
       network_access = true
       ```
     - In Claude Code, ask them to check their internet connection, then retry.

2. **The intervals.icu API key.** First ask whether they have an intervals.icu
   account. If not, have them sign up free at <https://intervals.icu>. Then
   connect their watch or training app under Settings → Connections (Garmin,
   Wahoo, Zwift, COROS, Polar, Suunto…). If their activities only reach
   intervals.icu through Strava, intervals.icu can't share the details; step 2c
   covers that.
   Then tell them:
   > Open intervals.icu/settings (sign in if asked), scroll down to
   > **Developer Settings**, click **Generate** next to API key, and copy it.

   Then let them choose how to hand it over:
   - **Paste it here** (easiest). Save it with
     `printf '%s\n' '<the key>' | bin/icu set-key` and nothing else. Never
     repeat the key back. Say once that it is now in this chat's history, and
     that they can regenerate it in intervals.icu at any time.
   - **Keep it out of the chat.** Create the file (`cp .env.example .env`
     if it's missing) and open it in their text editor:
     - macOS: `open -t .env`
     - Linux: `xdg-open .env`
     - WSL: `notepad.exe .env`

     They paste the key after `INTERVALS_API_KEY=`, save, and tell you.

   Never read, print or copy `.env` yourself. Run `bin/icu check` again until it
   says `ok`, then greet them by first name.

2b. **Check their history** (always, after a successful connection).
   Run `bin/icu activities <today−90d> <today>` and count the sessions. If it's empty or much thinner than they train, the
   history hasn't arrived yet. Some connections, Polar for example, only bring
   new activities until the athlete runs a separate history import. Tell them
   to look under intervals.icu → Settings → Connections → their device for an
   import option, or to upload old files. Coaching can start anyway: the first
   session asks about their training background instead.

2c. **Strava (optional, Claude Code).** Ask whether their activities reach
   intervals.icu through Strava, or notice it in 2b (activities with no power,
   HR or duration). If neither, skip this step.
   - **You already have Strava tools:** call the eligibility check. Eligible:
     tell them you'll read those sessions from Strava. Not eligible: the
     connector needs a paid Strava subscription (trials only count once they
     convert). Suggest connecting their device directly in intervals.icu →
     Settings → Connections instead.
   - **Claude Code, no Strava tools yet:** offer two ways.
     - If they use claude.ai: open claude.ai → **Customize → Connectors**, add
       **Strava** and click Connect. It shows up here the next time they start
       Claude Code, signed in with the same account.
     - Or, after asking, run
       `claude mcp add --transport http strava-mcp https://mcp.strava.com/mcp`
       (it adds Strava to Claude Code for this folder). Then they restart Claude
       Code in this folder, type `/mcp` and sign in to Strava.
   - **Codex:** the kit's Strava connector route is a Claude Code feature.
     Suggest connecting their device directly in intervals.icu instead.
   - Revoke any time in Strava → Settings → My Apps.

3. **Coach AMA data (only if it applies).** This kit started as the Coach AMA
   service, but most people using it never had a Coach AMA account.
   - If a `coach-ama-data*.zip` is in `~/Downloads`, ask whether to import
     it, then run `bin/import-data`.
   - Otherwise ask one short yes/no question: did they use Coach AMA?
     - **No:** go on to step 4. Don't mention it again.
     - **Yes:** while coach-ama.com is still up, they can sign in at
       <https://coach-ama.com/dashboard> and choose **Download your coaching
       data**, so the coach picks up where Coach AMA stopped. Then run
       `bin/import-data`. If the file is somewhere else, ask where and pass the
       path.
   - If they'd rather skip it, or the site is gone, that's fine: the first
     session rebuilds their profile.
   - After an import, tell them in a sentence what came in.

4. **Workouts on their device.** Ask whether they train with a Garmin, Wahoo,
   Zwift or similar. If so, tell them where to switch on sync: intervals.icu →
   Settings → Connections → their device → **Upload planned workouts**.

5. **How to come back.** Tell them, in two or three lines:
   - Claude Code: open this folder in the Claude app's Code tab, or run
     `cd <this folder> && claude`.
   - Codex: open this folder in the Codex app, or run `cd <this folder> && codex`.
   - Then say "morning", "debrief" or anything else.
   - Their coach's memory is the `athlete/` folder. Suggest keeping this folder
     somewhere that gets backed up.

   Use this folder's real path. If this session started in a different folder,
   say that next time they should start in this one, so the coach loads by itself.

6. **Hand over.** Ask whether they want to start now (about 10 minutes).
   - If they do, run `routines/first-session.md`.
   - With imported data, that routine starts at step 0: confirm the goal and
     availability, then check the next 10 days.
