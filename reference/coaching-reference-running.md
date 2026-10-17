# Coaching Reference — Running Periodization (v1)

## 1. How to use this file

- Your running training-science cheat sheet. Consult before planning. **Defaults, not laws** — `USER.md` data and constraints override.
- **Prescribe by pace, anchored to Threshold Pace (T).** Every pace target here is a **multiplier on this athlete's CURRENT T-pace** (in time/km; >1 = slower than T). Convert with THIS runner's live anchor — `read_athlete_profile` / `read_pace_model` — never numbers remembered from another runner or a stale test; rebase on every retest.
- ⚠️ **`create_workout` pace fields use the INVERSE convention:** `paceLow`/`paceHigh` are fractions of threshold **SPEED** (>1 = FASTER). Convert every ×T multiple as **fraction = 1 ÷ multiple** — the §4 table carries both columns. Feeding a ×T time multiple straight into `paceLow` inverts the workout's intensity (E 1.22–1.40 would export as a near-max effort).
- **HR (%LTHR) and RPE are fallbacks**, in that order, for terrain/conditions where pace lies (§7). HR lags 15–60 s and is **invalid below ~2 min of work**. Get an RPE (1–10) + one line of feel after key sessions; high RPE at normal pace = fatigue flag even when readiness looks fine.
- **Never conflate Threshold Pace with Critical Speed.** T ≈ ~60-min race effort (LT2). CS ≈ 30-min effort, **~4–6% faster**. Every workout multiplies the anchor, so a CS-in-a-T-slot error propagates into every session. intervals.icu's auto-fitted running CS is a **monitoring signal only**, never the anchor. Convert: **T ≈ CS ÷ ~0.95**.
- Well-established parts (~80% easy floor, the session-spike governor, taper mechanics) are stated with confidence. Contested levers are flagged in-line ("contested/individualize") — don't upgrade those to certainty when you talk to the athlete.
- Running load is **musculoskeletal, not just metabolic** — impact + eccentric loading every stride. Do **not** reuse cycling TSS² math; score runs on a stress axis (§5) and gate them (§5).

## Running intake

Applies when the athlete's primary discipline is running, and overrides the
sport-specific questions of SOUL's cycling-default Phase 1 (road/gravel/MTB,
FTP, trainer, power meter, which bikes). For triathlon or HYROX athletes their
own reference's intake governs; use this only for the run details it asks for.
The signup already says running — do not ask which sport they do. Age, sex,
goal, days/hours, the safety screen and medications still come from SOUL. Read
what intervals.icu already shows first, then one natural question at a time:

1. **Volume and the longest run.** Runs per week, weekly km or time over the
   last 4–8 weeks, and the longest single run in the last 30 days — that
   longest run is the baseline for the §5 session-spike governor. A returning
   or low-mileage runner ramps from what they run now, not from a past peak.
2. **A recent race result** — distance, time, date, course (flat/hilly,
   road/trail). A genuine 5k–10k from the last ~4–6 weeks is the default
   threshold-pace anchor (§3); older, mile or marathon results are context,
   not the anchor. No race? Offer the 30-min TT later — never open with a test.
3. **Surfaces and terrain:** road, trail, track, treadmill, hills — what they
   run on now and what the goal race demands. Each surface change is its own
   gated ramp (§5); treadmill pace does not map 1:1 to outdoor pace.
4. **Weigh injury history heavier than for a cyclist.** Every stride is impact,
   and a previous running injury is the most consistent predictor of the next.
   Ask about the last 12 months and anything recurring — shin, calf/Achilles,
   knee, hip, plantar fascia/foot — and any bone-stress injury ever (plus the
   §5 RED-S co-factors). A current niggle sets the first week, not the goal
   date. Screen and refer; never diagnose.
5. **Watch, footpod or Stryd.** Which watch records their runs, whether pace
   comes from GPS, a footpod or Stryd, and whether HR is wrist or chest strap.
   Note GPS-poor routes (forest, tall buildings) and treadmill-only running —
   they decide whether pace or HR/RPE leads (§7). Stryd running power is
   optional context, never the anchor; never ask a runner about a power meter.
6. **Long-run fueling** — what they eat and drink on runs over ~75–90 min
   today and how their gut tolerates it. Under-fueling feeds the bone-stress
   profile; ask about fueling and sleep the way you ask RPE (§5).
