# Athlete Playbook — Running (v1)

## 0. How to use this file

- Operational playbook. The science lives in `coaching-reference-running.md` — this is the **what-to-do** when a conversation turns to profiling a runner, reading a run, testing, or race demands. Consult it the moment any of those come up.
- Every target is **×threshold pace (T)** or **%LTHR** or an **RPE/feel** anchor. Convert to real min/km with THIS athlete's current anchors (`read_athlete_profile`, `read_pace_model`); rebase on retest.
- ⚠️ **`create_workout` pace fields are the INVERSE convention:** `paceLow`/`paceHigh` = fractions of threshold **SPEED** (>1 = faster). Convert ×T time multiples as **fraction = 1 ÷ multiple** (both columns in the §1 zone table). Never paste a ×T multiple into `paceLow` — it inverts the session.
- Numbers here are evidence-based **starting points to test in training**, not laws. Weak/emerging/contested evidence is flagged inline — don't upgrade it to certainty when you talk to the athlete.
- **You are a training-data analyst, not a clinician.** Scope-of-practice (reference §10) governs everything: never diagnose, prescribe meds, or treat — refer out. Bone-stress and RED-S are the running-specific escalation traps.
- **ANCHOR VOCABULARY (read first, load-bearing).** Store **one** anchor: **Threshold Pace (T)** ≈ ~60-min race effort ≈ LT2. It is the runner's "FTP." **T is NOT Critical Speed.** CS ≈ 30-min effort, ~4–6% faster; intervals.icu's auto-fitted CS is a *monitoring signal only*. Because every workout pace multiplies the anchor, a CS number dropped into a T slot corrupts every session. Never mix them.

## 1. Reading the runner — profile the pace-duration curve

Run a full assessment at onboarding, after every test block, and whenever data and self-report disagree. Output = a dated "Strengths & weaknesses" verdict in `USER.md` (template in §3).

### The curve (`read_pace_model`)

Running's power-duration curve is the **pace-duration (speed-duration) curve**. `read_pace_model` returns the fitted **Critical Speed (CS)**, **D′** (the curvature — running's W′ analogue, in **metres** of anaerobic distance reserve) and best-pace-per-duration. Read it the way you'd read a cyclist's MMP curve: as **best pace at benchmark durations**, reported so weaknesses show. **Its shortest bench is 60 s** — there is no sub-minute point, so sprint speed / speed reserve comes from observed strides or asking the athlete, never from a 200 m number you don't have.

| Dur (≈dist) | System | Read |
|---|---|---|
| **~1 min** (400 m) | Anaerobic capacity → **D′** | phenotype |
| **~4–6 min** (1500 m/mile) | VO2max / max aerobic speed (**vVO2max ≈ I pace**) | aerobic ceiling |
| **~30–60 min** (10k–HM) | Threshold → **CS / T anchor** | aerobic anchor |
| sprint (no bench) | Neuromuscular / speed reserve | from strides/athlete report — tool has no <60 s point |

- **CS = the asymptote** of the curve (aerobic anchor); **D′ = the curvature** (anaerobic reserve). High D′ / steep short end = speed-anaerobic phenotype; flat curve with small D′ = endurance/diesel. *Jones & Vanhatalo 2017; Vanhatalo 2011 (strong).*
- **The curve underestimates**, like MMP — it's built from real runs where the athlete rarely went truly maximal at every duration. Flag any benchmark with no recent near-max effort and **prescribe a test** before calling it a ceiling. *(moderate).*

### Phenotype by SHAPE — read the slope, not one pace

- **Riegel fatigue exponent** is the cleanest shape read: fit two race performances to `T₂ = T₁·(D₂/D₁)^k`. **k ≈ 1.04–1.06 = strong endurance/diesel** (holds pace as distance grows) · **k ≳ 1.08–1.10 = speed phenotype / endurance-limited** (fades badly at distance). *Riegel 1981 (moderate — population fit; individualize).*
- **Speed reserve (ASR):** gap between max sprint speed and vVO2max. A large reserve means VO2max reps sit at a *lower* fraction of the athlete's top speed → they tolerate I-pace better and want more speed-endurance; a small reserve → protect them, bias I conservative. *Sandford 2019; Bundle 2003 (emerging).*
- **Localize by the curve's weak band:** weak 200 m–400 m with strong 30-min = **diesel, no top gear** (5k/10k limiter is speed) · strong short end but marathon far slower than 5k predicts = **speed phenotype, poor durability/aerobic base** (the marathon limiter). **Changes <~2% = noise** — don't coach on smaller deltas.

### What "good" looks like — VDOT tiering

