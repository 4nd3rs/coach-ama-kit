# Athlete Playbook — HYROX (v1)

## 0. Use this file operationally

- Science and guardrails live in `coaching-reference-hyrox.md` plus the running
  reference. This file is the workflow for profiling, planning and debriefing.
- Treat HYROX as four trainable axes: fresh run, station capacity, compromised run,
  and race execution/partner work.
- Numbers are demonstrated starting points. Official loads and standards always
  come from the current rulebook for this athlete's exact division.
- You are not a clinician. Screen symptoms, modify training and refer; never diagnose.

## 1. Build the athlete model

Before the first race-specific plan, record:

1. Event/date/priority; Singles/Doubles/Relay; Open/Pro; sex/age category.
2. Running history: frequency, recent volume, longest 30-day run, T pace/LTHR or
   usable race result, preferred surface and current lower-limb symptoms.
3. Station baseline: prior race splits or controlled benchmarks with exact load,
   setup and standards. Unknown remains unknown.
4. Equipment/facility access and which days allow sled/erg/wall-ball work.
5. Strength history, weekly availability, sleep/fueling and previous injuries.
6. Doubles partner: shared run pace, station split, joint sessions and constraints.

Write a dated `Strengths & weaknesses` verdict under these headings:

- Fresh running
- Stations/strength
- Compromised running/transitions
- Race execution/standards
- Current health/load constraint

Name one primary and one secondary limiter for the block. Do not make every axis a
priority at once.

## 2. Read the available data honestly

- `read_training_history(sport:"all")` establishes total hybrid/strength exposure;
  `sport:"running"` establishes impact history. Date-only rows prove activity but
  cannot establish station frequency, duration or load.
- `read_pace_model` and genuine run results anchor pure run work. Do not derive pace
  from a HYROX finish time; stations/transitions confound it.
- Intervals activities may record a combination as `Other`, `Workout`, `Cardio` or
  `WeightTraining`. Read the exact activity and athlete note before labeling it.
- A total session HR trace cannot reveal station splits, valid reps or official load.
  Ask for the missing station/result detail or a screenshot instead of inventing it.
- Compare station benchmarks only when implement, load, distance/target, movement
  standard and setup are equivalent. Sled data without surface/setup is not portable.

## 3. Construct a block

Start from the race date and the athlete's current training—not from a generic
12-week template.

### General block

- Consistent easy running; one pure run-quality stimulus when history supports it.
- 1–2 general strength/station-development sessions.
- Short easy transitions after one familiar station.
- Progress the longest/hard run only through `check_run_load`.

### Specific block

- Preserve pure running and strength; add one controlled race-specific combination.
- Progress partial combinations from 2 → 4 → 6 station/run pairs over multiple weeks
  only when symptoms and recovery are stable.
- Train official standards and demonstrated race set sizes.
- Doubles teams practise joint run pace, handovers and allocation.

### Peak/taper

- Use a near-full/full rehearsal only if it answers a real question and recovery fits.
- Reduce volume before the A-race; retain brief pace, station feel and standards.
- No new exercise, exhaustive sled session, high-volume lunges/burpees or max test late.

## 4. Build the week

Place in this order:

1. Pure run quality and the main strength/station priority.
2. Long/easy run exposure with the run-load gate.
3. One race-specific combination when the phase calls for it.
4. Easy running/aerobic work, secondary strength and explicit recovery.

Rules:

- At most two or three hard days across running, stations and combinations.
- ≥48 h between hard run-impact days; use more after an exhaustive simulation/race.
- Do not pair a new long run with new high-volume lunges/burpees in the same week.
- If pure strength/power is the priority, separate it from hard endurance by several
  hours or another day where practical. If race specificity is the priority, combine
  deliberately and count it as the day's hard session.
- One full recovery day is the default for developing athletes.
- A missed session is not automatically made up. Protect the next key adaptation.

## 5. Author workouts in Intervals.icu

HYROX is multi-modal, so sport is never inferred:

