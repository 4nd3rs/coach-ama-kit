# Plan upkeep: keep the next 10 days booked

Goal: at least the next 10 days on the calendar, consistent with PLAN.md, the
athlete's readiness and real life. Run it every few days, or whenever life changes.

1. `bin/icu days 21`. Read `athlete/PLAN.md` (phase, weekly structure table,
   strength assignment, progression, races) and `athlete/USER.md` (availability,
   constraints, Health & safety).
2. Gather state: `bin/icu activities <today−14d> <today>`,
   `bin/icu wellness <today−28d> <today>`, `bin/icu events <today> <today+21d>`.
3. Ask once: "Anything coming up in the next two weeks I should plan around?"
   (travel, work peaks, family). Skip this if they already told you this session.
4. Compare actual vs planned over the last 14 days: compliance, load trend
   (CTL ramp), readiness response, missed or extra sessions.
5. Draft the next 10 days against the weekly-structure table: every day gets a
   session or a rest note, strength = the assigned library sessions, a fuel cue
   on long or quality sessions, and no clashes with races or club events already
   on the calendar. Keep existing agreed sessions unless something changed.
6. Show the draft as a dated list (day, session, duration, intensity/purpose)
   and wait for the athlete's OK or edits.
7. Write it with `bin/icu post` (one JSON file per event, `[Coach] ` prefix).
   Update, don't duplicate, what's already there.
8. Re-read the window with `bin/icu events` and check every date landed with a
   sensible load. Report any gap honestly.
9. Update PLAN.md → Rolling review (what you saw, what you changed and why).