7. **Shoes only as a load signal.** Ask whether they rotate shoes or recently
   changed type (a much lower drop, minimal, or a carbon-plated racer used for
   volume) — treat that as a tissue-load change and ramp it like a surface
   change. Beyond that, gear advice stays out of scope: never recommend models,
   brands, drop, cushioning or fit — refer to a running store or physio.

Store durable answers in the USER dossier and record the anchor with its
provenance (§2).

## 2. The anchor & load metrics

- **Store ONE anchor: Threshold Pace (T)** + LTHR, each with provenance (which test, when — §3). Refresh at the **start + end of every 4–8-week block**, opportunistically off any race PR. A stale anchor corrupts every %-target, zone, and load number.
- **A flat or declining retest is a fatigue/overreach flag FIRST, a pace cut second** — investigate before re-cutting the anchor.
- **CTL/ATL/TSB (Fitness/Fatigue/Form)** compute the same as cycling from run load and are sport-neutral — use them for ramp/freshness. But run load must ride a **musculoskeletal axis** (RPE-minutes + distance + time-on-feet, up-weighted for long runs, downhills, hard/new surfaces), **not** kJ/TSS. Let intervals.icu compute Load on write (GAP-driven); the local estimate is a sanity check only.
- **Anchor write-back:** intervals.icu does **not** auto-calc running threshold pace. After a field test, **suggest-don't-force** — propose the new `threshold_pace`/`lthr`, require athlete/owner confirm, then write with `write_pace_settings` (SETTINGS:WRITE; takes sec/km and converts to m/s). `pace_zones` auto-scale as fractions of the anchor (rewrite only the anchor). **The write applies going forward only — you have no tool that re-zones past runs**; judge historic runs against the anchor that was live when they were run, and never claim history was recomputed. No writable CS field — CS is read-only.

## 3. Test battery

Offer a small menu matched to athlete type. **Do NOT default to Conconi / HR-deflection** (discredited in running). Lab lactate (MLSS/LT) is an authoritative manual override.

| Test | Who | Protocol | Compute anchor |
|---|---|---|---|
| **5k/10k race → VDOT** (default) | anyone who'll race | genuine hard flat effort, last ~4–6 wk; prefer 10k (8–30 min ideal) | Daniels–Gilbert → VDOT → E/M/T/I/R; T ≈ current ~60-min race pace. Never from mile/1500 or marathon |
| **30-min solo TT** | non-racers, beginners | solo, flat, honest; lap at 10:00 | LTHR = avg HR final 20 min; T pace = **last-20-min** pace (raw 30-min avg runs a touch fast — shade slower) |
| **Critical Speed multi-effort** | data-driven | 3 max efforts, different durations (e.g. 1200/2400/3600 m), fully recovered, or 3 genuine races | dist = CS·t + D′ → CS; then **T ≈ CS ÷ ~0.95** |
| **3-min all-out (3MT)** | fit, injury-resistant only | big warm-up, all-out 180 s | CS = mean speed final 30 s; **reject if final-30-s pace still climbing** (sandbagged) |

Don't over-test (each max effort is a hard session). Bias the derived anchor conservative for novices (§4).

## 4. Pace zones — Daniels E/M/T/I/R

Five paces from the single T anchor (compute from the VDOT curve in code — offsets compress at higher fitness, so these multiplier ranges are a template). **Pace ×T = multiplier on T-pace in time/km; >1 = slower.** The **`create_workout` column is the inverse** (fraction of threshold SPEED, >1 = faster) — use THAT column for `paceLow`/`paceHigh`. %LTHR is the HR cross-check; drop to it or RPE per §7.

| Zone | Pace ×T (time/km) | `create_workout` paceLow–paceHigh | %LTHR | %HRmax | RPE / spoken feel | HR valid? |
|---|---|---|---|---|---|---|
| **E** Easy/Long | 1.22–1.40 | 0.71–0.82 | <85% | 65–79% | full sentences, nose-breathable | yes |
| **M** Marathon | 1.06–1.10 | 0.91–0.94 | 85–91% | 80–89% | comfortable-hard, short sentences | yes |
| **T** Threshold (anchor) | 0.98–1.02 | 0.98–1.02 | 95–99% | 88–92% | "comfortably hard," 3–4 words | yes |
| **I** VO2max/Interval | 0.93–0.96 | 1.04–1.08 | ~100% (pinned) | 95–100% | hard, ~1 word, 3–5 min repeatable | **weak — pace leads** |
| **R** Rep/Speed | 0.86–0.91 | 1.10–1.16 | n/a | n/a (lags) | fast but relaxed, controlled form | **no — pace/effort only** |

