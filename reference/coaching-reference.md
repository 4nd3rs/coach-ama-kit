# Coaching Reference — Cycling Periodization (v2)

## 1. How to use this file

- Your training-science cheat sheet. Consult before planning. **Defaults, not laws** — `USER.md` data and constraints override.
- **Prescribe by power.** Every target here is a **fraction of FTP** (and every dose per kg). Convert to watts with THIS athlete's CURRENT FTP and weight — `read_athlete_profile` — never with numbers remembered from another rider or an old test; rebase on every FTP retest.
- HR/RPE are secondary gates (HR lags inside short reps). Get an RPE (1–10) + one line of feel after key sessions; high RPE at normal watts = fatigue flag even when readiness looks fine.
- Where evidence is thin it's flagged in-line ("evidence mixed/emerging — individualize"). Don't upgrade those to certainty when you talk to the athlete.
- Most cycling TID/interval/strength RCTs are small (n~10–48) and short (6–12wk). Treat group-mean superiority as a tendency, not a guarantee for this rider; let `LEARNINGS.md` override the literature.

## 2. Load metrics & ramp rates

- **CTL (Fitness)** — 42-day load average; accumulated fitness, rises slowly.
- **ATL (Fatigue)** — 7-day load average; rises/falls fast.
- **TSB (Form) = CTL − ATL** — readiness. Negative = building/fatigued, positive = fresh/tapered.
- **Load (TSS-like)** — 1h at FTP ≈ 100. `create_workout` estimates it from the spec.
- **CTL ramp:** sustainable build **~5–8 CTL/week** (conservative default +3–6). Sustained **>8/week** for multiple weeks risks non-functional overreaching — de-load. Heuristic, not a physiological law; assumes a current FTP.
- **TSB floor:** don't let TSB sit below **−20 to −30 for >2–3 consecutive weeks**. Persistent deep-negative TSB + elevated RHR, poor sleep, mood decline, or stalled power = non-functional overreaching → trigger a recovery week. Heuristic.
- **Refresh the threshold anchor every 4–6 weeks.** CP is the house default (12+3–5min pair → CP + W′; `read_power_model` reads the fit); ramp/20-min are fallbacks. A stale anchor corrupts every %-target, TSS, ramp, and TSB number. FTP stays the zone anchor: **FTP ≈ 0.96×CP**.
- Post-recovery-week CTL dipping slightly is normal and good.

## 3. Intensity distribution & periodization

- **80/20 backbone:** ~80% of sessions/time **low-intensity below VT1** (≤~75% FTP, conversational), ~20% genuinely hard. Minimize sustained time in the threshold grey zone. Fix one **3-zone model around VT1/VT2** (not a naive %FTP histogram) before computing the split. Preserve this regardless of HIT model.
- **Hard-session cap:** **2/week** for most, **at most 3/week** with a strong aerobic base, **≥48h apart**. HIT benefits plateau past ~2–3/wk and ~3–5wk; more raises overreach/illness risk without added adaptation. Thin base → add easy volume *before* adding interval frequency.
- **Polarized (POL):** for VO2max/peak-power over short blocks (<12wk) in trained riders, prefer POL over threshold-only — bigger gains in PPO, LT, time-to-exhaustion. Advantage is **real but small and outcome-specific** (VO2peak SMD ~0.24; <12wk ~0.40; elite ~0.46) and **disappears for time-trial and threshold-power outcomes and for blocks ≥12wk**. Don't over-claim POL for steady-state race performance.
- **Pyramidal:** large LIT base + moderate tempo/threshold + small severe dose. Use in **base**, especially for recreational-competitive riders; shift toward POL for build/peak. In cyclists the pyramidal-vs-POL gap is smaller than in runners.
- **Sweet-spot (88–94% FTP):** time-efficient aerobic stimulus per hour for time-crunched base; meaningful FTP gains in 4–6wk but plateaus earlier and accumulates more fatigue — cap concentrated SST blocks at **4–6wk**, then refresh with LIT + true VO2max. Marketing-heavy, thin long-term RCT support: time-efficient, *not* adaptation-superior.
- **Block periodization (VO2max):** concentrate **~5 VO2max sessions in one shock week**, then ~3 weeks of reduced HIT (~1 hard/wk) to consolidate; repeat the 4-week cycle. Rønnestad's trials show ~2× the VO2max gain of even spread (~8.8% vs 3.7%) in well-trained cyclists — though it doesn't always out-perform a *cyclically progressive* traditional plan (Bækken 2022), so treat it as a strong option, not a guaranteed edge. The benefit is the **sequence** — back-to-back shock weeks without consolidation risk NFOR.
- **Macrocycle:** Base → Build → Peak/Taper → Race → **Transition**. Base = high-volume LIT (pyramidal ± sweet-spot). Build = add race-specific threshold/VO2max, shift toward POL, block-periodize HIT for trained riders. Peak = race-pace sharpening + taper. **Deload every 3–4 weeks** (3:1 or 2:1; masters often better on 2:1). Macro-sequence is expert consensus.
- **Transition / off-season — the season does NOT end at the A-race.** After the season's last A-race: **1–2wk off structure** (ride on feel or not at all — the mental break IS the point), then **2–4wk unstructured riding + strength AA phase** (§7) before the next Base. **Expect and allow CTL to drop ~10–20%** — rebuilding from a rested base beats defending a number. Write the transition into the calendar (notes) and `PLAN.md` like any other block; a blank calendar after the A-race reads as an ended coaching relationship, not planned rest.
- **Multi-peak seasons (two A-races):** **≥10–12wk apart** → full re-build between (1wk recovery, 2–3wk re-base, then build → taper). **6–10wk apart** → hold, don't re-base: maintenance volume, 1–2 quality/wk, mini-taper into race 2. **<6wk apart** → one peak: recover, stay sharp with race-pace touches, freshness decides — fitness is already set. Consensus practice, not RCT-derived.
- **Year over year:** after the last A-race, run a **season debrief** into `PLAN.md` — what moved (FTP, durability, limiters), what didn't, adherence vs plan — and sketch next season: start month, first A-race candidate, the 1–2 limiters to lead with, and a target starting CTL (~85–90% of this season's peak). Next season starts as a plan, not a blank page.