VDOT (a performance-derived pseudo-VO2max, Daniels–Gilbert) is the running analogue of the W/kg profile table. Tier by VDOT; derive exact paces from the VDOT curve in code (times below are men's-club reference points).

| Tier | VDOT | 5k | 10k | T pace /km |
|---|---|---|---|---|
| Exceptional | ~70 | 14:55 | 30:59 | ~3:14 |
| Excellent | ~62 | 16:35 | 34:23 | ~3:33 |
| Very good | ~55 | 18:22 | 38:06 | ~3:57 |
| **Good (strong club)** | **~50** | **19:57** | **41:21** | **~4:15** |
| Moderate | ~44 | 22:15 | 46:09 | ~4:45 |
| Fair | ~38 | 25:12 | 52:17 | ~5:20 |

- **VDOT is sex-neutral as an index** (same race time → same VDOT), but the *times* above are a men's-club reference. Tier a woman by her own competitive context, not against a man's absolute paces; the **phenotype-shape reading above is sex-neutral**. *Daniels 2014 (applied compilation, not peer-reviewed norms — use for tiering + shape, anchor competitive runners to actual results).*
- A runner near a tier boundary swings tiers on a stale or soft test — verify the anchoring race/test is genuine, flat, and recent before any phenotype claim.
- **Never present these as targets** — a tier is a readout, not a goal (weight/self-worth risk, same as W/kg).

### Durability — a separate axis, never inferred from fresh pace

- Running durability = **late-run decay in pace-at-effort / economy** (the marathon "wall" in miniature). Operationalize: compare **GAP at matched HR/RPE in the final third vs the first third** of a long/steady run, or pace at a fixed HR fresh vs after ~90–120 min. Large fade = durability limiter → long runs, medium-long runs, late-run quality, and **fueling rehearsal** (fade is often under-fueling, not fitness). *Maunder 2021; Coyle (emerging — trigger to investigate, not pass/fail).*
- Fresh 5k/10k fitness says nothing about durability. A marathoner with a great 10k but a fading long run is durability/fuel-limited, not speed-limited.

### The anchors — how they relate

- **T pace (the anchor)** ≈ 60-min race pace ≈ LT2/MLSS ≈ **95–99% LTHR** ≈ ~88–92% HRmax ≈ ~83–88% VO2max.
- **CS** ≈ 30-min race pace, **~4–6% faster** than T. Convert in **pace units (time/km, where slower = larger):** `T-pace ≈ CS-pace ÷ ~0.95`. Train *around* CS, never *at* it (it's a boundary). *Jones 2010 (strong).*
- **LTHR** is the HR anchor — from a test, never an age formula. **vVO2max ≈ I pace** (~3000 m–5k pace).
- Five training paces flow from the single T anchor (Daniels **E / M / T / I / R**), computed from the VDOT curve in code (multipliers below are a template — offsets **compress at higher fitness**):

| Zone | Pace ×T (time/km) | `create_workout` paceLow–paceHigh | %LTHR | Spoken feel | HR valid? |
|---|---|---|---|---|---|
| **E** Easy/Long | 1.22–1.40 | 0.71–0.82 | <85% | full sentences, nose-breathable | yes |
| **M** Marathon | 1.06–1.10 | 0.91–0.94 | 85–91% | comfortable-hard, short sentences | yes |
| **T** Threshold (anchor) | 0.98–1.02 | 0.98–1.02 | 95–99% | "comfortably hard," 3–4 words | yes |
| **I** VO2max | 0.93–0.96 | 1.04–1.08 | ~100% pinned | hard, ~1 word, 3–5 min repeatable | **weak — pace leads** |
| **R** Rep/Speed | 0.86–0.91 | 1.10–1.16 | n/a | fast but relaxed, controlled form | **no — pace/effort only** |

- **The ×T column is time/km (>1 = slower) for talking paces; the `create_workout` column is the speed fraction (= 1 ÷ ×T, >1 = faster) for `paceLow`/`paceHigh`.** Don't mix them.

- **HR is invalid below ~2 min of work** (strides, R, short I) — cue by pace/effort, never HR. **Bias novices ~1–2% slower at T and I**, and shade conservative whenever HR climbs above LTHR at the prescribed T pace. **Cap E on the slow-safe side** (talk test / <first threshold) to stop easy-day grey-zone drift — but never police easy pace on the fast side. *Daniels 2014; Seiler 2010 (strong for the easy-cap principle).*

## 2. Conversation assessment + limiters

### Ask the runner (data the files can't show)

Ask in chat, log to `USER.md`:
1. **Where does it fall apart?** (early speed / the last mile of a 5k / holding marathon pace after 30k / on hills / on descents) → localizes the limiter to a duration/terrain band.
2. **What feels easy vs hard?** (cruising tempo vs top-end reps) → cross-checks phenotype.
3. **Terrain / surface you race and train on?** (track / road / trail / hilly).
4. **When do the legs go in a long run** — and did you fuel it? → durability vs fueling.
5. **Any recurring niggles** (shin, knee, Achilles, foot), and **how's sleep and fueling?** → the bone-stress/RED-S screen runs continuously, the way the coach asks RPE for power-less rides.
Plus **sRPE** (0–10, ~30 min post-run) — quantifies internal load where pace can't.

### Data ≠ self-report — reconcile before prescribing

- Fast 5k but marathon collapses / "legs gone at 30k" → **durability + fueling gap**, invisible to fresh tests; confirm with a long-run decoupling check and a fueling history, not another VO2max block.
- "Strong on the flat, shelled on hills" → strength/economy or pacing on gradient — read GAP, not raw pace.
- Anchor/test **>~6–8 weeks old** loses validity → retest before concluding.

### Limiters — taxonomy → diagnostic

- **Aerobic base / durability** = long + late-run decay · **threshold/LT2** = 20–60 min sustained · **VO2max** = 3–5 min · **speed/economy** = R-pace + strides · **repeatability** = decay across interval reps.
- A limiter is an **event-specific** weakness. A weakness the target race never taxes (top-end speed for a marathoner) is not a limiter and must not drive the block.
- **Target 1–2 limiters per block; maintain — don't grow — strengths.** Fix base/durability/economy first in developing runners; add top-end sharpening late.

## 3. Test battery

Schedule each as a structured workout with warmup/cooldown bookends. **Ask conditions each test** (surface, weather, treadmill vs road) and record them on the result — pace read on a hot day or a trail is not a fitness drop. Most runners have **no running power**; pace + GAP + HR + RPE is the full instrument.

**Choosing the test (best fit for THIS athlete):**
1. **Need one at all?** If a genuine hard 5k/10k landed in the last ~4–6 weeks, harvest it → VDOT; don't test.
2. **Else pick:** **5k/10k race → VDOT** is the default (prefer 10k, more aerobically robust) · **30-min solo TT** for non-racers/beginners (also gives LTHR) · **CS multi-effort** for data-driven track/GPS athletes · **3-min all-out (3MT)** only for the fit and injury-resistant.
3. **Do NOT** use Conconi/HR-deflection (discredited in running). Lab lactate (MLSS/LT) is an authoritative manual override if the athlete has it.
4. Keep the **SAME protocol** across retests (switching breaks the trend); store the anchored protocol + its provenance in `USER.md`.

| Test | Who | Protocol | Compute the anchor |
|---|---|---|---|
| **5k/10k race → VDOT** (default) | anyone who'll race | genuine hard flat effort, last ~4–6 wk; prefer 10k | Daniels–Gilbert → VDOT → E/M/T/I/R; **T ≈ current ~60-min race pace**. Never derive from mile/1500 (over-rates anaerobic) or marathon |
| **30-min solo TT** | non-racers, beginners | solo, flat, honest; **lap at 10:00** | **LTHR = avg HR of final 20 min**; **T pace = last-20-min pace** (raw 30-min avg is a touch fast — shade slower). Solo under-reads vs a real race ~2–6% |
| **CS multi-effort** | data-driven, track/GPS | 3 max efforts, different durations (e.g. **1200/2400/3600 m**), fully recovered; or harvest 3 genuine races | `dist = CS·t + D′` → CS (slope), D′ (intercept); **T ≈ CS-pace ÷ ~0.95** |
| **3-min all-out (3MT)** | fit, injury-resistant only | big warm-up, all-out **180 s** | CS = mean speed of **final 30 s**; **reject if final-30-s pace is still climbing** (sandbagged start) |

**Retest cadence:** calibration checkpoint at the **start + end of each 4–8 week block**, plus opportunistically off any race PR. **A flat or declining retest is a fatigue/overreach flag FIRST, a pace cut second** — investigate (sleep, load ramp, fueling) before re-cutting paces. Don't over-test; each max effort is a hard session. *Daniels 2014; Jones 2017 (strong).*

### How intervals.icu models running fitness (know what you're reading)

- **Pace domain, not watts.** The Pace tab builds a **best-pace-per-duration curve** and fits a **Critical Speed** — the running eFTP analogue — auto-estimated and continuously re-adapting from best efforts across *all* runs (a hot parkrun moves it). GAP (grade-adjusted pace) normalizes hilly runs so the curve and load aren't wrecked by terrain.
- **`threshold_pace` is NOT auto-calculated.** Unlike the opt-in power eFTP, intervals.icu does **not** auto-set a running threshold pace. **The coach owns the anchor:** compute it from a field test and **write it back with `write_pace_settings`** (takes sec/km + optional LTHR) under SETTINGS:WRITE, **suggest-don't-force** — propose the new `threshold_pace` + `lthr` after a test, require athlete/owner confirm (mirrors the FTP/W′ accept-and-write flow). **The write applies going forward only — you have no recompute tool for history**; judge past runs against the anchor live at the time, and never claim history was re-zoned. There is **no writable `critical_speed` field** — CS is read-only. If the write path returns a reconnect error, the athlete hasn't granted settings-write; tell them, and never claim you changed intervals when the tool didn't write.
- **Anchor strategy — pick one per athlete, don't let them fight:** (a) Pace Preference = **CS** → zones auto-adapt, zero writes, but inherit curve noise; (b) Pace Preference = **Threshold Pace** → coach owns it, writes it back. **Default (b)** for a pace-owning coach. Store which test produced the anchor + when, so you can explain paces and refuse to over-claim.

### Write the verdict into `USER.md`

```
## Strengths & weaknesses
- Curve (60d): 400m 1:12 · 1500m 5:02 · CS 3:58/km · T 4:11/km (from 10k 41:20 → VDOT 50)
- Riegel k across 5k→HM = 1.09 ⇒ speed phenotype, endurance-limited
- Durability: long-run final-third GAP +14 s/km at matched HR = fade (fuel? base?) — protocol: 2h steady
- Athlete says: dies in last 6k of the half — agrees with data
- Limiters for [half]: (1) durability/threshold endurance (2) fueling · Strength: 5k speed — maintain
- Anchors: T 4:11/km + LTHR 168 (30-min TT, road, [date]); CS monitor only
- Retests due: 10k or TT wk of [date]; keep protocol = road 10k
```

State it plainly to the athlete — one strength, the 1–2 limiters, and what the next block does about them.

## 4. Reading a run by type (`read_activity` / `read_effort_analysis` first)

**GAP is the first screen, not raw pace.** Compute/read GAP for any run with elevation before judging it. Then judge against what the run *type* should look like:

| Type | Well-executed looks like | Common failure |
|---|---|---|
| **Easy / recovery** | GAP in E band, HR <85% LTHR, decoupling <5%, RPE 2–4, conversational | HR/RPE creeping into M–T = **grey-zone drift** (the #1 amateur error: easy days too hard) |
| **Long run** | E-body, controlled; watch **final-third GAP + decoupling** | fade + HR drift late = under-fueled, over-paced, or base/durability gap — ask which |
| **Tempo / threshold (T)** | GAP within **±2%** of T pace, even splits, HR 95–99% LTHR | went out at I/CS pace then faded (classic); HR above LTHR at T pace = anchor too fast or fatigue |
| **Intervals (I / VO2)** | judge **per rep**: pace within ~±2–3% of I target, no downward fade across reps | over-paced start → late reps drop; reps cut short / count reduced = fatigue. **Don't trust HR on <2 min reps — it lags** |
| **Reps / speed (R)** | crisp pace, clean form, full recovery, no fade | ran them too long/fast (turned R into I); ignore HR entirely |
| **Race** | even or slight **negative split**; GAP holds | **positive split** late = over-paced start; GAP fade + HR drift = fitness or fueling |

- **Aerobic decoupling (Pa:HR)** — the run analogue of Pw:HR, on **steady, flat, temperate** runs only: first-half vs second-half pace:HR efficiency drift. **<5% = base coping (green to progress)** · **>10% = build more base** (or rule out heat/dehydration/under-fueling/fatigue first). Always pair the number with conditions — heat inflates decoupling with no fitness change. *Friel; TrainingPeaks (5% is a practitioner heuristic, not a precise cut-off).*
- **Interval execution — review per rep, not session average:** flag any rep >3% under target, a downward fade where late reps drop vs the first, or a cut-short set. Report which reps failed and whether pacing or fatigue.

### When pace lies — the pace → HR → RPE hierarchy

Not a two-tier switch; a terrain-and-duration-aware hierarchy. **Every prescription names a primary control + a named fallback** (e.g. *"tempo 4:20/km GAP; if trail or >22 °C, hold threshold HR / RPE 7"*).

- **Steep/technical/long descents →** RPE/HR. **GAP over-optimistic past ~−8% grade — never set downhill pace off GAP.**
- **Trail / GPS-poor / treadmill →** HR (steady) / RPE (hard); raw pace unreliable.
- **Heat >~15 °C / altitude >~1500 m / wind →** drop pace targets, coach by effort (slower runners lose ~4× the pace per °C that fast runners do; headwind costs more than a tailwind returns).
- **Elevation has no universal seconds-per-vertical-metre conversion.** Total gain alone cannot price a route: grade distribution, surface, runnable descents, weather and the runner determine the cost. Use recorded GAP, the sampled profile and this runner's comparable courses; otherwise give a clearly uncertain range, never “3–5 seconds × each vertical metre.”
- **Short intervals (≤3 min), strides, R →** pace or RPE, **never HR** (HR lags 15–60 s and under-reads the rep).
- **Long run / marathon →** HR for the first 30–45 min, then RPE; **expect 10–20 bpm cardiac drift — don't chase it by slowing indefinitely.**
- **Require an individually tested LTHR — never 220−age** (±10–12 bpm error).
- **Treat disagreement as data:** high RPE + low HR = fatigue/under-recovery flag; low RPE + high HR = heat/dehydration/drift flag. Late in long/hot efforts, trust RPE + GAP over a drifting HR (directional evidence — flag as debated, not law).

### Data hygiene — confirm before judging

Common confounders: trail logged like a road run (GAP wild), treadmill pace uncalibrated, a hot/humid day read as a fitness drop, a hilly "easy" run with high HR that was actually honest for the terrain. **When GAP, HR, surface, weather, or a stale anchor conflict with the label — ask the runner what the run actually was BEFORE judging execution.** Misreading a hot trail run as a weak effort is the most common analysis error.

## 5. Race demands by event — train the decisive effort

| Event | Duration | Center of gravity | Race pace ≈ | Key sessions resemble |
|---|---|---|---|---|
| **5k** | ~14–25 min | VO2max / speed | I / CS pace, ~95–100% VO2max | 5–6×1 km at goal pace, 4–5×3–5 min I, CV cruise, R for economy |
| **10k** | ~30–50 min | threshold ↔ VO2max | ~CS (T+), ~90–95% VO2max | cruise intervals, longer I reps, 3×2 mile at T, 6×1 km |
| **Half** | ~1–2 h | threshold + endurance | ~T (M–T for most amateurs) | long T runs, cruise intervals, M-pace long runs, progressions |
| **Marathon** | ~2.5–5 h | marathon-pace endurance + **durability + fueling** | M (1.06–1.10×T), ~75–84% VO2max | long runs with MP blocks (2×8–10 km at MP), medium-long runs, T to lift the ceiling, **fuel rehearsal** |
| **Trail / ultra** | 2 h–all day | aerobic + eccentric/downhill durability + power-hiking + **fueling** | **effort-capped, not pace** | long back-to-backs, vert/hill reps, downhill eccentric conditioning, power-hike practice, race-nutrition rehearsal |

- **5k–10k peaks tilt to VO2max/CV;** make the key session look like the race late in the build (5–6×1 km at goal 5k pace).
- **HM–marathon peaks stay threshold/MP-weighted** (more pyramidal, not more polarized). The marathon is won on **durability + fueling**, not top-end — a great 10k with a fading long run means the marathon block is durability/fuel work, not VO2max.
- **Trail/ultra:** judge and prescribe by **effort/HR/RPE/time-on-feet/vert**, never pace (GAP unreliable on steep/technical). Downhill eccentric resilience and power-hiking are trainable, race-decisive skills.
- **Pacing:** even to slight negative split for 5k–HM; **never start above race pace** (the classic blowup is 5k pace for the first km then fade). Marathon = disciplined MP + fueling from the gun. Ultra = a hard **effort cap**, first hours should feel too easy; finish is decided by fueling and hiking economy. *Daniels 2014; marathon pacing literature (strong).*

## 5b. Technique & skills — trainable, prescribable

Running technique is trainable the way handling is on the bike, and it belongs on the plan — not just in a description. Same backbone: isolate slow → add speed → vary → add fatigue; cue the *effect* ("run tall, quiet feet", "float the downhill"), not body parts; drill on fresh legs, then rehearse under fatigue. *Motor-learning literature (moderate); running-specific technique evidence is thin/practitioner-consensus.*

**Reactive, not nagging:** program technique/skills where the runner's events clearly need it (a trail runner losing time and getting hurt on descents), but don't push form or cadence tweaks on road runners who don't need them. Give real specifics when asked; don't nag.

- **Worth prescribing:** **downhill running** (eccentric control, quick light steps, lean with the slope, eyes ahead — trail-decisive and injury-protective; condition it progressively); **technical trail** (foot placement, cadence over rocks/roots, power-hiking the steep pitches — often faster than running); **form drills** (strides, hill sprints, A-skips) placed fresh for turnover/mechanics; **cadence** — a ~5% bump only for a specific reason (recurrent shin/knee issues, clear overstriding), never a universal 180 target (see §6); **start/positioning** for road races.
- **The remote-coach boundary:** prescribe the drills, cues and progressions, and review the runner's **video** async. Refer to an in-person gait/technique coach for an ingrained fault the runner can't self-perceive or first-time skill acquisition; **gait retraining for a running injury is a physio/specialist call** (reference §10 scope). You coach the practice, not a hands-on gait clinic.

## 6. Myths to avoid (don't let these into the coaching)

1. **"80/20 polarized is proven-best."** No — **~80% easy is the robust floor** (shared by pyramidal too); the split of the hard 20% is small, contested, phase/individual-dependent. Sell "keep most running truly easy" with confidence; frame polarized-vs-pyramidal as a tunable. Pyramidal is evidence-equal and often better for base and marathon. *Seiler 2010; Casado 2022; Filipas 2022 (contested).*
2. **"Easy volume is the causal master variable."** It's a proxy for durability/training-age. Grow mostly-easy volume first only for genuinely under-volumed, durable, time-rich athletes; otherwise the **intensity split** is the better lever. Don't sell volume as a guaranteed differentiator.
3. **"The 10%/week rule prevents injury."** Debunked (failed its RCT). Use ~5–10%/wk only as a gentle beginner ceiling; the real guardrail is the **single-session spike** (gate every run against the longest run in the trailing 30 days) + hard-day spacing + deloads. *Buist 2008; Nielsen 2014 (strong debunk).*
4. **"ACWR tells you injury risk."** Statistically discredited (mathematical coupling, arbitrary windows) — a trend signal at most, never a red/green gate. *Impellizzeri 2020 (strong critique).*
5. **"Daniels' volume caps are injury guardrails."** They're **quality-dose** limits (keep reps productive) — keep and relabel them, and layer the real load-safety rules on top.
6. **"Critical Speed = threshold = 1-hour pace."** No — CS ≈ 30-min pace, ~4–6% faster than T. Never feed a CS number into a T slot; convert or relabel.
7. **"30-30s maximize time at VO2max."** True in *cycling*, not running — **long 3–5 min reps win for runners** (more time above ~90% VO2max). Default I to long reps; keep 30-30 only as an option. Don't import cycling's short-interval superiority.
8. **"Run TSS = bike TSS."** A modeling convenience — running's eccentric/impact cost per metabolic unit is far higher. Model run load on a **musculoskeletal-stress axis** (RPE-minutes + distance + time-on-feet, up-weighted for long runs and downhills), not pure TSS.
9. **"MAF (180−age) is your aerobic threshold."** Unvalidated per-individual — a conservative easy-run HR ceiling for beginners only, never the master anchor. Prefer a measured LTHR.
10. **"Chase 180 spm cadence."** No universal target; running well above preferred cadence hurts economy. Cue a **~5% bump only for a specific reason** (recurrent shin/knee issues, clear overstriding <~165 spm), gradually, at the same effort. *Heiderscheit 2011 (moderate, symptom-specific).*
11. **"Soft surfaces / strength work prevent injury."** Weak/inconclusive on injury prevention — the leg self-adjusts stiffness. **Sell strength/plyo honestly for economy (2–6%) and durability**, not injury-proofing; and ramp any abrupt surface/terrain change (road→trail, flat→hills, track) as its own gated progression. *Blagrove 2018 (economy: moderate; injury-prevention: contested).*

## 7. Ergogenic aids — evidence-tiered + when/how to suggest

Food-first; batch-tested only (Informed Sport / NSF Certified for Sport). These
apply to runners exactly as to cyclists; the doses are per-kg and discipline-neutral.

**Fundamentals before marginal gains.** Sleep, daily fuelling, session-matched
carbs, consistency and training structure are the 90%. An ergogenic aid is the last
1–2% — never introduce one to a runner whose basics aren't dialed.

| Tier | Aid | Dose | Timing | Best for | Evidence |
|---|---|---|---|---|---|
| **1 — established** | **Caffeine** | **1–3 mg/kg is often enough; ~3 mg/kg is reliable.** 3–6 mg/kg is traditional, but more is rarely better | ~60min pre; **gum ~5–10min** for a late top-up | endurance ~+2–3%, 5k–marathon, the final kick | STRONG *(Guest 2021; dose NMA 2025)* |
| **2 — moderate / event-specific** | **Sodium bicarbonate** | 0.2–0.3 g/kg | **time to the runner's own [HCO₃⁻] peak, 30–180min** | 1–10min hard efforts: 800m–3k track, hard 5k/10k surges, XC, the final-lap kick | MODERATE, trained>recreational *(Aguiar/de Oliveira 2022)* |
| | **Beta-alanine** | 3.2–6.4 g/day, split into ≤2g doses with meals | **daily loading over weeks — NOT a pre-workout** (carnosine builds ~2–12wk; cumulative dose drives it) | 800m–3k, hard 5k/10k surges, the finishing kick; **not <60s or steady/marathon pace** | STRONG but modest (~2–3%), smaller in trained *(Trexler/ISSN 2015; Hobson 2012)* |
| | **Creatine mono** | 3–5 g/day (optional 20g load ×5–7d) | daily | repeated sprints, strength/power | STRONG — **+1–2 kg water** (matters uphill/at distance) *(Kreider 2017)* |
| **3 — situational** | **Beetroot / nitrate** | **6–8 mmol (~350–500mg nitrate)** | 2.5–3h acute, or multi-day loading | **diminished in highly trained runners (ceiling)** — value at altitude/hypoxia + short high-intensity; distance TT/VO2max ~null. ~500mg is the upper end of the standard range, not “well above”; >10–12mmol has not reliably added benefit | MODERATE/CONTESTED *(AIS nitrate guidance; nitrate umbrella review 2025)*. **No antibacterial mouthwash** |
| | **Vitamin D** | 1,000–2,000 IU/day Oct–Mar (59°N) | daily | correcting a deficit | **test 25(OH)D first**, physician-guided *(Owens 2018)* |
| | **Iron** | **only if tested deficient** | medical | true deficiency (runners are higher-risk — foot-strike haemolysis) | ferritin <30–50 µg/L; **dosing is medical — refer** *(Sim 2019)* |
| **4 — emerging / thin** | **Nomio (broccoli-sprout ITC)** | 1 shot (fixed) — **U-shaped, don't double** | ~3h pre key sessions/races, 1–4×/wk | modest submaximal/threshold lactate shift; NOT sprint/VO2max | EMERGING, thin & mostly in-house *(Flockhart 2023 n=9)*. WADA-legal, mild GI, premium. Food-first = broccoli sprouts. **Don't proactively suggest; not for under-18s** |

- **Bicarbonate — usable, not miserable:** GI distress is the limiter. Take **with a carb-rich meal (~1.5 g/kg CHO)**, split the dose over 30–60min, use enteric-coated, or **serial-load 0.2 g/kg/day for 3–5 days** (less gut upset). **Maurten Bicarb System** (hydrogel) cuts GI distress and gives a faster/higher peak, but hasn't been shown to out-*perform* plain NaHCO₃; you're buying tolerability. Additive with **beta-alanine**. **Never debut on race day — trial 2–3× in training.**
- **Beta-alanine — a loading supplement, not a pre-workout:** it raises muscle carnosine (an *intracellular* buffer, complementing bicarb's extracellular one) over **weeks** of daily dosing — felt ~2–4wk in, saturating ~10–12wk; a single dose before a session does nothing acutely, and a higher daily dose only saturates *faster*, not higher. The **tingle** (>~0.8g in one hit) is harmless and is **not** the effect — split into ≤0.8–1.6g doses or use sustained-release; no tingle ≠ not working. Carnosine decays slowly (half-life ~8–9wk), so no tight cycling. **Best stacked with bicarbonate** for a track/5k–10k race — start the load ~4–6wk out, add race-day bicarb.
- **Caffeine — the reliable one:** habituation only partly blunts it; a pre-race washout has no proven benefit. CYP1A2 genotyping is **not yet actionable**. Keep it **≥6h from bed**; even **100mg near bedtime can disrupt sleep**. For evening races weigh the gain against the sleep hit.
- **Performance dose ≠ safety limit.** For a **healthy adult**, EFSA's no-safety-concern references are up to **200mg in one dose from all sources** (including before exercise) and **400mg across the day**. They are not performance targets, and 400mg/day spread out does not make a **400mg bolus** harmless. Total coffee, gels, drinks, gum, tablets and pre-workout. Pregnancy, medication, cardiovascular symptoms/conditions, anxiety sensitivity or other medical context → ask/refer rather than saying “safe”, “harmless” or “not dangerous”.
- **Nomio, honestly:** broccoli-sprout sulforaphane → NRF2; a small submaximal lactate shift, but the "12% less lactate" headline isn't peer-reviewed and the studies are small and company-authored. WADA-legal, low-risk, but well behind the Tier-1 aids and not batch-certified. If asked: give exactly this read, mention the broccoli-sprout food alternative, don't push it.
- **Ketone esters:** for **race-day performance, skip them** — acute evidence is null-to-negative. Their real use is **post-session recovery/overreaching** in heavy blocks — see the recovery adjuncts below.

### Reading the products athletes actually use — map the label to the compound

You don't sell brands; you translate them. When a runner says "I use X," name the active compound(s), give the honest evidence read from the tiers above, and stay compound/food-first. Never tell them to buy a specific product.

**Product-review protocol:** If the athlete pasted a URL in the current message, call `read_web_page`. Get the current whole label (serving, full active panel, directions, warnings); the package wins if web copy differs. Convert serving amounts to compound doses and total the **whole stack/day**, especially caffeine, nitrate and beta-alanine. Separate acute benefit, loading-only ingredients, safety and marketing. Check weight, sleep, medication/conditions and prior tolerance. For tested athletes, verify the **current batch** in Informed Sport or NSF Certified for Sport — GMP or “third-party tested” is not anti-doping certification. Finish with one integrated use/omit plan, not isolated mini-verdicts.

**Ratio trap:** a BCAA ratio such as **2:1:1 is not glucose:fructose**, and total carbohydrate/sugars cannot reveal a carb-source ratio. State a glucose:fructose ratio only when the current full label explicitly identifies the carbohydrate sources or quantities.

- **Umara U Intend** (Swedish pre-workout many runners use): a current label lists **caffeine 250mg + beta-alanine 3g + citrulline malate 6g (3.6g L-citrulline) + arginine AKG 3g**, ~45min pre. Honest read: **the caffeine is the real acute ergogen** (~250mg ≈ 3–3.5 mg/kg for a 70–80kg runner — a solid dose). The **beta-alanine won't buffer THIS session** (it's a loading compound — the tingle just makes it *feel* active); citrulline malate is modest/emerging, arginine AKG weak. Treat it as a fixed-dose caffeine shot, total every caffeine source and keep it **≥6h from bed**. Recheck the package because formulas change.
- **Fairing M-46 PWO Shot (60ml):** current official page: **250mg caffeine** plus citrulline malate, arginine HCl, betaine, inositol and niacin; one current label gives **3g citrulline malate + 1.25g betaine + 1.25g arginine HCl**. Caffeine is the main acute ergogen. 250mg exceeds EFSA's 200mg single-dose no-concern reference, so don't stack it with capsules/Intend/coffee/gels. This is not the same product as M-46 powder.
- **Fairing M-46 powder:** current official serving: **10g with 300mg caffeine**, plus beta-alanine, creatine malate, alanine, tyrosine, beet powder, rhodiola and spinach. Treat it primarily as high caffeine; beta-alanine/creatine work only through adequate daily loading and unquantified beet/spinach is not a research nitrate dose. Never transfer this formula to the similarly named shot.
- **Fairing Endurox PWO Shot (60ml):** official headline doses: **beta-alanine 3g + caffeine 150mg**, with spinach/nitrate and acetyl-L-carnitine. One July 2026 package label stated **60mg nitrate per shot**. Honest read: caffeine may help; beta-alanine is loading-only; 60mg nitrate is far below the ~350–500mg acute protocol.
- **Fairing Nitrat capsules:** official direction is **3 capsules/day** from four nitrate sources; one July 2026 label stated **390mg nitrate per 3 capsules**. If the current package confirms it, that is inside the research range. No proven brand advantage; compare stated dose, timing, tolerance and batch certification, and don't stack another full-dose nitrate.
- **Fairing Koffein:** **200mg caffeine/capsule**. One capsule reaches EFSA's healthy-adult single-dose reference. Two = 400mg, which is the full-day reference when spread out — not a recommended pre-race bolus. Total every source and scale need to body mass, tolerance and sleep timing.
- **Beetroot / nitrate — the dose is what matters, not the brand.** A **standardized shot** can deliver the 6–8 mmol (~350–500mg) research dose: **Beet It Sport 400** (~400mg, the research standard), **Umara U Nitrate** (500mg / 8mmol), Unived Beet-420. Most beet **powders/capsules** don't state nitrate — measured content spans ~4–500mg, so "I use beet" ≠ a research dose. **Food-first** ≈ 500ml beetroot juice, or a big handful of rocket/spinach. Same caveats: **no antibacterial mouthwash**, don't spit, harmless red urine, and the trained-athlete ceiling is product-independent.
- **AIOSS-style greens/all-in-one products:** never classify one from a vitamin panel. AIOSS's maker page describes **46 active ingredients**, including ~5.9g botanicals, 2g fibre and probiotics; ingredient count is marketing, not performance evidence. Deficiency correction supports normal function but does not make the blend an endurance aid. Botanicals and probiotics are ingredient-/strain-/dose-specific; read the full label and medication context.
- **Concentrated green-tea extract:** calculate actual **EGCG** (extract mg × standardization). It is not an established endurance aid and concentrated extracts carry a liver-injury signal, especially fasted. EFSA could not identify a safe supplement dose and found concern at **≥800mg EGCG/day**; that is not proof every lower dose is safe. Liver disease, symptoms or interacting medication → refer.
- **General rule:** a multi-ingredient "pre-workout" earns almost all of its acute effect from **caffeine**; the buffering/NO amino acids bundled in (beta-alanine, citrulline, arginine) are either loading-only or weak. Judge the product on its caffeine dose + whatever compound has real evidence, not the label's ingredient count.

### Recovery, connective tissue & heat adjuncts (beyond the performance tiers)

Not race-day pace — these serve recovery, injury-resilience, and hot-race prep. Same gates: fundamentals first, trial in training, batch-tested.

- **Collagen + vitamin C — the one worth knowing for injury-prone / masters runners** (Achilles, shin/bone-stress, patellar tendon): ~15g collagen peptides (or gelatin) + vitamin C, **30–60min BEFORE** connective-tissue loading (plyo, heavy/slow lifts, hard running), then do the load — the pre-load timing floods low-blood-flow tendon/ligament/bone with substrate. Roughly doubles collagen-synthesis markers; tendon/bone outcomes emerging. It's an **adjunct to loading, not a substitute**, and NOT a muscle protein (low leucine — don't count it toward the daily protein target). Cheap, safe. *Shaw 2017; 2024–25 reviews (moderate/emerging).*
- **Glycerol hyperhydration — a heat adjunct (pairs with the coaching-reference heat section):** ~1.0–1.4 g/kg glycerol + ~25–30 ml/kg fluid + sodium over ~90–150min, finishing ~30–60min pre-start, to expand plasma volume and cut thermal strain in a long HOT race (hot marathon, trail-ultra). **WADA-legal since 2018.** It costs acute body-water weight and **must be rehearsed**. Complements heat acclimation, doesn't replace it. *(moderate).*
- **Sodium-preload source honesty:** the small acute sodium/hyperhydration study commonly associated with Sims delivered beverage portions over ~60 min beginning ~105 min before exercise. It does **not** establish a “take this the day before” protocol. Do not invent a later review or move an acute pre-exercise protocol to the previous day.
- **Ketones for recovery/overreaching (NOT race-day):** ~25g mono**ester** (not the harsher salts) post-session in a heavy mileage block / stage race / camp helped athletes tolerate ~15% more load and protected energy balance + sleep — the real reason some pro teams use it. Emerging, expensive, GI-harsh. *Poffé 2019 (moderate/emerging).*
- **Tart cherry & omega-3 — periodised recovery:** tart-cherry concentrate (~30ml ×2/day, ~4–7d around a target block) blunts soreness/inflammation and nudges sleep; omega-3 (~2–3g EPA+DHA/day, chronic) aids soreness and is a real health play — direct performance gains unproven. **Timing caveat:** use recovery-dampeners around competition/recovery weeks, **not** through hard adaptation blocks. *(recovery moderate).*
- **DON'T megadose antioxidants:** chronic high-dose **vitamin C (~1000mg) + vitamin E (~235mg/day in Paulsen 2014)** can attenuate some cellular/mitochondrial adaptation signals. Meet needs from food. **Do not extrapolate that trial directly to a lower-dose multivitamin** (for example 500mg C + 25mg E) or declare that it “blocks adaptation”; unnecessary and proven harmful are different claims. *Paulsen 2014 (strong for biomarkers at the studied doses; performance effect less clear).*

### The hype shelf — recognize it, stay honest

When a runner asks about the latest pro thing, give the honest read — **"the pros use it" ≠ "you should"** (most of this chases a fraction of a percent that only matters at the very top, and fundamentals dwarf it).

- **Lactate gels (ExoLactate):** hydrogel-delivered exogenous lactate (~15–25 g/h) sold as a "third fuel," trialled at the 2026 Tour de France. Real product, but the human evidence is one small ~4% pilot against several nulls — athletes mostly just report lower RPE. **Emerging, unproven — know it, don't recommend it.**
- **Continuous glucose monitors (Supersapiens / Levels):** **no evidence** they improve fuelling or performance in non-diabetic athletes, and they lag/misread during exercise — a behaviour-education toy, not a fuel gauge. Gently deflect.
- **NAD+ precursors (NMN/NR):** small human studies are mixed; an isolated amateur-runner signal plus later null trials is not a reliable endurance benefit. **Insufficient/mixed**, not “proven useless” and not a reason to recommend an expensive stack.
- **Note-only:** cluster dextrin / UCAN / Vitargo (no upgrade over a 2:1 glucose:fructose mix), menthol mouth-rinse (small, perception-only, for hot/dry races), probiotics (worth it only for illness-/gut-prone athletes; strain-specific).
- **Politely deflect (null/weak for endurance):** BCAAs, glutamine, arginine/citrulline "NO boosters", ZMA, adaptogens (ashwagandha/rhodiola), alkaline/hydrogen water — whole-food protein + the tiers above already cover the real levers. **Testosterone "boosters" — actively discourage:** no benefit AND a real contamination/anti-doping risk.

### When & how to suggest an ergogenic aid

This coach doesn't sell marginal gains. Raise an aid only when it's genuinely
decisive for *this* runner's *next* race — otherwise stay reactive and honest.

- **Gate 1 — fundamentals first.** If sleep, fuelling, consistency or structure aren't dialed, fix those; the aid comes last.
- **Gate 2 — event-triggered proactivity:**
  - **Caffeine** — race-day default for any goal race; confirm it suits the runner in training first.
  - **Bicarbonate** — proactively propose a *training trial* in the build when the goal race is decided by hard 1–10min efforts (track 800m–3k, 5k/10k, XC). Trial 2–3× in training, then lock a race-day plan. Never a race-day debut.
  - **Beta-alanine** — only worth starting when the goal race is punchy (track/5k–10k with hard 1–4min surges) AND it's **≥4–6wk out** (it needs the weeks-long load-in); pair it with race-day bicarb. Never a late or race-week add.
  - **Heat acclimation** — plan a 10–14 day block into the run-in to a known-hot goal race (coaching-reference §11), integrated with the taper. Not for a cool race.
  - **Nitrate** — only when it fits (altitude race, short high-intensity); otherwise, if asked, give the trained-runner-ceiling read honestly.
  - **Nomio / anything Tier-4** — reactive only. Honest read when asked, no push.
- **How to raise it:** one intervention at a time, tied to the runner's actual next race, in your normal voice — never a supplement-stack pitch. Frame it as an **experiment to trial in training** and log it in `LEARNINGS.md` as a hypothesis with a check date. Confirm it works for *this* runner before it's race kit.
- **Guardrails:** current-batch Informed Sport / NSF Certified for Sport only for any tested athlete (flag when a product isn't certified; GMP/“third-party tested” is not equivalent). **Under-18 → no supplement advice; defer to a parent/physician.** Medical dosing (iron, vitamin D) → test-and-refer. Scope (reference §10) still governs — you coach the engine and the fuelling, not medicine.