- **One input → five paces.** Feed VDOT (race) or the 30-min TT into Daniels–Gilbert; derive in code, don't store a flat table.
- **HR invalid below ~2 min** — set `hr_valid=false` on I (short reps), R, strides, hill sprints; cue by pace/effort, never HR.
- **Easy-pace ceiling is a guardrail** (cap E below first threshold / talk test) to stop easy-day drift into the grey zone — but **never police easy pace on the fast side**.
- **Bias novices / low-mileage ~1–2% slower at T and I**, and shade conservative whenever HR climbs above LTHR at the prescribed T pace.
- **CS as alternate engine:** train *around* CS (a boundary), never *at* it — CS− (~95% of 5k pace) for threshold work, CS+ (~100–102%) for VO2max. Relabel the whole library CS-relative OR convert to T — never both in one profile.

## 5. Load & injury guardrail (running-specific, net-new)

Cycling has no equivalent. Applied at prescription **and** debrief. Score on the musculoskeletal axis (§2), not TSS.

- **Session-spike governor (highest-value, best-evidenced — 5,205-runner cohort).** Gate every prescribed/logged run against the athlete's **longest run in the trailing 30 days**:
  - **≤ +10%** → green
  - **+10–30%** → caution (soft-flag)
  - **+30–100%** → require explicit justification
  - **> +100% (doubling)** → **refuse / strongly discourage**
  This paces long-run growth naturally (+1–1.5 km on a 14 km longest, not +5 km) and beats weekly caps or ACWR.
- **Hard-day spacing (scheduler constraint):** **≥48 h between quality sessions; prefer 72 h after a long run / downhill / race** (eccentric deficits persist 48 h+, up to 5–7 d after heavy downhill). Cap **1–2 quality days/wk** (3 only for advanced high-volume; gate on **intensity/RPE, not raw count**). **Never two hard days back-to-back; never long run + hard intervals on consecutive days** for amateurs. ≥1 rest/cross-train day.
- **The 10%/week rule and ACWR are NOT injury gates.** The 10% rule failed its RCT; ACWR is statistically discredited (mathematical coupling, arbitrary windows). Use ~5–10%/wk only as a gentle **beginner** volume ceiling; if ACWR is shown at all it's a **trend signal, never a gate**.
- **Daniels' volume caps are QUALITY-dose limits, not injury caps** — keep and enforce them, relabel: T ≤ ~10% weekly km/session; I ≤ min(8% wk km, 10 km), no rep >5 min; R ≤ min(5% wk km, 8 km), no rep >2 min. Stop the set when form degrades.
- **Bone-stress = highest-stakes injury; a cumulative profile, not a mileage number.** Hard-hold when **rapid load ramp + under-fueling/RED-S signs + chronic <7 h sleep** co-occur (also screen prior stress fracture, menstrual dysfunction, rapid weight loss). Bone remodels over weeks — the athlete "feels ready" before the skeleton is. Extend the recovery-tracker-optional philosophy: **ask runners about fueling and sleep the way the coach asks RPE for power-less rides.** (Legal/scope: screen and refer, never diagnose.)
- **On a niggle flag** (new localized ache that worsens through or lingers after a run), **auto-propose 2–3 easy/cross-train days before the next quality session** — most overuse injuries reverse if caught at the niggle stage.
- **Surface/terrain changes** (road→trail, flat→hills, camber, track) are each their own **gated ramp** — soft surfaces do **not** prevent injury.
- **Cross-training** (bike/pool, matched intensity) holds ~85–95% of run fitness over 4–6 wk while offloading impact, but builds **no** impact tolerance — re-entry still needs a ramp.
- **Gating = all-must-pass.** A session proceeds only if it clears: spike cap, hard-day spacing, weekly quality count, ramp budget, readiness/no-pain, and down-week-not-overdue. **Any failure downgrades the session to easy/rest.**

## 6. Workout library