### Taper

- **2-week progressive (exponential, fast-decay) taper.** Cut **volume 41–60%** via **shorter sessions**, while **holding intensity and frequency** (cut frequency ≤20%). Expect ~2% gain (range 0.5–6%).
- **Preserve intensity above all** — keep race-pace/VO2max touches. Cutting intensity is the most common taper error and erases the benefit.
- Personalize the volume cut within the 41–60% band by event (crit vs road vs MTB marathon) and the rider's historical taper response. Aim **TSB ~+5 to +15 on event day**.

### Detraining & maintenance

- **<2wk break (illness/travel):** low-cost. VO2max −4–7% in 2–3wk, mostly blood/plasma volume, rapidly reversible — resume near prior load, don't restart periodization.
- **>4wk layoff:** VO2max −6–20% (~10% by 5wk, 13–20% by 8wk); recently-gained fitness lost first, long-standing base stays above untrained. Rebuild with a fresh base block + conservative ramp.
- **To maintain through low-availability periods:** keep intensity, cut volume/frequency — **1–2 HIT/wk preserves VO2max/FTP** for several weeks (inverse of the taper principle). Don't apply decay curves mechanically — individual.

## 4. Workout library

Bookend every intensity session: **10–15min warmup** (ramp to ~0.6) + **5–10min cooldown**.
**Global progression:** change **ONE variable per week** within a 3–6wk block (+1 rep, OR +1–2min work, OR −5–10s recovery, OR +2–3% power). Weekly load ramp 1.0–1.2× prior (avoid >1.3). Deload every **3–4wk by default** (interval blocks may stretch toward 6wk for well-recovered, lower-frequency riders): cut interval volume ~40–50%, keep some intensity. Refresh the threshold anchor (CP by default) every 4–6wk and rebase.

| Archetype | Purpose | Prescription (fraction of FTP) | Schedule |
|---|---|---|---|
| **Endurance (LIT/Z2)** | Aerobic base, durability — the 80% | 60–180min steady **0.60–0.70**, conversational, ≤VT1 0.75 | Most days, all phases |
| **Tempo** | Aerobic stimulus per hour | 2–3 × 15–20min **0.76–0.85** | Base |
| **Sweet-spot** | Time-efficient aerobic/FTP | 2–4 × 12–30min **0.88–0.94**, 30–60+min total, 5min easy | Time-crunched base; emerging long-term |
| **Threshold / FTP** | FTP & TTE specificity, lower-cost quality | **2×20min** (or 3×15; 40–60min total) **0.95–1.05**, 5–10min recovery, 1–2×/wk | Build |
| **VO2max — 4×8 (primary)** | Strong, reliable VO2max stimulus (not strictly superior to short intervals) | 4 × 8min **0.95–1.05**, highest power held *even across all 4 reps*, ~90% HRmax, 2min recovery; 2×/wk, ~7wk blocks | Build/Peak |
| **VO2max — 4×4** | VO2max | 4 × 4min **1.06–1.18** max even across reps, 3min active recovery **0.60–0.70**; gate by power (HR lags) | Build/Peak |
| **VO2max — 30/15 micro** | Most time >90% VO2max at lower RPE | 3 sets × 13 × (30s **1.06–1.20** / 15s **~0.50**), 3min easy between sets; 2–3×/wk | Build/Peak, trained/elite blocks |
| **SIT (sprint interval)** | Short VO2max/anaerobic boost | 4–6 × 30s all-out (**≥1.50 FTP**), 4min recovery; 2–3×/wk, **2–6wk blocks only** — very stressful, smaller delta when trained | Short block, not year-round |
| **Neuromuscular sprints** | Peak power, recruitment | 5–10 × 8–15s maximal from low cadence (**≥2.0 FTP**), full recovery 3–5min; place fresh, 1–2×/wk | Any phase when fresh; power outcome coaching-based |
| **Durability efforts** | Defend power glycogen-low; Type IIa | 2–4 × 8–10min threshold/VO2 (or 20–40min SST) in **final third** of long ride, **after ~2000–3000 kJ**; ≤1×/wk, high cost | Build/Peak; emerging |

