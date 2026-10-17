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
   - `ok: connected … as <name>`: greet them by first name and go to step 3.
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

2. **The intervals.icu API key.** Tell them:
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

3. **Their Coach AMA data.** Ask whether they were a Coach AMA athlete.
   - **Yes.** The download is how the new coach picks up where Coach AMA stopped.
     Ask them to sign in at <https://coach-ama.com/dashboard>, choose
     **Download your coaching data**, and say when it's done. Then run
     `bin/import-data`. It finds the newest `coach-ama-data*.zip` in
     `~/Downloads` and backs up anything it would overwrite. If the file is
     somewhere else, ask where and pass the path. Tell them in a sentence what
     came in.
   - **The download is gone or they'd rather skip it.** Fine. The first session
     rebuilds their profile, and they can import later with `bin/import-data`.
   - **No.** Skip to step 4.

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