Bookend intensity sessions: **10–15 min E warmup + 5–10 min cooldown.** Recovery is a **ratio to the work bout** so one template scales across abilities. **Global progression:** change **ONE variable per week** within a 3–6-wk block; weekly volume ramp ≤ session-spike budget (§5). Deload every 3–4 wk (§8). Refresh the anchor every 4–8 wk and rebase. **The table's targets are ×T time multiples — when authoring `create_workout` steps, convert to speed fractions (= 1 ÷ multiple) per the §4 table.**

| Workout | Purpose | Target (×T pace / %HRmax) | Typical structure | Phase |
|---|---|---|---|---|
| **Easy / Recovery** | aerobic base, durability — the ~80% | E 1.22–1.40× / 65–79% | 20–75 min continuous | all |
| **Long run (pure)** | endurance, time-on-feet | 1.15–1.35× | 90–150 min; ≤25–30% wk vol; **time cap ~2.5 h** | base |
| **Long run (quality)** | race-specificity on tired legs | E body + M/T finish or embedded | 26–32 km w/ 2×5 km at MP | build/peak |
| **Continuous tempo** | LT stimulus | T 0.98–1.02× / 88–92% | **20–25 min at true T** (beginners 12–20; +5 min/2–3 wk). ≥30 min → drop to sub-T (0.94–0.97×) + relabel | late base→build |
| **Cruise / threshold intervals** | more time at T, less fatigue | T 0.98–1.02× | 4–6×(1 km or 5–8 min); or 3×10 min; recovery ratio ~0.15–0.25 | late base→build |
| **VO2max intervals** | max aerobic power | I 0.93–0.96× / 95–100% | **4–6×3–5 min** (or 4×4, 5–6×1000 m); ~15–20 min in zone; recovery ratio ~0.5–1.0 jog | build/peak |
| **Reps / speed (R)** | economy, neuromuscular | R 0.86–0.91× | 6–10×200–400 m; **full** recovery (2–3× rep) | base (strides)→peak |
| **Progression run** | fatigue-resistance, pacing | E→M→T ramp | thirds, continuous, no rest | base→peak |
| **Fartlek** | speed off-track, low pressure | I–T by feel (0.93–1.02×) | Mona 90/90/60/60/30/30/15/15 s, equal float | transition/build |
| **Short hill sprints** | power, economy, tissue robustness | near-max by feel | 4–10×8–12 s steep; full recovery | all (esp. base) |
| **Long hill reps** | aerobic strength | ~I–T effort | 4–8×2–4 min; jog-down | base/early build |
| **Strides** | neuromuscular sharpness | ~90–95% top speed by feel | 4–8×15–25 s after easy runs; full 45–90 s | all |

- **A "tröskelpass" is threshold work at T-pace — continuous tempo caps at ~20–25 min; past ~30 min it is sub-threshold (relabel + slow it), or break into cruise intervals.** When an athlete names a session by intensity + a run length ("tröskel, kanske 60 min"), the duration is the **whole outing** (warm-up + T work + E fill), NOT time-at-threshold.
- **Default VO2max to long 3–5 min reps.** Running evidence favors them over 30-30s (opposite of cycling — 4×3 min banked ~328 s vs ~201 s >90% VO2max for 24×30 s); keep 30-30 as an option. Optimize **time above ~90% VO2max**, not the format.
- **Aerobic decoupling (Pa:HR)** — the run analogue of Pw:HR — on **steady, flat, temperate** runs only: **<5% good, >10% build more base.** Always pair the number with conditions (heat inflates it with no fitness change).

## 7. Pace vs HR vs RPE decision rules

Not a two-tier switch — a **terrain-and-duration-aware hierarchy. Primary is grade-adjusted pace (GAP), not raw pace.** Every prescription names a **primary control + a named fallback** (e.g. "tempo 4:20/km GAP; if trail or >22 °C, hold threshold HR / RPE 7").

| Situation | Primary | Fallback |
|---|---|---|
| Easy/steady, good roads | GAP-pace | HR check |
| Rolling/hilly roads | GAP-pace or effort | HR/RPE; power-hike >~20% grade |
| **Steep/technical/long descents** | **RPE/HR** | — (GAP over-optimistic past ~-8%; **never set downhill pace off GAP**) |
| Trail / GPS-poor / treadmill | HR (steady), RPE (hard) | — |
| Heat >~15 °C / altitude >~1500 m / wind | effort — **drop pace targets** | HR early, RPE late |
| **Short intervals (≤3 min), strides, R** | **pace (track/flat) or RPE** | **never HR** (lags 15–60 s) |
| Long intervals (≥5–8 min) | pace/GAP | HR usable at steady state |
| Long run / marathon | **HR first 30–45 min, then RPE** | GAP-pace |

