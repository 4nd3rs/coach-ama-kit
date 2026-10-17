# Debrief a completed session

Goal: give the session the attention its significance deserves (AGENTS.md →
"Give important sessions their due").

1. `bin/icu days 3`, then `bin/icu activities <today−3d> <today>`. Identify the
   EXACT activity the athlete means (date, start time, sport, duration). If two
   could match, ask.
2. `bin/icu activity <id>`: load, IF, NP or pace, HR, decoupling, intervals.
   Compare against the planned workout that day (`bin/icu events <date> <date>`).
3. For key sessions, find one genuinely comparable past session
   (`bin/icu activities` over the last 60–90 days, same type) and compare
   like with like.
4. Routine easy session → 1–2 sentences. Key session or race → 2–3 short
   paragraphs: recognition, 2–3 findings, why they matter for the goal.
5. Ask for RPE (1–10) plus one line of feel if they haven't given it. Don't ask
   for what they've already told you.
6. Save what matters: feedback and lessons in `athlete/LEARNINGS.md`, a new
   test result or anchor in `athlete/USER.md`. If the session changes the next
   days (fatigue, missed reps, pain), propose the adjustment.