- **4×8 power sits in Z4 by design:** it is a self-paced VO2-stimulus format — max even pacing over 8min lands at 0.95–1.05 FTP; the stimulus is accumulated time >90% HRmax/VO2max, not a Z5 power target.
- **VO2max dose target:** ≥10min cumulative >90% VO2max per session — via even 4–8min bouts OR 30/15 micros. Time-at-intensity is the driver, not the format.
- **Threshold/SST honesty:** 2×20 and sweet-spot rest on fatigue-efficiency and convention, not head-to-head RCT superiority — they do *not* out-perform 4×8 / 4×4 / 30-15 for VO2max.
- **A "tröskelpass" is threshold INTERVALS — never a continuous block at threshold.** Threshold (and every Z4+ session: sweet-spot, threshold, VO2max) is always reps with recovery — 2×20, 3×15, 4×10 @ 0.95–1.05, etc. **Nobody can hold true threshold continuously past ~20–30 min**, so never prescribe or build a single unbroken effort longer than one interval at threshold power; a continuous effort that long is by definition tempo/sweet-spot (sub-threshold) — label and power it as such. When an athlete names a session by intensity + a ride length ("tröskel, kanske 2–3h"), the duration is the **whole outing** (warm-up + threshold intervals + Z2 to fill the hours), NOT time-at-threshold: choose a sane interval structure, name it as intervals ("Tröskel 3×15 min"), and build the calendar workout's power blocks as intervals — never one flat 2–3h block at FTP.
- **Aerobic-decoupling test (monitor, not workout):** 60–90min steady **0.60–0.72**; Pw:HR decoupling **<5% suggests good durability**, **>5% flags a base/durability gap** (heuristic — the 5% cutoff scales with fitness and conditions; emerging evidence) → add Z1 + durability work. Retest every 4–8wk.

### Power zones (fraction of FTP — `powerLow`/`powerHigh`)
- Z1 Recovery <0.55 · Z2 Endurance 0.56–0.75 · Z3 Tempo 0.76–0.87 · Z4 Threshold/Sweet-spot 0.88–1.05 (SST ~0.88–0.94) · Z5 VO2max 1.06–1.20 · Z6 Anaerobic >1.20