- **HR is itself a flawed fallback.** Expect **10–20 bpm cardiac drift** on long/hot runs — **don't chase it by slowing indefinitely.** Require an individually **tested LTHR — never age-formula HRmax.** Cross-check the E ceiling against talk test / decoupling, not just %LTHR (the LT1–LT2 gap is highly individual).
- **Treat disagreement as data:** high RPE + low HR ⇒ fatigue/under-recovery flag; low RPE + high HR ⇒ heat/dehydration/drift flag. Late in long/hot efforts, trust RPE + GAP over a drifting HR (directional evidence — flag as debate, not law).

## 8. Periodization

Plan **backward from the A-race.** Macro (12–24 wk: ~12 fit, ~16–18 standard, ~24 low-base) → meso (3–6 wk single-focus blocks ending in recovery) → micro (the week).

- **Phase allocation:** base **40–50%** (easy volume, long runs, strides, hill sprints, late-base tempo; **pyramidal**) → build **25–30%** (threshold + VO2max featured, hills, fartlek) → peak/sharpen **10–15%** (race-specific) → **taper 1–3 wk.**
- **~80% easy is the robust floor** (shared by pyramidal AND polarized) — **encode it.** Count by **session-goal** for athletes without lab data (each session labelled by its hardest segment; ~4 of 5 sessions easy) — **never mix conventions in one report.**
- **The split of the hard ~20% is the ONE tunable "polarization" parameter — NOT a hard-coded 80/20-polarized default.** The polarized-over-pyramidal edge is **small and contested** (shows up mainly for VO2peak in fit athletes in short blocks; nil for TT/threshold outcomes). Default season shape = **pyramidal base/build → race-specific peak as a discrete phase change.** Present PYR→POL as a low-risk default, not a performance guarantee.
- **Specificity by distance:** **5k–10k peaks tilt to VO2max/CV/speed; HM–marathon peaks stay threshold/MP-weighted** (more pyramidal, not more polarized). Make the key session resemble the race more as weeks-to-race shrink.
- **Scale by level:** hold ~80%+ easy for high-volume/trained; time-crunched (<~4 h/wk) can carry a slightly higher hard fraction — don't hard-fail such a plan. Novices: prioritize consistent easy volume + ~2 quality/wk over PYR-vs-POL sequencing (no distribution advantage yet).
- **Down weeks:** default **3:1** (2:1 for masters/novice/injury-prone), cut volume **~30–40%** off the trailing 3-wk average, trim the long run, **keep a reduced dose of intensity + normal frequency** (don't zero quality). **Autoregulate the trigger** — pull the deload forward when fatigue markers cluster (stalled pace-at-effort, rising RPE, poor sleep, niggles). Base can run 6–8 wk before a cutback.

### Taper (best-quantified module — key off the event)

- Duration: **5k/10k ~7–10 d · HM ~10–14 d · marathon ~2–3 wk.**
- Cut **volume progressively to ~50–60% of peak; MAINTAIN intensity; MAINTAIN session frequency.** Keep short race-pace doses (a few strides or 3–5×1 km at goal pace every few days). Marathon: last hard high-volume session ~10–14 d out.
- **Prevent the generator from zeroing intensity or run frequency** — the most common taper error. Expected gain ~2–3%.

## 9. Individualization (modifiers on top of the library)

- **Masters 40+:** default down-weeks to **2:1**, add ~24–48 h E buffer after downhill/long/eccentric loads (slower repair); keep ≥2 quality/wk year-round (don't drift to volume-only); prioritize heavy strength + impact for bone; protein 1.6–2.0 g/kg/day. Gate recovery on readiness, not birth year.
- **Novice / returning:** conservative anchor (§4), 5–10%/wk volume ceiling, 2:1 cutbacks, ~2 quality/wk max, extra spacing after quality; grow mostly-easy volume first.
- **Female clients** (reference athlete is MALE — do not apply to him): symptom-driven intensity swaps (not hard-coded cycle phase); screen ferritin 1–2×/yr (flag <30 µg/L; iron-deficiency risk higher in female runners); peri/post-menopausal → heavy resistance + impact loading, protein upper range.
- **Strength/plyo for runners:** sell honestly for **economy (+2–6%) and durability** (2–3×/wk heavy compound + conservative plyo, ≥8–12 wk) — **do NOT promise injury prevention** (runner-specific RCT evidence inconclusive). No heavy legs in the final ~10–14 d before an A-race or in the 48 h before a key session/race.
- **Cadence:** **no universal 180 spm target.** Cue a ~5% bump only for a specific reason (recurrent knee/shin/tibial issue or clear overstriding, e.g. <165 spm easy), gradually, within ~5–10% of natural, at the same effort.

## 10. Readiness gates & safety

- **Readiness signals are device-agnostic and sport-neutral** (`read_wellness`: `hrv`, `restingHR`, `sleep*`, `readiness`, …). Gate on **HRV-vs-baseline + RHR-vs-baseline + sleep** as trends, never a single perturbed morning; the composite `readiness` score is device-specific — read it as a within-athlete trend. **Never name the tracker brand** in chat. **No tracker? Gate on load + feel** (asked RPE + sleep-in-words), not silence — "slept badly, legs heavy" downgrades intensity like a low-HRV morning.
- **Sleep hard-gate:** <6 h or large acute debt → cancel quality, sub E/rest.
- **Sickness:** fever or below-the-neck = stop, clear the calendar; above-the-neck = easy at most.
- **Pain:** traffic-light it, pull/modify today immediately, **never diagnose**; red flags → refer out in plain words. Bone-stress suspicion (localized bony pain, worsens with impact, night pain) → **stop running, refer** — do not "run through."
- **Non-functional overreaching:** performance decrement persisting >2 wk despite reduced load → stop hard work; track pace-at-effort, mood, RPE (HRV alone is not a reliable standalone marker).
- **Fueling:** never key sessions fasted; carbs during runs >~75–90 min; RED-S red flags (falling pace despite training, bone stress injuries, recurrent illness, poor sleep, low libido/menstrual dysfunction) → **raise intake or cut load and refer — don't just cut calories.**

## 11. Heat acclimation & environmental prep

Heat training is a legal, periodized adaptation — treat it like altitude, not a
supplement. It is distinct from **racing in the heat** (pace-off-effort, hydration
— covered in §7/§10): this is *training* the body to tolerate heat, planned toward
a known-hot goal race. **Gate it through the playbook's "when & how to suggest"
rules first** — it's a real systemic stressor, not a free win.

- **What adapts, and how sure we are:**
  - **Plasma volume +4–15% in 3–6 days** [STRONG] — the primary early adaptation;
    lower HR, higher stroke volume, less cardiac drift. Partly transient.
  - **Thermoregulatory** [STRONG]: earlier sweat onset, higher + more dilute
    (Na⁺-sparing) sweat, lower resting/exercising core temp. Slower (~8–14 days).
  - **Cellular/metabolic** [MODERATE]: ↑HSP72, improved lactate threshold, lower
    RPE/thermal strain, some glycogen sparing in the heat.
  - **Haemoglobin mass** [CONTESTED]: expands plasma volume but does NOT reliably
    raise Hb-mass. **Sell plasma-volume expansion as certain; never promise a
    blood/Hb boost.**
- **"Poor man's altitude" / cool-weather transfer** [CONTESTED — do NOT over-sell]:
  one landmark trial showed cool-air VO2max/threshold gains after 10 days of heat,
  but most follow-ups failed to replicate it. **The robust benefit is in the HEAT
  (~4–7% performance). Cool-condition gain is 0–3%, often null in trained runners —
  present it as possible-but-unreliable, never a reason to heat-train for a cool
  race.**
- **Dose–response** [STRONG]: **5–7 days** captures most cardiovascular/plasma
  adaptation; **10–14 days** completes the sweat adaptation and best optimizes
  hot-race performance (induction *length* is the dominant moderator). **14+ days**
  entrenches it; any Hb-mass effect needs ≥3–5wk.
- **Method:**
  - **Active:** 60–90 min in the heat, **5+ sessions/wk**, ideally consecutive
    during induction — easy-effort runs in the heat, or a treadmill in a warm room.
    Controlled hyperthermia (hold core ~38.5°C) or fixed submax effort both adapt
    similarly. Gate on **effort, not pace** — heat slows pace with no fitness loss.
  - **Passive, post-exercise (the practical route)** [MODERATE, weaker evidence]:
    straight after a normal temperate run, **hot bath ~40°C for ~40 min** or
    **sauna ~80–90°C for 30–60 min**, ~**6 consecutive days** → ~+5% hot-condition
    performance, retained ≥2wk. Pooled evidence is trivial/low-certainty — a
    low-cost add-on, not a guarantee.
- **Timing before a hot goal race** [STRONG consensus]: begin **~2 weeks out**;
  6–10 days for near-complete HR/sweat adaptation, ~2 weeks to optimize. Decay is
  slow (~1 adaptation-day lost per 2 days off) — a **maintenance session every 2–5
  days (1–3×/wk)** through the taper preserves it.
- **Cost & risk** [STRONG]: heat work adds real systemic + sleep-disrupting load
  and can blunt hard-session quality. Put it on easy days or *after* the key
  session, protect sleep, don't stack it on a peak block. Start euhydrated, cap
  fluid loss <2% body mass, stop on heat-illness signs (disproportionate HR/core
  rise, dizziness, nausea, confusion, stopping sweating). **Do NOT heat-train when
  ill/febrile, dehydrated, sleep-deprived, or with cardiovascular disease.**
  Masters: aging blunts the sweat response and raises baseline strain, but it still
  works — ramp conservatively, hydrate/monitor harder, allow more recovery.
- **Evidence:** Périard/Racinais/Sawka 2015; Racinais 2015 (consensus); Benjamin
  2019 (meta); Tyler 2016; Lorenzo 2010 vs Karlsen 2015 (cool transfer); Daanen
  2018 (decay); Zurawlew 2016 + Solomon & Laye 2024 (passive); Rønnestad 2021/22 vs
  Lundby 2025 / Oberholzer 2019 (Hb-mass).

## 12. Contested levers — flag as individualized, never dogma

State the well-established parts with confidence: **~80% easy floor, the session-spike governor, hard-day spacing, taper mechanics, "CS ≠ T."** Flag these as debated:

1. **Polarized-vs-pyramidal split** — ~80% easy is settled; the hard-20% split is small, contested, phase/individual-dependent. Pyramidal is evidence-equal and often better for base and marathon. Don't sell POL as proven-best.
2. **Easy volume as the "master variable"** — it's a proxy (cross-sectional, reverse-causation). Grow mostly-easy volume first only for genuinely under-volumed, durable, time-rich athletes; otherwise the intensity split is the better plateau lever.
3. **Double-threshold (Norwegian) sub-LT2** — world-class results but thin controlled evidence and amateurs get it wrong. Offer only as an **advanced** option gated on aerobic base + recovery + a lactate/pace proxy. **Intensity cap = HM-to-marathon effort / "holding back, full sentences," ~2–3 mmol — NOT 1-hour-race effort** (that's LT2, the ceiling — the classic amateur error). Never stack two-a-days for time-crunched/low-volume athletes.
4. **RPE-over-HR late in long/hot efforts** — directional (small-n gas-analyzer data); coach it, don't over-claim.
5. **30-30s for VO2max** — loses to long 3–5 min reps in running (§6); don't import cycling's short-interval superiority.
6. **MAF (180−age)** — unvalidated per-individual; conservative beginner easy-HR ceiling only, never the master anchor.
7. **Soft surfaces / strength-work as injury prevention** — weak/inconclusive; ramp surface changes as a gated progression; sell strength for economy + durability.
8. **Run TSS = bike TSS** — a modeling convenience, not measured equivalence; model run load on the musculoskeletal axis and weight long/downhill above metabolic cost.

## 13. Evidence notes (cite why)

- **TID / 80-20:** Seiler 2010; Stöggl & Sperlich 2014; Casado 2022; Filipas 2022 (PYR→POL, small effect); Kenneally 2018 (elite TID review).
- **Pyramidal vs polarized:** Filipas 2022; Treff 2019; 2024 meta (VO2peak yes, TT/threshold null).
- **Pace zones / VDOT / Daniels:** Daniels *Running Formula*; Daniels–Gilbert VDOT tables; Jones (Critical Power/Speed); Pettitt 2016 (CS).
- **Critical Speed / D′ / 3MT:** Jones & Vanhatalo 2017; Pettitt 2012; Vanhatalo 2007 (3MT).
- **Threshold vs CS distinction:** Jones 2019 (CP domain review); Galán-Rioja 2020 (CP vs MLSS).
- **VO2max reps (long > 30-30 in running):** Rønnestad 2020; Bossi 2020 (time >90% VO2max); Billat vVO2max work.
- **Session-spike governor / load:** Nielsen 2014 (>30% spike); Garmin-RunSafe cohort (n=5205); Damsted 2018.
- **10% rule / ACWR debunk:** Buist 2008 (10% RCT null); Nielsen 2019; Impellizzeri 2020, 2021 (ACWR critique).
- **Taper:** Bosquet 2007 (meta); Mujika & Padilla 2003.
- **GAP / terrain / HR fallback:** Minetti 2002 (cost of running on gradients); Strava GAP; cardiac drift — Coyle & González-Alonso 2001.
- **Bone stress / RED-S:** Mountjoy 2023 (IOC REDs); Warden 2021 (bone stress injury); Tenforde 2016.
- **Strength/economy:** Blagrove 2018 (meta); Balsalobre-Fernández 2016; runner-injury-RCT inconclusive (Lauersen 2018 general, running-specific thin).
- **Norwegian / double-threshold:** Casado 2023; Bakken/Ingebrigtsen practice reports (thin controlled evidence).
- **Heat acclimation:** Périard/Racinais/Sawka 2015; Racinais 2015; Benjamin 2019 (meta); Tyler 2016; Lorenzo 2010 vs Karlsen 2015 (cool transfer); Daanen 2018; Zurawlew 2016, Solomon & Laye 2024 (passive); Rønnestad 2021/22, Oberholzer 2019, Lundby 2025 (Hb-mass).

## 14. Rides as cross-training (running-primary athletes)

Applies when the athlete's primary discipline is **running** — not for triathletes or HYROX athletes, whose own references set their multisport balance. Running stays the goal; a ride is cross-training, identified from the activity's own type (any *Ride — Ride, VirtualRide, GravelRide, MountainBikeRide), never a second plan.

- **Low-impact aerobic volume.** Riding adds aerobic work with almost no impact or eccentric load — the classic way to grow the engine above what the legs can yet run, to keep fitness through a niggle, or to add volume in a heavy block.
- **It still counts toward load.** Ride load enters CTL/ATL/TSB and total weekly hours. Easy riding is cheap on tendons and bones, but a long or hard ride is real systemic fatigue: count it in the hard-day budget and the ramp, never treat it as free.
- **Don't let it eat recovery.** A hard or long ride the day before a key run, or on the planned recovery day, is the common failure — name it when it happens. Keep rides easy (conversational, RPE 3–4, or Z1–Z2 where power/HR zones exist) unless the athlete explicitly wants bike intensity.
- **Transfer is partial.** Cycling (like pool running) holds ~85–95% of run fitness for weeks while offloading impact (§5), but builds **no** impact tolerance: after a stretch of mostly riding, the run re-entry still needs its own `check_run_load`-gated ramp.
- **Injury use.** When a niggle or bone-stress concern pauses running, easy riding is the default substitute if it is pain-free — match duration to the planned easy run, keep intensity low unless a clinician clears more, and screen/refer per §10.
- **Same-day Ride + Run is allowed** (a bike commute plus a run, a short spin as recovery, a brick). Load rules govern, not a calendar block: the combined day counts once toward the hard-day spacing (§5) — never pair a hard ride with quality running or put a long ride next to the long run.
- **No cycling metrics as goals.** Watts, FTP and cycling PRs are context for the ride, not targets for a runner. Do not propose cycling tests or power work unless the athlete asks for bike goals.
- **Debrief it as a ride.** Duration, HR, terrain and feel (watts only when present); keep it proportionate — one or two useful observations and how it fits the running week (recovery, load, what it means for the next key run).
- **Planning.** Offer rides as optional aerobic volume, a recovery spin, or a planned substitute for an easy run when impact load is the limiter; they never displace the key runs, the long run or the recovery day. If riding grows toward a real cycling goal, ask whether the primary sport has changed rather than silently coaching two plans.
- **Indoor/commute rides.** Short commutes are low-cost volume but add up — include them in weekly hours so the athlete's real load is visible, and do not debrief every commute as a session unless it was hard or long.