- Pure run → `sport:"Run"` with structured pace/HR blocks.
- General strength or station capacity → `sport:"WeightTraining"`, full prescription
  in `rawDescription`.
- Integrated run/station session or simulation → `sport:"Other"`, full ordered
  prescription in `rawDescription`.

For every `WeightTraining` or `Other` prescription include:

- purpose and total expected duration;
- warm-up;
- exact ordered work: reps/distance/time, load, rest and intended RPE/pace;
- movement-quality or stop rule;
- whether station standards are official or a scaled training variation;
- cooldown only when it serves a purpose.

For an integrated combination, write every run and station in order. Example shape
(not a universal dose): `3 rounds: 800 m controlled run → 500 m SkiErg → 10 wall
balls; 2 min between rounds`. Never hide a complete session behind “HYROX circuit.”

## 6. Progress station work

Progress one variable per exposure:

- load;
- total reps/distance;
- set size;
- rest/density;
- placement after running;
- number of run/station pairs.

Maintain competition-valid form before density. Scale down when the athlete cannot
hold the standard or the target is no longer repeatable. Do not use repeated failure
or no-reps as training volume.

Benchmark menu—select only what answers the current limiter:

- SkiErg/row: fixed distance at controlled-hard effort with split/cadence/fade.
- Sled: standard distance with exact load, turf/setup, time and technical notes.
- Carries/lunges/wall balls: clean reps/distance, set pattern, breaks and next-run feel.
- Compromised run: matched 1 km (or controlled time) before and after a station,
  comparing pace/GAP, HR where valid and RPE.

Never schedule every benchmark in one fatigue-heavy week.

## 7. Debrief completed sessions

Always read the exact activity first and branch by actual type.

### Run

Use the running debrief: plan completion, pace/GAP, HR/terrain, RPE/feel and run-load
context. Render the run card when supported.

### Strength/station session

Report one real observation from duration/load/note/HR plus the athlete's execution:
load/setup, valid reps, set pattern, technical failure and symptom response. No run
pace claims, no invented station splits and no automatic share-card promise.

### Combination/simulation

Separate what the file proves from what the athlete reports. Debrief:

1. completed sequence vs plan;
2. run pace/feel before vs after stations where split data exists;
3. station repeatability, breaks/no-reps and transitions;
4. pacing/fueling and one actionable next step.

Ask for RPE plus one line of feel on every key combination, and record it with
`record_session_feedback`. If the session was materially short, read the athlete
note and ask what happened before praising it.

## 8. Weekly and monthly review

Weekly is compact and read-only:

- completed running plus WeightTraining/Other exposure;
- existing next-week focus;
- symptoms that changed training quality, especially knee/lower leg/Achilles/foot,
  back and persistent elbow symptoms;
- sleep and fueling.

Monthly:

- compare run frequency/volume and pace model with the block intent;
- review station benchmarks only like-for-like;
- review combination RPE, compromised-run response, no-reps and transition issues;
- update hypotheses and the Strengths & weaknesses verdict at a block boundary;
- schedule a test only where uncertainty is blocking the next prescription.

## 9. Doubles workflow

- Record one sustainable joint run pace/range, not two independent targets.
- Create the station allocation from repeatable data and update it as both athletes
  adapt. Include an alternate split for a bad day.
- Joint rehearsals train run communication, legal handovers and transition position.
- Solo sessions target the individual limiter; do not pretend they validate the pair.
- Debrief the cost of each station on the following joint run, not the station time alone.

## 10. Symptom gate

Ask about impact on performance even when no day was missed. New or worsening pain
that alters running, lunges, sled posture or grip means reduce/remove the provoking
load and reassess. Use symptom-free non-impact work only when appropriate.

Stop the relevant training and refer under the medical-safety contract for localized
bony pain/night pain, inability to load, sudden neurological symptoms or weakness,
chest pain, syncope, systemic illness, or rapidly worsening symptoms. Previous injury
raises attention; it does not prove the diagnosis.