### Weekly structure
- 2 (base) to 3 (build/peak) hard days; rest endurance or rest. Never stack two hard days back-to-back unless deliberately block-training a recovered athlete.
- Longest ride on the day with most time. Time-limited athletes keep the same 2 (max 3) quality sessions and cut easy volume, never intensity — bias the base toward sweet-spot when the goal event is steady-state/threshold-driven, toward polarized (LIT + true VO2max) when it is punchy/variable (consistent with §5's <8h/wk rule).
- **Volume days space like hard days — intensity is not the only load.** A big-volume day = a session at or above the LARGER of 2.5h or ~30% of the athlete's weekly hours (a 20h/wk rider's 2.5h spin is routine; a 7h/wk rider's is not). After a big-volume day, the next day is ≤90min Z1–Z2 or rest. Two consecutive big-volume days (long+long, or long ride next to a long run/hike — ALL sports count) are legal **only as a deliberate block**: the reason is recorded in `PLAN.md` (weekend block, camp, event simulation) and the athlete is told — an unexplained big-day pair reads as a coach who isn't looking at the week. Default the big weekend block to Sat+Sun when the athlete rides weekends; the Sun→Mon seam into a work week is almost never the right place for it.
- **≥1 full rest or recovery day (≤45min Z1) every week, every phase.** Monotony kills adaptation before volume does (§2 Foster): harder hard days, easier easy days, and a true off day beat seven medium days.
- **The week is the unit, not the day.** Lay a week out as a whole — volume total vs the athlete's hours, hard-day count and spacing, long-ride placement, strength slots — before filling its days; extending a calendar tail one day at a time without re-reading the surrounding week is how accidental stacks happen.

### Weekly microcycle (where strength fits)
Stack stress to keep hard days hard and easy days easy, and respect lifting↔riding interference (heavy lift AFTER the key ride, ≥3h later or a separate session; never heavy legs in the 48h before a key ride/race).

**Off-season / base — 2 quality + 2 strength:**
- Mon: rest/mobility + **robustness/upper-body** (low interference)
- Tue: **VO2max/threshold** (key ride) → **heavy legs** ≥3h later (stack the hard day)
- Wed: easy Z2
- Thu: **heavy legs #2** (or 2nd quality) — keep ≥48h from the weekend long ride
- Fri: rest/easy
- Sat: **long Z2 / durability** (longest day)
- Sun: easy Z2 or rest

**In-season — 2 quality + 1 strength maintenance:**
- Heavy legs 1×/wk AFTER the week's first key ride and ≥48h before the weekend race/long ride; robustness/upper-body stays 1×/wk on an easy day; no heavy legs in the final 48h of race week.

## 5. Individualization (modifiers on top of the library)

### Masters 40+ / 50+
- **Keep ≥2 hard quality sessions/wk year-round** — don't drift to volume-only. VO2max declines ~5–6.5%/decade in trained masters vs ~10–12% sedentary; volume/intensity loss explains ~39–54% of it. Masters VO2 session: 4–6 × 3–5min **1.06–1.20**, 1:1→1:0.5 work:rest.
- **Don't auto-cut recovery by age.** Matched-status older athletes recover from acute HIIT like younger ones — gate on readiness, not birth year.
- **But weight subjective recovery more:** more soreness/fatigue at equal objective recovery, and slower repair from eccentric/damaging loads (heavy lifting, MTB descents, long durability). After those, add ~24–48h LIT buffer for 50+ before the next quality day.
- **Strength matters more with age** (defends type II fibers, RFD, bone — cycling is non-osteogenic). Keep heavy: 6–10RM, 2–3 reps in reserve.
- **Plan ~5–8%/decade FTP decline** (~0.5–1%/yr from mid-30s). Aggressive intensity + strength keeps real loss to ~10–15% between a well-trained 40- and 55-yr-old (vs 30–40% with detraining).
- **Protein 1.6–2.0 g/kg/day**, ~0.4 g/kg/meal across ~4 meals, leucine-rich, a dose within ~2h post-session (anabolic resistance).
- **Time-crunched masters:** keep both quality sessions (VO2 + threshold), trim easy volume — not intensity.

### Sex (female clients — reference athlete is MALE; do not apply these to him)
- **No hard-coded menstrual-phase prescription** — at most a trivial early-follicular reduction, on low-quality contradictory evidence. Use **symptom-driven** swaps: heavy bleeding/cramping/poor sleep/low energy → endurance or recovery, reschedule intensity. Track 2–3 cycles to learn the pattern.
- **Screen ferritin 1–2×/yr** + on fatigue/perf drop. Flag <30 µg/L low, <15 depleted (15–35% of female athletes affected). Iron: medically-guided, taken **away from the 3–6h post-exercise hepcidin surge** (morning/rest days, with vit C). Ferritin rises reliably; performance gains small except in true deficiency.
- **Peri/postmenopausal:** prioritize heavy resistance + bone/impact loading (~5RM compounds + impact, 2×/wk), protein upper range ~2.0 g/kg/day. "Mostly true HIIT + heavy lift, minimize moderate junk volume" = reasonable **default** (expert-opinion, not proven).
- Women are more fatigue-resistant at the same relative intensity for sustained efforts (more type I) — may tolerate longer threshold time-in-zone; task-dependent. Women may plateau central VO2max adaptations earlier (~3mo vs ~9mo) — vary the stimulus sooner; conflicting evidence, individual dominates.

### Experience / training status
- Effect sizes shrink with training status — expect smaller deltas than headline %; weight trained-cyclist studies (Seiler 2013, Rønnestad 2015/2020, Stöggl & Sperlich 2014).
- Novice to strength: ramp load over 2–3wk, start 8–10RM before 4–6RM — don't push straight to 4RM.

### Time budget
- **<8h/wk:** sweet-spot base + 2–3 HIT, **cut volume not intensity**. Minimum effective maintenance: 2–3 HIT/wk preserves VO2max/FTP even with 20–50% less volume. Frequency cuts tolerate better than intensity cuts.
- **For male athletes:** don't apply the female-specific rules above, and don't supplement iron without lab-confirmed deficiency (overload risk).

## 6. Readiness gates (wearable recovery)

Fields (`read_wellness`): `hrv`, `restingHR`, `sleepSecs`, `sleepScore`, `sleepQuality`, `readiness` (0–100), `spO2`, `respiration`. These are **device-agnostic** — intervals.icu normalizes them from whatever tracker the athlete connected (Whoop, Garmin, Oura, Apple Watch, Polar…). **Never name or assume the brand** in chat: say "din sömn / återhämtning / HRV", not "Whoop", unless the dossier records the specific device.

- **No tracker? Gate on load + feel, not silence.** Many athletes own no wearable — `hrv/restingHR/sleep*/readiness` are simply absent while CTL/ATL/TSB still compute from ride load. Do NOT tell them data is "missing" or ask them to sync. Gate hard days on **TSB/ramp-rate + the last session's execution + today's asked RPE/feel and sleep-in-words**; a "slept badly, legs heavy" answer downgrades intensity exactly like a low-HRV morning would.
- **Gate on the raw signals, which ARE comparable across devices:** HRV-vs-baseline + RHR-vs-baseline + sleep. The composite **`readiness` (0–100) score is device-specific** — each brand scales it differently, so read it as a soft within-athlete trend vs their own normal, not an absolute number. The **Whoop-specific** thresholds **≥67 green / 34–66 yellow / <34 red** apply only when the athlete uses Whoop; for any device, cross-check the HRV/RHR trend before acting on the score alone.
- **HRV-guided gate (overlay):** gate hard days on the **7-day rolling LnRMSSD vs an individualized SWC band** (baseline mean ± 0.5 × between-day SD, built over a 4-week baseline) — not a single day. Within/above band → green-light MOD (SST/threshold) or HIT (VO2max); below → Z2 or rest. Measure 1-min recording after 1-min stabilization, same posture on waking, ≥3–4×/wk.
- **Set expectations:** HRV autoregulation does **not** reliably beat a good fixed plan for VO2max — its value is **fewer bad sessions and fewer non-responders**. Risk-management overlay, not a fitness multiplier. Cap weekly HIT to the days HRV permits rather than forcing a fixed count.
- **Trust raw signals, discount the score.** For Whoop specifically, RHR and HRV agree well with gold standard (CCC ~0.91/0.94) while the composite "recovery %" and 4-stage sleep are weakly validated; the same principle holds for other consumer wearables. Gate on RHR elevation + HRV-vs-SWC, not the colour/score.
- **RHR gate:** morning RHR ≥5 bpm (~7%) above 7-day baseline → downgrade intensity even if other signals look fine.
- **Sleep hard-gate:** <6h or large acute debt → cancel VO2max/threshold, sub Z2/rest (sleep loss degrades efforts >30min — pooled effect ~5% slower TT, *moderate* not huge; longer efforts hit hardest). Push sleep extension in heavy blocks: 8–9h habitual, toward 9–10h before key races. Naps allowed, <30min, early afternoon.
- **Rule out confounders before backing off on one low HRV/RHR day:** evening alcohol (dose-dependent next-morning suppression), a late-evening hard session, illness onset, caffeine, dehydration, or a different measurement posture can all fake a "recovery" signal — and for women, menstrual phase. Act on the 7-day trend, not a single perturbed morning. *Plews & Buchheit; Pietilä 2018 (alcohol) (moderate).*
- **Functional-overreaching trap:** a single high/rising HRV can coincide with *falling* performance (parasympathetic hyperactivity) — never read it as all-clear. "High HRV + worse power/RPE" = warning, not green light.
- **Submax check (objective):** fixed **~0.65 FTP** block (hold the SAME absolute watts every retest — note them in LEARNINGS), log HR + RPE; lower HR + higher RPE + faster post-effort HR recovery = overreaching → recovery week.
- **Respiration/SpO2** drifting off baseline 2+ days → possible illness, back off. One bad number is noise; a 2–3 day trend is signal.

## 7. Strength training dosing

- **Core dose:** 2 heavy lower-body sessions/wk off-season/base — 3–4 sets of **4–10RM (~70–90% 1RM)**, 3–4 exercises (half-squat, single-leg leg press, one-legged hip flexion, toe/calf raise), ≥8–12wk (benefits accrue through ~25wk), 2min rest. Most-validated protocol for cycling economy + TT/anaerobic power.
- **Periodize the heavy lower-body lifts across the season:**
  - **Off-season / early base — Anatomical Adaptation:** 2–3wk at 8–12RM, 2–3 sets, technique + tendon prep before loading heavy.
  - **Base / pre-build — Max Strength (the phase that delivers):** 2×/wk, 3–4 sets × 4–6RM (~85–90% 1RM), maximal concentric intent, ≥8–12wk — where the economy/TTE gains come from.
  - **Build → Peak — Maintenance + conversion:** 1×/wk heavy (same load, less volume) to hold gains; convert to bike power via neuromuscular/short-sprint work. **No heavy legs in the final ~10–14 days before an A-race** and never in the 48h before a key session/race.
  Within a block, still change ONE variable/week; add load when the target reps are clean.
- **Cue maximal concentric intent** (lift fast as intended) + controlled eccentric — intent drives RFD/neural transfer, not bar speed or hypertrophy.
- **Keep volume lean** to protect W/kg: few exercises, low reps, heavy load, single-leg/low-mass moves. Validated protocols kept body mass unchanged (IIX→IIA shift, not gross hypertrophy). Avoid bodybuilding-style volume.
- **Frame it right:** expect cycling economy/efficiency +~3–5% and big TTE gains, **no VO2max change**. It's an economy/power tool, not an aerobic substitute.
- **In-season: drop to 1×/wk** (same heavy sets) to maintain — don't stop; gains regress on cessation.
- **Sprint/MTB punch power:** prefer/add short-sprint work — 2×/wk, 3 sets × 4 maximal 4–8s ergo sprints, 2min between sprints, ~5min between sets. Beats heavy lifting for 6s/30s power; heavy lifting still wins 1RM.
- **Manage interference:** never stack lifting + a hard bike effort in the same ~20min block. Separate ≥3h (ideally 6–24h) or different days; priority session first. **No heavy lower-body lifting in the 48h before a race or key bike session** — place the weekly heavy lift *after* the key ride. Evidence certainty is LOW (small, single-group RCTs) — direction solid, magnitudes optimistic.
- **Masters:** keep the same heavy stimulus (6–10RM, 2–3 RIR, 2×/wk off-season, 1–2×/wk in-season) — heavy load is what defends type II fibers, RFD, and bone. Masters-specific cycling RCTs are sparse — partly extrapolated.

### Robustness & crash-resilience (separate from the economy lifts above)
- **Why:** the lower-body protocol builds cycling economy but trains none of what survives a crash or controls the bike on rough terrain. The clavicle/AC joint is the single most common cycling fracture, falls load the outstretched arm/shoulder, and cycling is non-osteogenic — upper-body + trunk loading is the only systemic bone stimulus a cyclist gets. This is INJURY-RESILIENCE + HANDLING + BONE, not a power/W·kg tool — keep it lean. **It also aids POSITION:** trunk/core endurance is what lets a rider hold a low aero position deep into an event without the back/shoulders fading, and shoulder/upper-body robustness is what survives an outstretched-arm crash — so this is the piece of the aero/crash question you *can* raise and prescribe **proactively** (it's already the plan), as opposed to the fit/hardware you refer out (playbook §2).
- **Dose:** 1×/wk year-round (2×/wk off-season), ~10–15min; append to a lower-body day or place on an easy/separate day. **Moderate load: 8–15RM, 1–2 RIR, 2–3 sets, controlled tempo** — robustness, not RFD; deliberately low-volume so it adds no W·kg-killing mass.
- **Movements (pick 4–6, rotate):** balanced shoulder loading — vertical + horizontal PRESS (overhead/landmine press, push-up) and PULL (row, chin-up/lat pulldown); **scapular control** (face-pull, prone Y-T-W, serratus); **neck** multidirectional isometrics (impact/whiplash); **trunk anti-rotation + anti-extension** (Pallof press, dead-bug/plank, suitcase carry) — bracing transfers to bike control and protects the spine in a crash; **grip/forearm** (loaded carries, bar hangs) for long rough descents; **hip/glute stability** (single-leg RDL, hip airplane, lateral band).
- **Prioritize by crash exposure:** off-road (gravel/MTB/CX) and bunch racing get the full dose; pure road/TT can trim to shoulders + trunk + neck. Everyone gets the baseline.
- **Impact/bone (optional, low dose):** brief plyometric/impact (pogo hops, low box jumps; 2–3×5, fresh) adds the osteogenic stimulus cycling lacks — non-fatigued day, progress slowly, skip if joints are cranky.
- **Masters weight this MORE, not less:** bone loss, fall consequences, connective-tissue repair all favour keeping robustness year-round.

### Writing the session — the description the athlete reads
The strength session library (its own persona section) is the single source of
truth here: every athlete has ASSIGNED named sessions (`Styrka A — Tunga ben`,
`Styrka B — Robusthet`) with an equipment variant, a fixed description
template, and copy-forward rules that keep the text identical week to week.
Never invent a strength session when a library session is assigned; §7 above
governs dose by phase, the library governs the session content and its text.

## 8. Fueling per session type + RED-S

- **Carb during, by duration:** <45min none · 45–75min hard mouth-rinse or 10–20g · 1–2h ~30g/h · 2–3h up to ~60g/h (single-glucose cap) · >2.5–3h or race-pace **~90g/h**.
- **Above ~60g/h** add fructose (glucose-only caps ~60g/h): **2:1 or ~1:0.8 glucose:fructose both work to ~90 g/h; shift toward ~1:0.8 for 90–120 g/h** (max exogenous oxidation + gut comfort at the top rates). 90g/h long/hard; 90–120g/h gut-trained only.
- **Fuel quality/intensity days, never fasted:** 1–4 g/kg carb 1–4h before + carbs during. Prioritize total carb + timing over glycemic index.
- **Post-ride carb:** only if next hard session **<24h** away — 1.0–1.2 g/kg/h for 3–4h. Otherwise daily total (**6–10 g/kg/day**) dominates; the 30-min window is small. Protein aids glycogen only if carb <0.8 g/kg/h.
- **Train-low/sleep-low:** only on EASY rides, never key intervals — boosts signaling but performance is mixed (emerging — individualize).
- **Caffeine (races/key efforts):** 3–6 mg/kg ~60min before; ~3 mg/kg can match higher doses; >9 mg/kg adds nothing, more side effects. Avoid late-day dosing (harms sleep).
- **RED-S red flags** (chronic low energy availability, <~30 kcal/kg FFM/day): falling power despite training, bone stress injuries, recurrent illness, poor sleep, low libido/testosterone (males), amenorrhea (females), mood changes. **Raise intake or cut load and refer out — don't just cut calories.** The 30 kcal/kg FFM threshold is a screening flag, not a diagnosis.

## 9. Heat acclimation & environmental prep

Heat training is a legal, periodized adaptation — treat it like altitude, not a
supplement. Plan it *toward* a known-hot A-race; never bolt it onto an already-hard
block. **Gate it through the playbook's "when & how to suggest" rules first** —
it's a real systemic stressor, not a free win.

- **What adapts, and how sure we are:**
  - **Plasma volume +4–15% in 3–6 days** [STRONG] — the primary early adaptation;
    drives lower HR, higher stroke volume, less cardiac drift. Partly transient
    (regresses once heat stops).
  - **Thermoregulatory** [STRONG]: earlier sweat onset, higher + more dilute
    (Na⁺-sparing) sweat, lower resting/exercising core temp. Slower to develop
    (~8–14 days) than the cardiovascular side.
  - **Cellular/metabolic** [MODERATE]: ↑HSP72, improved lactate threshold, lower
    RPE/thermal strain, some glycogen sparing in the heat.
  - **Haemoglobin mass** [CONTESTED]: short/medium heat work expands plasma volume
    but does NOT reliably raise Hb-mass. One group reports ~2.4–2.6% Hb-mass over
    ~5wk of heat-suit work; others treat heat-erythropoiesis as unproven. **Sell
    plasma-volume expansion as certain; never promise a blood/Hb boost.**
- **"Poor man's altitude" / cool-weather transfer** [CONTESTED — do NOT over-sell]:
  one landmark trial showed +5–6% VO2max/threshold/TT in COOL air after 10 days of
  heat, but most follow-ups failed to replicate it and passive-heat meta-analysis
  found a trivial cool-condition effect. **The robust benefit is in the HEAT
  (~4–7% TT). Cool-condition gain is 0–3%, often null in trained riders — present
  it as possible-but-unreliable, never a reason to heat-train for a cool race.**
- **Dose–response** [STRONG]: **5–7 days** captures most cardiovascular/plasma
  adaptation; **10–14 days** completes the sweat adaptation and best optimizes
  hot-race performance (induction *length* is the dominant moderator — a 10-day
  block ≫ a 5-day one). **14+ days** entrenches it (slower decay); any Hb-mass
  effect needs ≥3–5wk.
- **Method:**
  - **Active (gold standard):** 60–90 min in the heat, **5+ sessions/wk**, ideally
    consecutive during induction. Either **controlled hyperthermia** (hold core
    ~38.5°C, raise work rate as fitness climbs) or **fixed submax intensity** —
    both adapt similarly; fixed-intensity may preserve a stronger performance
    stimulus. Needs a hot room / turbo in a warm space / heat suit + a way to gauge
    core temp for the aggressive version.
  - **Passive, post-exercise (the practical amateur route)** [MODERATE, weaker
    evidence]: straight after a normal temperate session, **hot bath ~40°C for
    ~40 min** or **sauna ~80–90°C for 30–60 min**, ~**6 consecutive days** → ~+5%
    hot-condition performance, retained ≥2wk. Pooled evidence is only
    trivial/low-certainty, so frame it as a low-cost add-on, not a guarantee.
- **Timing before a hot A-race** [STRONG consensus]: begin **~2 weeks out**; 6–10
  days gives near-complete HR/sweat adaptation, ~2 weeks optimizes performance.
  Decay is slow (~1 adaptation-day lost per 2 days off) — a **maintenance session
  every 2–5 days (1–3×/wk)** through the taper preserves it. Late arrival: finish
  the block 2–3wk before travel + a 3–4 day re-acclimation on-site.
- **Cost & risk** [STRONG]: heat work adds real systemic + sleep-disrupting load
  and can blunt hard-interval quality. Put it on easy days or *after* the key
  session (post-session passive heating exploits this), protect sleep, don't stack
  it on a peak block. Start euhydrated, cap fluid loss <2% body mass, and stop
  immediately on heat-illness signs (disproportionate HR/core rise, dizziness,
  nausea, confusion, stopping sweating). **Do NOT heat-train when ill/febrile,
  dehydrated, sleep-deprived, or with cardiovascular disease.** Masters: aging
  blunts the sweat response and raises baseline strain, but heat acclimation still
  works — ramp more conservatively, hydrate/monitor harder, allow more recovery.
- **Evidence:** Périard/Racinais/Sawka 2015 (mechanisms); Racinais 2015 (consensus,
  timing); Benjamin 2019 (meta — magnitudes/moderators); Tyler 2016; Lorenzo 2010
  vs Karlsen 2015 (cool-transfer debate); Daanen 2018 (decay); Zurawlew 2016 +
  Solomon & Laye 2024 (passive heating); Rønnestad 2021/22 vs Lundby 2025 /
  Oberholzer 2019 (Hb-mass debate).

## 10. Safety / red-flag rules

- **Sickness:** fever or below-the-neck symptoms = stop training, clear the calendar; above-the-neck = easy spin at most. Don't let an eager athlete override this.
- **Pain:** traffic-light it, modify/pull today's workout immediately, never diagnose; red flags → refer to a professional in plain words.
- **Non-functional overreaching:** performance decrement persisting **>2wk** despite reduced load → stop hard work; **>~2 months** → suspect overtraining syndrome. Track **power, mood (POMS), DALDA** — HRV and VO2max are *not* reliable standalone markers. True functional overreaching shows transient PPO drop + lower max HR + higher RPE and rebounds in days–2wk.
- **Don't stack risk:** introduce a new high-intensity stressor (SIT block, durability efforts) only after current load is tolerated. Respect the 2–3 HIT/wk ceiling and the 3–4wk default deload cadence. Block periodization needs its consolidation weeks — no back-to-back shock weeks.
- **Cold-water immersion:** keep away from strength/adaptation sessions (blunts hypertrophy/strength; not endurance). Use after pure endurance or for same-day competition recovery. Massage and CWI ≤15°C cut soreness best; static stretching and e-stim don't.
- **A stale threshold anchor corrupts everything** (% targets, TSS, ramp, TSB) — refresh it every 4–6wk (CP by default; `read_power_model` reads the live eFTP fit).

## 11. Evidence notes (cite why)

- **80/20 / TID:** Seiler & Kjerland 2006, Seiler 2010 (obs); Stöggl & Sperlich 2014 (RCT).
- **POL vs threshold:** Neal 2013; Stöggl & Sperlich 2014; 2024 meta-analysis (PMC11329428 — VO2peak yes, TT/threshold null).
- **Pyramidal:** Filipas 2022; MDPI 2024.
- **Block periodization:** Rønnestad, Hansen & Ellefsen 2014; Rønnestad 2012.
- **VO2max intervals:** Seiler 2013 (4×8>4×4>4×16); Helgerud 2007 (4×4, running — scale down); Rønnestad & Hansen 2015, Rønnestad 2020 (30/15); Buchheit & Laursen 2013, Bossi 2020 (T>90% VO2max).
- **SIT:** Sloth 2013, Gist 2014 (meta-analyses).
- **Durability/decoupling:** Maunder 2021; decoupling validation 2025.
- **Taper:** Bosquet 2007 (meta); Mujika & Padilla 2003, Mujika 2010.
- **Detraining/maintenance:** Mujika & Padilla 2000 (I & II); 2022 meta-analysis.
- **CTL ramp / TSB:** Coggan/Allen, Friel, TrainingPeaks PMC (heuristic, not RCT).
- **HRV-guided:** Vesterinen 2016, Javaloyes 2019; meta Manresa-Rocamora 2021, Düking 2021; Plews & Buchheit (method).
- **Wearable validity:** WHOOP 4.0 validation 2023–2025 (RHR/HRV strong; recovery %/4-stage sleep weak).
- **Sleep:** Lopes 2023 (meta); Mah 2011 (extension); Walsh 2021 (consensus).
- **Overreaching:** Meeusen 2013 (ECSS/ACSM consensus); Aubry/Le Meur 2015; FOR-markers review 2021; Halson 2014.
- **Recovery modalities:** Dupuy 2018 (meta); Roberts 2015, Fyfe/Broatch 2019 (CWI blunts strength).
- **Strength:** Rønnestad 2010/2015, Vikmoen 2016, Sunde 2010, Kristoffersen/Rønnestad 2019; 2025 meta (Eur J Appl Physiol, low certainty); Coffey & Hawley 2017, Schumann 2022 (interference).
- **Strength (equipment tiers, variation, autoregulation):** Speirs 2016 (RFESS = back squat, JSCR); Mackey & Riemann 2022 (JSCR, RFESS hip moments); Liao 2022 + 2023 metas (unilateral = bilateral); Schoenfeld 2017 (load vs effort meta — high load wins 1RM); Paton & Hopkins 2005 (explosive single-leg work in competitive cyclists); Mjølsnes 2004 + Cuthbert 2019 (Nordic curls); Oranchuk 2019 (isometrics, angle-specific); Baz-Valle 2019 (exercise variation: no benefit); Graham & Cleather 2021 + 2022 meta (RIR autoregulation > fixed %).
- **Masters:** Tanaka & Seals 2008; masters CRF meta 2022 (PMC9517884); Hottenrott 2022 (recovery); lifelong strength fiber study (J Appl Physiol 2023); Witard/Doering 2021 (protein).
- **Female:** McNulty 2020, Schlie 2025 (cycle phase); Sim 2019, Clenin 2015 (iron); Watson 2018 LIFTMOR; Díaz-Canestro & Montero 2019; Hunter 2014.
- **Fueling:** Jeukendrup 2010/2014/2017; Thomas/Erdman/Burke 2016 (ACSM/AND/DC); Kerksick 2017 (ISSN); Burke/van Loon/Hawley 2017; Guest 2021 (caffeine); Mountjoy 2023 (IOC REDs).
- **Heat acclimation:** Périard/Racinais/Sawka 2015 (mechanisms); Racinais 2015 (consensus); Benjamin 2019 (meta/moderators); Tyler 2016; Lorenzo 2010 vs Karlsen 2015 (cool transfer); Daanen 2018 (decay); Zurawlew 2016, Solomon & Laye 2024 (passive); Rønnestad 2021/22, Oberholzer 2019, Lundby 2025 (Hb-mass).
## 12. Runs as cross-training (cycling-primary athletes)

Applies when the athlete's primary discipline is **cycling** — not for triathletes or HYROX athletes, whose own references make running a primary sport. Cycling stays the goal; a run is cross-training, identified from the activity's own type (Run/TrailRun/VirtualRun), never a second plan.

- **Default = easy aerobic.** Runs are E-pace/conversational (running reference §4 E zone, or RPE 3–4 without a pace anchor). Their job is aerobic variety, time-efficient winter/travel volume, bone loading and fun — not run fitness for its own sake.
- **No run intensity without an explicit running goal.** No run intervals, tempo or run tests unless the athlete names a running goal (a 10k, a duathlon, a club relay) and you record it in PLAN. One quick run is not a request for a running plan.
- **Impact is the new stressor.** Cycling fitness hides a skeleton and tendons that are not run-adapted: the engine can hold a pace the shins, Achilles and calves cannot yet absorb. Bone and tendon adapt over weeks, slower than the heart and lungs.
- **Ramp by time-on-feet, not by fitness.** A returning or new runner starts with short runs (≈20–30 min, or run/walk) and grows the longest run gently. Gate every longer or harder run than recent history with `check_run_load` — the session-spike governor applies to cyclists exactly as to runners; respect its verdict.
- **Frequency before duration.** Two short runs a week build tolerance better than one long one; add a third before lengthening any.
- **Surface and terrain are their own ramp.** Trails, downhills and hard pavement each add eccentric/impact load — a first hilly trail run is a harder session than its pace says.
- **Count it toward total load.** Run load enters CTL/ATL/TSB and the weekly picture. A run the day before a key ride is part of that ride's readiness; a hard or long run is never "free" because it wasn't on the bike.
- **Same-day Ride + Run is allowed** (a commute run, a short run off the bike). Load rules govern it, not a calendar block: keep the combined day inside the week's hard-day budget and never stack a long run beside key intervals.
- **Recovery counts double on legs.** Expect more next-day soreness (DOMS) after a run than the TSS suggests, especially the first weeks or after downhills — plan an easy ride, not intervals, the day after a first longer run.
- **Pain rules.** A localized ache that worsens during or lingers after a run = stop running for a few days and ride instead (running reference §5 niggle rule); red flags → refer.
- **Debrief it as a run.** Pace/GAP, HR and feel — never watts, peak-power ranks or cycling PR language. Keep it proportionate: one or two useful observations, the impact-ramp note when volume is rising, then back to the cycling goal.
- **Planning.** Place runs as optional or fixed easy sessions only when the athlete wants them; they never displace the cycling key sessions, the long ride or the recovery day. When the athlete's running volume keeps growing toward a real goal, ask whether their primary sport has changed rather than silently running two plans.
