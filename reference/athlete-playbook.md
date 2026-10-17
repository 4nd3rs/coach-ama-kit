# Athlete Playbook — Pro-Coach Protocols

## 0. How to use this file

- Operational playbooks. The science is in `coaching-reference.md` — this is the **what-to-do** when a conversation turns to data review, races, injury, illness, fuel, cross-training, or scope limits. Consult the moment any of those come up.
- Every target is %FTP / per-kg. Convert to watts with THIS athlete's current FTP and weight (`read_athlete_profile`); rebase on retest.
- Numbers here are evidence-based **starting points to test in training**, not laws. Weak/emerging/contested evidence is flagged inline — don't upgrade it to certainty when you talk to the athlete.
- **You are a training-data analyst, not a clinician.** Section 8 governs everything: never diagnose, prescribe meds, or treat — refer out.

## 1. Professional data review

### Weekly analysis checklist (run every weekly re-plan)

1. **Planned vs completed** — volume/TSS and key sessions (`read_weekly_summary`).
2. **Intensity distribution** vs 80/20 target — flag volume clustered just below threshold (grey-zone drift).
3. **Execution quality** of key sessions — target-vs-actual + VI (below).
4. **Load progression** — CTL ramp / chronic-load trend (reference limits).
5. **sRPE load** with monotony & strain (below).
6. **Decoupling & durability** trend (below).
7. **Subjective wellness + wearable recovery** (HRV/RHR/sleep, any tracker).
8. **New eFTP/MMP personal bests.**

Close with **one** clear adjustment for the coming week, in 1–2 messages.
*Synthesis of Foster sRPE, Coggan TSS/CTL, Seiler TID, Leo et al. 2022.*

### Power profiling — four benchmark durations (`read_power_curve`)

| Dur | System | Read |
|---|---|---|
| **5s** | Neuromuscular / sprint peak | phenotype |
| **1min** | Anaerobic capacity | phenotype |
| **5min** | VO2max / max aerobic power | aerobic ceiling |
| **20min** | Threshold → **FTP ≈ 95% of best 20min** | FTP anchor |

Report all four as **W and W/kg** so weaknesses show. *Allen & Coggan; Leo et al. 2022 (strong).*

- **W/kg context (reference scale, NOT targets):** e.g. ~3.8 W/kg ≈ Cat 2–3 / strong amateur. Pro 20-min: ~6.59 W/kg at 90th pct (n=144); Grand Tour GC ~5.8 W/kg on climbs. *Valenzuela/van Erp 2022; Leo 2022. Never present these as goals — weight-behaviour risk.*
- **Phenotype by relative strength across durations, not watts:** sprinter dominates 5s–1min; pursuiter/TT specialist peaks 1–5min (flat); all-rounder balanced; climber/diesel best at 5–20min (highest sustained W/kg). Re-test climbing efforts on real climbs, TT efforts on flat. *Pinot & Grappe 2011 (moderate).*
- **MMP curve underestimates** — it's built from real rides where the athlete rarely went truly maximal. Don't treat a stale point as a ceiling; flag durations with no recent max effort and **prescribe a test** before concluding. *Leo 2022 (moderate).*
- **eFTP/CP cadence:** intervals.icu re-fits eFTP/W'/pMax whenever a new short or ~20-min best lands — treat resets as data, not guaranteed fitness. **Re-confirm with a deliberate benchmark test every 4–6wk**; a formal test's predictive validity decays after ~6 months. *Leo 2022 (moderate).*

### Execution & fatigue signals

- **Variability Index (VI = NP/AP):** steady endurance & TT **1.00–1.06**; road races higher; crits can exceed **1.3**. High VI on a "steady"/SST prescription = rider surged → stimulus ≠ plan. *Coggan (moderate).*
- **Aerobic decoupling (Pw:HR):** on a steady aerobic ride **60–120min**, **<5% = base coping**, **>5% flags base gap OR a confounder** (heat, dehydration, fatigue, under-fuelling — rule out first). Steady sub-threshold only. *Friel; TrainingPeaks. 5% is a practitioner heuristic, not a precise individual cut-off.*
- **Durability:** expect late-ride power decline — pro MMP falls **~1.6–3.0% after 15 kJ/kg**, **~6–10% after 45 kJ/kg**. Periodically compare a 5-min effort **fresh vs after ~1500–2500 kJ**; larger-than-expected drop = durability limiter → train with long rides + late-ride efforts. *van Erp/Valenzuela 2022; Maunder 2021 (emerging — trigger to investigate, not pass/fail).*
- **Interval execution — review per rep, not session average:** acceptance band **mean of each work interval within ±5% of target.** Flag (a) any rep >5% under, (b) downward fade where late reps drop >5% vs first, (c) reps cut short / count reduced. Report which reps failed and whether pacing or fatigue. *Allen & Coggan; Leo 2022 (moderate).*
- **Tool read:** `read_effort_analysis` supplies `plannedExecution` (planned vs completed rep count, target verdict), plus each set's `execution` (rep-power CV, early-vs-late power/HR/cadence, efficiency fade, recoveries). Its `repAverageTimeInTargetPct` credits a whole detected rep when that rep's **average** intensity is inside the target — useful for rep adherence, but never call it second-by-second time-in-zone. An unavailable or ambiguous plan match is unknown, not failure; the athlete's stated structure still wins.

### What to ask the athlete (data the files can't show)

- **sRPE:** single **0–10 (CR-10)** rating **~30min after** each session; **× session minutes = internal load (AU)**. Quantifies non-power activities and cross-checks planned TSS. *Foster 1998/2001; Haddad 2017 (strong).*
- **Monotony = mean daily load / SD of daily load; Strain = weekly load × monotony.** Persistent high monotony + high load precedes illness/maladaptation → prescribe harder hard days, easier easy days, a true rest day. *Foster 1998 (moderate).*
- **RPE-vs-power mismatch = fatigue flag:** RPE up for the same watts, or watts down at the same RPE, across multiple sessions → suspect non-functional overreaching. Corroborate with the stack (rising decoupling, falling durability, low recovery/HRV from their tracker) before cutting load. *(moderate).*
- **Wearable recovery = modifier, not prescription** (any device): red/low recovery + suppressed HRV escalates scrutiny on a hard day; **green alone never overrides a planned rest day or ignores a power decline.** Use 7-day trends vs the rider's own baseline, not single-day absolutes. *(moderate).*

### Compliance metrics (report weekly, act on them)

% prescribed sessions completed · planned vs actual TSS/duration · time-in-zone adherence on key workouts. Flag **chronic under-completion** (under-dosing → stalled adaptation) AND **chronic over-completion** (added intensity → grey-zone drift, rising monotony/strain). *Foster; TrainingPeaks/Coggan (moderate).*

### Reading a ride by discipline (`read_activity` first, always)

VI = NP/avg is the first screen for what a file actually was:

| VI | Reads as |
|---|---|
| 1.00–1.05 | TT / steady trainer / disciplined Z2 |
| 1.05–1.15 | gran fondo, gravel, XCM, hilly endurance |
| 1.1–1.3 | road race |
| 1.2–1.6+ | crit, CX, XCO — surge sports |

- **Average power lies off-road:** MTB average runs ~10%+ below road at the same effort (terrain, traction, body-English the meter never sees) and XCO spends ~27% of race time at zero power coasting. Judge MTB/CX/gravel by **NP, kJ, time>FTP, surge count — never average.** *Granier/Viana 2021; FasCat (strong).*
- **A surge costs more than it looks:** variable efforts burn more glycogen and fatigue more than steady riding at equal average. *NP theory; Theurel & Lepers (strong).*
- **Well-executed by discipline:** XCO = NP near/above FTP with controlled surge fade across laps (a flat low-VI XCO file = soft-pedaled, not an easy course) · XCC = supra-tempo floor + terminal sprint for ~25min · XCE = judge per heat (peak power holding across rounds), whole-day averages are meaningless · XCM/gravel/fondo = the diagnostic is **durability** — final-third NP and decoupling vs first-third, fade + HR drift = under-fueled or over-paced · road race = judge by NP/IF, surge count, late-race MMPs vs fresh (avg is draft-suppressed) · crit = NP/IF near 1.0, sprint count, peak 5–15s; low surge count = sat in (easy day despite "race" label) · TT = VI ≤1.05, positive decoupling late = over-paced start · CX = HR pinned at threshold while running sections put zeros in power — cross-check HR before calling it easy. *Granier 2021; Sanders & van Erp 2021; van Erp 2021 (strong/moderate).*
- **Calibration guard:** a sudden whole-file power shift vs the athlete's norm at matched HR = zero-offset/battery/calibration, not fitness. Verify before trend conclusions. *(strong applied practice).*

### Data hygiene — confirm before judging

Common mislabels: MTB/gravel logged as plain "Ride", indoor as outdoor, commute as training. Signatures: a "Ride" with VI >1.2 + high zero-power fraction is almost certainly MTB/CX/crit; a "race" with VI ~1.0 and no surges was a TT-style ride or a sat-in day; "outdoor" with no GPS and implausibly steady speed = indoor. **When VI, speed-vs-power, decoupling, GPS, or zero-power fraction conflict with the label — ask the athlete what the ride actually was (discipline, indoor/outdoor, race vs training, surface, mechanicals) BEFORE judging execution.** Misreading an MTB race as a weak road ride is the most common analysis error. *(expert-opinion, applied practice).*

## 1b. Assessment — strengths, weaknesses, and testing

Run a full assessment at onboarding, after every test week, and whenever data and athlete self-report disagree. Output = a dated "Strengths & weaknesses" verdict in `USER.md` (template in "Write the verdict" below).

### 1. Data assessment — read the curve

Pull `read_power_curve(90)`. Benchmark **W/kg** at four anchors (Coggan men's table; book compilation, not peer-reviewed — top tiers run high vs pro databases (van Erp/Valenzuela 2022); use for amateur tiering + shape, anchor competitive riders to peer-reviewed norms):

| Tier (men) | 5s | 1min | 5min | FTP |
|---|---|---|---|---|
| Exceptional | 22.2 | 10.4 | 6.6 | 5.5 |
| Excellent | 20.4 | 9.7 | 6.0 | 5.0 |
| Very good | 18.7 | 9.0 | 5.3 | 4.4 |
| **Good (Cat 3)** | 16.6 | 8.2 | 4.6 | **3.8** |
| Moderate | 14.8 | 7.5 | 4.0 | 3.3 |
| Fair | 13.0 | 6.8 | 3.4 | 2.8 |

- A rider near a tier boundary swings tiers on small weight or FTP errors — verify current weight + test protocol (`read_athlete_profile`) before any phenotype claim.
- **Women: never tier against the men's table above.** The table is men's; women's Coggan tiers run materially lower at every anchor (women's threshold ceiling ~**5.69 W/kg** vs the men's higher top). Tier female riders against the **published women's Coggan column** and anchor competitive women to peer-reviewed female norms (Leo et al. 2022 includes women). Phenotype SHAPE-reading below is sex-neutral; only the absolute W/kg cutoffs differ.
- **Read the SHAPE, not just tiers** — connect the four anchors: steep **down-slope** (big 5s–1min, weak FTP) = sprinter · **up-slope** = TT/diesel · **inverted-V** peaking 1–5min = puncheur (big VO2/anaerobic, thin base) · **flat** = all-rounder, no single weapon. Ratios: **5min normally runs ~1.10–1.20×FTP** (it tracks VO2max/MAP, structurally above threshold), so the puncheur bar sits *above* the norm — **5min ≥~1.25×FTP** = puncheur; **5min ≲1.10×FTP** with weak short power = diesel.
- Largest tier-gap across anchors = candidate limiter; smallest = racing strength. **Changes <5% = noise** (15s ICC 0.99, 30s CV 4.5% — Leo/Spragg/Mujika 2022); don't coach on smaller deltas.
- **Durability is a separate fourth axis — never infer it from fresh power.** Operationalize: same max effort fresh vs after **~2000 kJ** (≥1500 kJ preload or the test under-exposes the trait). Fatigued drop **≤6–7% good, ≥12% poor** (emerging — Spragg 2023, Frontiers 2025; thresholds not interchangeable across protocols, pick ONE and hold it). % retained separates riders at matched fresh fitness. Also mine history: `read_activity_intervals` on long rides, compare late-ride vs fresh power at the same duration.
- **Event-demand gap analysis (Friel order):** (1) quantify the target event — durations, % time per zone, surge pattern, total kJ; (2) overlay profile + durability; (3) largest demand-vs-capacity gap on a *race-decisive* duration = priority limiter. Priors (descriptive cohorts — refine against the athlete's own race files): **crit** ~20% of time >120% FTP, ~50% soft-pedaling → W′ + surge repeatability beat raw FTP · **XCO** ~37% time >VT2, surges 5–30s → anaerobic capacity + repeatability · **gran fondo** 4–7h, repeated 10–60min climbs → durability + fueling, not sprint power.

### 2. Conversation assessment — ask, then reconcile

Ask in chat, log answers to `USER.md`:
1. **Where do you get dropped?** (climbs / sprints / after repeated accelerations / late in long rides) → localizes the limiter to a duration band.
2. **What feels easy vs hard?** (steady tempo vs explosive surges) → cross-checks phenotype.
3. **Terrain preference?** (rolling / sustained climbs / flat TT).
4. **How well do you recover between surges?** → repeatability.
5. **When do the legs fade in a long ride/race?** → durability.
Plus: RPE per work interval, rated separately for work vs recovery bouts — captures what the file can't.

**Data ≠ self-report is a red flag — reconcile before prescribing:**
- High FTP but dropped on long climbs → suspect ramp/20min-inflated FTP (high-anaerobic phenotype beats the 0.75/0.95 corrections); true limiter is muscular endurance. Validate with a long TT or eFTP.
- Strong fresh numbers but "legs gone late" → durability gap invisible to fresh tests; confirm with the post-kJ test.
- Profile data >**6 months** old loses predictive validity (Leo 2022) → retest before concluding anything.

### 3. Limiters — taxonomy and prioritization

- Fixed taxonomy (Friel + modern extensions) → diagnostic duration: **aerobic endurance/durability** = long + post-kJ power · **muscular endurance** = 20–60min · **anaerobic endurance** = 1–3min · **sprint** = 5–15s · **repeatability** = decay across repeated max surges · plus force, speed-skills, pacing discipline.
- A limiter is a **race-specific** weakness. A weakness the event never taxes is not a limiter and must not drive the block.
- **Target 1–2 limiters per block. Maintain — don't grow — strengths.** Developing riders fix basic limiters (aerobic endurance, force, muscular endurance) in base; 3+ years of base → work advanced abilities.
- Race to strengths via event *selection*: pick races suiting the phenotype rather than remodeling a weakness the calendar doesn't demand.

### 4. Test battery (schedule each as a structured workout)

Warmup/cooldown bookends per coaching-reference §4 (workout library). **Ask indoors/outdoors EACH test** — it varies seasonally (summer out, winter in). Record the modality on the result (`protocol`). When a retest is a different modality than the last, apply the **~5–10% indoor-lower** correction before calling any change fitness (a winter indoor retest is not a fitness drop).

**Power availability (record it in the dossier: all rides / indoor only / none).** Many athletes have power only on the indoor trainer. Tests and structured %FTP prescriptions still work — run them where the meter is (usually indoors). For their outdoor rides recorded without power, prescribe the same watt targets but voice a feel/RPE anchor alongside, and debrief those rides from duration, HR, route and their RPE — never as "no power data".

**Choosing the test (best fit for THIS athlete):**
1. **Need one at all?** If `read_power_model` eFTP reflects a fresh near-max 3–20min effort **<~6wk** and training naturally has hard efforts → use the model, don't test.
2. **Else pick by can-pace × venue × phenotype/goal:** **CP** is the default (can pace, either venue) · **Ramp** for can't-pace/beginner/quick check (indoor/ERG) · **long TT or post-kJ durability** for diesels or when a ramp/20min looks inflated vs long-climb power · **max sprint** as a Pmax add-on (often free off the power curve) · gravel/XCO → add an intermittent **2×6×40/20** race benchmark alongside the physiology test. Power-cadence/F-V (§7) is an optional one-off only if they ask about cadence/gearing AND have a capable head unit.
3. **Coach RECOMMENDS the best fit** with one line of why; the athlete may override. Keep the **SAME protocol** across retests (switching breaks the trend) — store the anchored protocol in `USER.md`.
4. **The number.** FTP stays the zone anchor: derive it from the test (CP → **~0.96×CP**; ramp → **MAP×~0.72**). **Confirm the new FTP with the athlete** (it rescales every zone), then push it with `write_power_settings` (zones follow). If that returns `needsReconnect`, the athlete hasn't granted settings-write — tell them to tap **"Accept new eFTP"** in intervals and set W′ once, and offer the reconnect link so next time it's automatic. NEVER claim you changed intervals when the tool didn't write.

| Test | Protocol | Measures / validity | Retest |
|---|---|---|---|
| **CP/W′ (default)** | 12 + 3–5min max pair (or 3/7/12min on **separate days**); fit P vs 1/t; `read_power_model` returns the fit | CP, W′, pMax (Karsten 2017); FTP ≈ **0.96×CP** | 8–12wk |
| **Ramp (fallback)** | +steps to failure; FTP = **MAP × ~0.72** (conservative; 72–77% individual); best **indoor/ERG** | Can't-pace / beginner / quick check. Bias-prone: under-rates diesels, over-rates sprinters — cross-check vs eFTP/long TT | fallback |
| **20min (fallback)** | 5min hard opener (clears anaerobic contribution), rest, 20min max even; FTP = **×0.95** | TE ~4.7% vs MLSS — best single-effort proxy | 4–6wk |
| **Long TT (gold, alt)** | 40–60min max steady (Kolie Moore 30–70min) | FTP, best validity (Borszcz 2018); use for diesels or when a ramp looks inflated | 4–6wk (reference §2) |
| **Power profile** | 15s + 1min + 5min max, **longest first, ≥30min between** | Phenotype anchors; <5% = noise | 8–12wk (pair with CP retest) |
| **LTHR** | Solo 30min max TT; LTHR = avg HR of **last 20min** (lap at 10min) | Friel HR zones. Wrist/optical HR (any watch/band) only for steady ≥3–4min — chest strap for sprints/ramps | with the CP/threshold test |
| **Durability** | 20min max fresh (separate day) vs same after **~2000 kJ** Z2 (~3h) | % drop: ≤6–7% good, ≥12% poor (emerging) | 8–12wk (house default), build/peak |
| **LSCT (submax)** | 6/6/3min @ 60/80/90% HRmax + 90s HRR | Weekly fatigue tracker: power, RPE, HRR (Lamberts 2009) | weekly |

**No-test alternatives:** intervals.icu **eFTP/W′/pMax** (read via `read_power_model`) from 3–12min efforts — trust only with a fresh near-max 3–20min effort **within 6wk**. Submax drift: weekly LSCT + the decoupling test (reference §4) + the ~0.65-FTP submax check (reference §6). Treat any field FTP as a **3–6% typical-error estimate**, never one true number (FTP ≉ MLSS ≉ CP — Jeffries 2020).

### 5. Test week template — and when NOT to test

- **D1** power profile (15s/1min/5min) · **D2** Z2 easy · **D3** rest or recovery spin · **D4** the athlete's anchored threshold test (CP 12+3–5min pair by default; 20min/long TT if that's their protocol); take LTHR from the test ride's HR trace (avg HR of the 20min effort — approximation of the Friel 30min protocol; run the standalone 30min TT another week if you need it exact) · **D5** Z2 · **D6** rest · **D7** durability test (**always last** — it wrecks the legs; the fresh leg = D4's 20min result — if D4 was the long TT, add a fresh 20min later or defer durability). Follow with an easy week start. Tests on separate days, **24–48h easy before each**, same modality/venue/time of day.
- **Do NOT test if:** HRV/RHR off baseline (reference §6 gates), any illness, sleep <6h, or last LSCT showed raised HR/RPE. Mini-taper first or defer to eFTP — a fatigued test writes a false FTP into every downstream number.
- A wearable recovery/readiness score is a soft gate only — never let it override measured power in classifying strengths/weaknesses.

### 6. Write the verdict into USER.md

Update the `Strengths & weaknesses` section every assessment, dated, with supporting numbers:

```
## Strengths & weaknesses
- Profile (90d): 5s 13.0 · 1min 7.0 · 5min 4.0 · FTP 3.5 W/kg (280W @ 80kg, from CP test 290W / W′ 18kJ, outdoor)   ← illustrative numbers
- Tiers: 5s Fair+ / 1min Fair+ / 5min Moderate+ / FTP Moderate+→Good — up-slope ⇒ diesel
- Durability: 20min fresh 295W vs post-2000kJ 272W = −7.8% (borderline; protocol: fresh-vs-2000kJ)
- Athlete says: dropped after repeated attacks, fine on long climbs — agrees with data
- Limiters for [event]: (1) repeatability/W′ (2) 1–3min power · Strength: muscular endurance — maintain
- Retests due: CP wk of [date] · profile [date] · LSCT weekly · protocol: CP 12+3min, outdoor
```

State the verdict to the athlete in plain words — one strength, the 1–2 limiters, and what the next block does about them.

### 7. Force/velocity (power–cadence) profile + CP nuances

- **Sprint P/C test:** 4–6 maximal seated sprints of 5–7s from low rolling speed, fixed gear per rep, 2–3 different gears across reps to spread cadence points; only the first ~3–4 crank revolutions count (before metabolic fatigue distorts the profile); **≥5min easy between reps.** Standardize: 10min @80–90rpm warmup + one ~3s primer, same position/crank/trainer every time. Outputs: **Pmax** (W, W/kg) and **optimal cadence Copt**. *Taylor 2023; Dunst 2022 (strong/moderate).*
- **Compute & read:** call `analyze_power_cadence(activityId)` on the deliberate test activity. It fits crank torque–cadence as a line → T0 (torque intercept) and C0 (cadence intercept); **Copt = 0.5×C0, Pmax = T0×C0×(2π/60)/4** when cadence is rpm. Trust/report only `available:true` (the tool enforces ≥3 valid sprints, enough cadence range, a physically valid negative slope and combined R²≥0.95); `available:false` means repeat the protocol, never rescue the numbers by mental fitting. Copt ~110–135rpm (sprinters high, diesels low); expect Pmax ~10–16 W/kg for a non-sprint road athlete. *Driss & Vandewalle 2013; Dunst 2022/24 (strong).*
- **Deficit → prescription:** relative low T0 (spins, no force) = **F0-deficit** → heavy gym strength + low-cadence big-gear work (~40–60rpm seated torque). Relative low C0 (torque, but power dies as cadence rises) = **V0-deficit** → high-cadence spin-ups (130–160rpm) + short overspeed efforts. Transfer of deficit-targeted training to cycling is **plausible-but-emerging — verify with retest.** *Samozino & Morin framework (emerging for cycling).*
- **Never coach everyday cadence toward Copt** — it's a neuromuscular ceiling, not an endurance target (economy-optimal cadence is far lower). *Driss & Vandewalle 2013 (strong).*
- **NM-fatigue monitor:** weekly mini-version — 2–3 standardized 5–6s sprints in a warmup, same gear/protocol. **Pmax >5–10% below rolling baseline** (test noise ~2%) = neuromuscular fatigue flag; **falling Copt** = fast-twitch-specific fatigue. Catches fatigue HRV misses — pair them, don't substitute. *Tofari 2014; Dunst 2024 (moderate/emerging).*
- **CP nuances** (battery row above): prefer **≥3 trials** (e.g. 3/7/12min) — 2-test fits are fragile; the 3-min all-out is convenient but **overestimates CP / underestimates W′** in trained riders and needs 2–3 familiarizations (fit >97% = well-paced). **CP ≈ 4–5% above 60-min power (FTP ≈ 0.96×CP).** W′ bands: road-endurance men ~9–15 kJ, punchy riders ~15–30 kJ; surge budget ≈ W′ ÷ (surge W − CP). *Vanhatalo 2007; Karsten; High North applied (strong/moderate).*
- **Safety:** no maximal sprint/torque testing with unresolved musculotendinous niggles, acute illness, an already-depressed Pmax, cold muscles, or sketchy surfaces — trainer preferred. Masters: longer warmup + inter-rep recovery; keep strength training to preserve the type II pool being measured. *(expert-opinion).*

## 2. Races

### Priority system

- **A** = peak target → taper for it (reference taper). **B** = train through. **C** = training race. The macro plan always points at the next A race.

### Demands by event type — train the decisive effort, not just the duration

| Event | Duration | Decisive effort |
|---|---|---|
| Road race | 2–5h | 15s–5min selections on climbs/crosswinds |
| Criterium | 30–75min | dozens of near-max accelerations out of corners |
| TT | 10–60min | steady threshold |
| Gran fondo | 4–11h | sub-threshold; fuelling + drafting decide |
| XCO | 80–100min | repeated supramaximal surges |
| XCM / marathon MTB | 3–6h | mixed |
| Cyclocross | 40–60min | repeated max efforts + dismounts |
| Track endurance | 10s–~4min | bunch races 40–60km |

*Mujika & Padilla 2001; Lucia 2001; Menaspà 2015; Granier 2018; UCI regs (strong).*

- **Road/crit:** once FTP is adequate, prioritize **repeated-sprint + 1–5min capacity** ("fatigued power") — crit sprints come after ~70–80 prior accelerations. Sessions: **3×(10min tempo + 30s max sprint)**, over-unders. *Menaspà 2015; van Erp 2021 (moderate).*
- **Mass-start off-road (XCO, CX, Cykelvasan blocks):** deliberately **fast start above threshold**, settle within 5–10min — position beats energy saved. Train **2min @130% FTP → 8min @90–95%.** *Granier 2018 (strong).*
- **Drafting is the biggest free watts in any mass-start event:** sitting on a wheel cuts power demand **~30%**, and in the sheltered middle of a big bunch drag falls to **5–10% of solo (~90% reduction)** — worth **50–100+ W** at Vätternrundan, more than any equipment. Coach the tactic: sit ~5–15 riders back on the sheltered side (near the front avoids the accordion surges at the back that cost more than the draft saves); in a crosswind the shelter is diagonal — get to the leeward side before the echelon forms or you're in the gutter and gone. Require demonstrated group skills first (crash risk). *Kyle 1979; Blocken 2018 (strong).*
- **Discipline training emphasis:** XCO = race-start max efforts (30–60s all-out from rolling), 30/15-40/20 supra-threshold repeats, 1–3min VO2 work with technical skills under fatigue (anaerobic power correlates r≈−0.79 with placing) · XCC = crit-on-dirt: repeated 1–5min at race density + finishing sprint · XCE = maximal 30–60s anaerobic reps with short recovery + standing starts · XCM = durability (threshold late in long rides) + climbing tempo + fueling rehearsal — a durable high threshold beats top-end W' · gravel = long tempo/SST durability, very long Z2, 90+ g/h gut training · CX = repeated 2–4min over-FTP, 30/30s, start efforts, skills under fatigue. *Impellizzeri & Marcora 2007; Inoue 2016/2018; Granier 2021 (strong/moderate).*

### Pacing by event type

- **TT:** near-even **95–105% FTP** for 40km (shorter = higher %), vary **±5–10%** (harder on climbs/headwind, easier on descents/tailwind). **Never** start above target in the first 2–3min — the classic amateur blowup is 110–120% for 5min then fade. *Atkinson 2000/2007; Abbiss & Laursen 2008 (strong).*
- **Ultra (Vätternrundan 315km, Styrkeprøven):** hard power **cap**, not a target — **IF 0.60–0.72 (e.g. ≈185–225W normalized at a 310W FTP)**, never surge above ~FTP even on hills. First 100km should feel too easy; finish time is decided by fuelling + group riding, not early fitness. *Abbiss & Laursen 2008; Jeukendrup (moderate).*
- **Two pacing upgrades that fix the common amateur error:** (1) even *effort* on the flat, but **variable power on gradients** — a bit harder into climbs/headwinds, ease on descents/tailwinds; beats constant power by ~1–3% on undulating courses (time is nonlinear in speed). (2) For any effort >~4min, a **slightly conservative first quarter** (start ~2–5% under target, finish at/above) beats a fast start, which spikes early lactate and forces a bigger fade. Surges are expensive — NP is a 4th-power average, so letting VI drift 1.0→1.1 at the same average power costs ~5–8% more. *Atkinson 2007; Abbiss & Laursen 2008 (strong).*

### Bike-handling skills — train them, don't just describe them

Skills are trainable and prescribable, not just describable — and off-road they're often more decisive than watts (XCO first-lap position correlates **r≈0.91** with final placing; skilled riders brake later and carry speed, then need less power on the next climb). Put skills on the plan the way you put intervals on it. *Motor-learning + XCO/skills literature (moderate; discipline-specific handling is largely practitioner-consensus).*

**Reactive, not nagging (covers all of §2's bike / aero / position / crank material):** program skills sessions when the athlete's discipline clearly needs them — an XCO racer bleeding time in corners is a training gap like any other — but don't push aero tweaks, crank length, position changes or equipment on anyone unprompted. When an athlete asks or wants to go deep, engage and give the real specifics here, never a vague brush-off. The one thing you raise proactively is the **strength that supports position-holding and crash-robustness** (coaching-reference §7) — it's already in the plan.

- **How to prescribe any skill (the backbone):** isolate the sub-skill slow → add speed → add variability (vary the drill/line) → add race-reality (fatigue + other riders + unknown lines). Cue the *effect on the environment*, not the body part ("look to the exit / drive the tyre into the dirt", not "bend your elbow"). Novices need more repetition first, then randomise. Program skills on FRESH legs to learn, plus some reps UNDER fatigue (end of a hard ride) — that's where races are lost.
- **The remote-coach boundary:** you prescribe the sessions, drills, progressions and cues, and review the athlete's **video** of a drill as async feedback. Refer to a hands-on skills clinic for the three cases video can't fix: (1) a skill the rider can't do at all yet (first drop/jump/remount), (2) an ingrained fault they can't self-perceive, (3) high-consequence real-time correction (fast descending). "Follow a confident descender and match their lines" is a legitimate prescribed drill.
- **By discipline (drill families to prescribe):**
  - **MTB (XCO/marathon):** attack position (level pedals, hinged hips, heavy feet/light hands); cornering (figure-8 on grass → berm reps outside-in-out, eyes to exit → switchbacks slow-then-fast); braking ("finish braking before the corner" markers → trail-braking); rock gardens/roots (walk it → slowest ride-able speed, momentum > brakes → repeat one line → vary under fatigue); drops (curb-height → progress); technical re-starts from a stop on a gradient (huge after bottlenecks); pump-track for momentum.
  - **Cyclocross:** dismount/remount broken into leg-swing / shoulder-lift / step-through / remount — 2×10 slow → faster → under fatigue; barriers (~40cm, ~4m apart); run-ups/shouldering; sand, off-camber and ruts (commit + look); loose-corner reps.
  - **Gravel:** the headline is durability + fuelling (train those), plus loose/washboard cornering and descending-on-marbles (same brake-before / look-to-exit family), reading the line, and bunch-on-gravel positioning before pinch-points (climbs, singletrack).
  - **Road / crit:** corner-and-reaccelerate reps (corner at speed → 5–10s sprint → settle, ×8–12) — trains the skill AND the exact energy system; positioning drills (move up on the sheltered side without a big effort); sprint/leadout technique; crosswind/echelon group sessions (learn the gutter).
  - **Descending (all):** the four pillars — vision (look to the exit), braking (upright, before the corner), line (outside-in-out, late apex on blind corners), body (outside pedal down, weight low, relaxed grip). Prescribe repeated laps of one safe descent, one focus per rep.
  - **Starts (XCO/CX/crit — outsized effect):** standing-start reps (gear choice, clip-in speed, 15–30s all-out then settle) + "hard-start" intervals (30–60s max → settle to threshold) to train recovering after redlining off the line.
- **Cadence & gearing (how you ride, not what you buy):** self-selected ~85–100 rpm suits most — a higher cadence trades a little O₂ for much less leg fatigue (better durability); a big gear / low cadence is a strength-endurance *stimulus*, not a way to race. Coach the principle: carry enough **gear range to hold your target cadence at target power on the event's steepest sustained climb** (grinding <~60 rpm burns the legs early). The specific cassette/chainring / 1×-vs-2× is a mechanic's spec — you set the cadence target, they pick the parts.

### Swedish / Nordic targets (verified June 2026 — RE-VERIFY on organizer sites before advising; logistics change yearly)

- **Vätternrundan** 315km around Lake Vättern, start/finish Motala, mid-June, ~9 depots. **Halvvättern** 150km. **Tjejvättern** ~100km (women). Motionslopp — start-group seeding by prior results.
- **Cykelvasan 94** Sälen→Mora, August, on the Vasaloppet trail: ~87km forest road/gravel + ~7km asphalt per the organizer (fast, low-tech; avg finish ~5h22min). **Cykelvasan 45/30** from Oxberg.
- **MTB Lidingöloppet** ~30km, September. **Långloppscupen** = national XCM series (Billingeracet, Lida Loop, Ränneslättsturen, Engelbrektsturen) and Cykelvasan seeding races.
- **Birkebeinerrittet** 84–86km MTB Rena→Lillehammer, late August (long opening climb). **Styrkeprøven** ("Trondheim–Oslo") ~540km June ultra. **Nordic Gravel Series** incl. Evertsberg Gravel 56/102/159km.
- **Racing structure:** real racing needs an **SCF license**; a 40+ amateur races **Masters** classes (H30/H40…) on a Master license; **Sportmotion** accepts a motion license or **engångslicens** bought at the race. Lowest-friction entry = Sportmotion or Masters via local club. *Organizer sites + scf.se (strong).*

### Bike choice (coach-level, not shop-level)

Vätternrundan/Halvvättern = road, 28mm. Cykelvasan / Birkebeinerrittet = **XC hardtail** is default/fastest (full-suss unnecessary; check current bike rules). Gravel events = 38–45mm. XCO/Lidingöloppet = XC MTB. CX = 33mm. **Most versatile single bike for a Swedish amateur = a gravel bike.** *Organizer surface data; rolling-resistance lab data (expert-opinion).*

- **Aero rule of thumb:** above ~30 km/h, ~90% of power fights air, and the **body is 70–80% of drag.** Cost-effectiveness order: tight clothing → lower/narrower trained position → aero helmet → wheels/frame last. Clip-on aero bars TT-only and **banned in mass-start road races** — verify Vätternrundan's current rules. *Martin 1998; Crouch 2017 (strong).*
- **Position is the biggest aero lever, and it's trainable:** since the body is ~70–80% of drag, the target isn't the lowest CdA — it's the **most aero position the athlete can hold and still make power for the event's duration**. Get there by *adapting into it*: progressive time-in-position, mobility (hip flexors, hamstrings, thoracic), and testing sustainable power IN the race position (not just upright); cue narrow elbows, relaxed shoulders, flatter back. The exact bar/pad/saddle numbers are a fitter's job — you coach holding and powering the position. *Fintelman 2015; Crouch 2017 (moderate/strong).*
- **Fit stays coach-level:** saddle height ≈ 25–35° knee flexion at BDC; rider can hold drops/hoods for event duration. Any numbness/knee pain/saddle sores → stop chat-tuning, refer to a pro fitter (§3). *Bini 2011 (moderate).*
- **Crank length — set expectations, don't spec it:** strong evidence it barely changes sustainable power or efficiency across ~150–180mm — there are no free watts in a crank swap. Riders change it for hip/knee comfort or to **open the hip angle for a lower, more aero position** (the real reason pros run 160–165mm), not power. If an athlete asks "should I go shorter?", give that honest read and flag it as worth exploring with a fitter — never prescribe the length. *Martin & Spirduso 2001; Barratt 2016 (strong for the no-power-effect).*

### Race week

- **Taper (A-event):** cut **volume 40–60% over 1–2wk**, hold intensity + frequency → ~1–3% gain (full rules in reference). **One-day mid-season event:** 5–7 day mini-taper, normal week minus ~40% volume, last hard session 3–4 days out. *Bosquet 2007; Mujika & Padilla 2003 (strong).*
- **Openers (day before):** 45–90min easy + **3–4×60–90s builds to race pace + 2–3×10s sprints**, full recovery, <5min above threshold. Long events (Vätternrundan): 30–45min easy spin suffices. *Bailey 2009 + established practice (expert-opinion).*
- **Carb-load (events >90min):** **10–12 g/kg/day for 36–48h pre** — rice, pasta, juice, white bread, sports drink; cut fat/fibre. One day at 10 g/kg is enough if trained. *Thomas/Erdman/Burke 2016; Bussau 2002 (strong).*
- **Checklist:** 7d out last big session · 3–4d last short quality · 2d rest/easy + start carb-load · 1d openers + logistics (bike check, drop bags, start-group time) · race morning wake ~3h before, meal 3h before, warm up per event. **Nothing new on race day** — food, gear, position, clothing all pre-tested.

### Race-day fuelling timeline

- **Pre-race meal:** **1–4 g/kg CHO, 1–4h before** (default ~250g, 3h out, low fibre/fat).
- **During:** 30–60 g/h for 1–2.5h events; **up to 90 g/h** for >2.5h (Vätternrundan, Cykelvasan) using **glucose:fructose 2:1 (or ~1:0.8 — both validated to ~90 g/h; ~1:0.8 above that)**, gut-trained only. Convert in chat: 90 g/h ≈ **3 gels or 2 bottles of 45g mix per hour.** Plan depot stops in advance.
- **Hydration:** 0.4–0.8 L/h scaled to heat/sweat; add sodium **~300–600 mg/h for events >4–5h.** Warn against overdrinking plain water in cool Swedish June (hyponatremia in 10h+ riders). *Sawka 2007; Hew-Butler 2015 (strong).*
- **Caffeine:** 3–6 mg/kg 45–60min before the **decisive** part; on long events dose late (final ~2h), not at a 04:30 start. *Ganio 2009; Maughan 2018 (strong).*
- **Warmup by type:** short/intense (TT, crit, XCO, CX) = 20–30min progressive ending with 2–3 race-pace/sprint efforts, finish within ~10min of start; long events = roll out easy, first 30–60min is the warmup. *McGowan 2015; Tomaras & MacIntosh 2011 (strong).*

## 3. Injury playbook

### Pain traffic light (ask for a 0–10)

- **GREEN 0–2** (aware of it, doesn't change pedalling) → train, monitor daily.
- **AMBER 3–5** → ride modified: **Z1–Z2, cut volume ~30–50%, avoid the aggravating posture** (big-gear low-cadence for knees, long TT position for back).
- **RED >5** at any point, OR pain that alters pedalling, OR worse next morning, OR a week-on-week worsening trend → **stop the session, rest/cross-train** until back to green/amber.

**Next-morning rule:** after any amber ride, ask next morning "back to baseline?" Worse at 24h = load too high → cut next session a step. **Two failed morning checks = pause riding + book a fysioterapeut.** *Silbernagel 2007 RCT (strong).*

**Prioritize knee + back** in check-ins — pro 12-mo prevalence **58% lower back, 36% anterior knee**; of time-loss injuries **57% knee, 22% back.** The check ("Any niggles — knees, back, hands, saddle area?") is not a fixed weekly line. Ask it when there is an active issue or new data (a reported ache, a feel/RPE flag, a cut-short session, a bike or position change), and never when the athlete has asked to raise issues themselves. *Clarsen 2010 (strong).*

### Per-injury: cause → modify

| Injury | Bike-fit / training cause | Modify |
|---|---|---|
| **Anterior knee / PFP** | saddle too LOW or FORWARD; recent big-gear/climbing jump; cleat. Target **25–35° knee flexion at BDC (25–30° sweet spot)** | raise saddle **3–5mm** steps, spin **90+**, avoid big-gear intervals while symptomatic. *Bini 2011; Holmes 1994 (moderate)* |
| **Lateral knee / ITB** (also posterior knee) | saddle too HIGH; cleats over-internally-rotated; low float; narrow stance | lower saddle 3–5mm, neutral-to-slightly-toes-out cleats with float, ride below symptom-onset time. *Holmes 1993 (expert-opinion)* |
| **Lower back** | excess saddle-bar drop/reach; long aero/TT; sudden volume; weak trunk endurance | shorten longest ride, **stand 10–20s every 10min**, temporarily raise bars/shorten stem, trunk work 2×/wk. Keep riding green/amber (movement > rest for non-specific LBP). *Clarsen 2010; Marsden 2010 (moderate)* |
| **Saddle sores** | friction; bib hygiene; saddle level/height | chafing → ride on (clean bibs every ride, chamois cream, shower + change immediately). Painful raised lesion → 24–72h off / pain-free cross-train. **Never lance, never antibiotics.** *Leibovitch 2005 (expert-opinion)* |
| **Perineal numbness** | saddle tilt (nose-up common), no cut-out, height/setback, aero time | stand 20–30s immediately; level saddle, consider cut-out. *Leibovitch 2005; Sommer 2010 (moderate)* |
| **Hand numbness (cyclist's palsy)** | bar pressure; long reach; saddle nose-down | change position often, padded gloves/double tape, neutral wrist, raise bars. AMBER = resolves 24–48h. *Patterson 2003 (moderate)* |
| **Neck** | bars too low/far; aero; new helmet/eyewear | raise stem/shorten reach, shrug + chin-tuck breaks every 10–15min. *Asplund 2005 (expert-opinion)* |
| **Achilles** | saddle too HIGH (toes-down), cleats too FORWARD; sudden climbing/running | cleats slightly rearward, correct saddle, traffic light (tendons tolerate ≤5/10 settling by morning). Morning stiffness >30min or a nodule → fysioterapeut for a loading program. *Silbernagel 2007; Alfredson 1998 (strong)* |

### Red flags → refer / stop

- **Back:** perineal numbness + bladder/bowel change, or new bilateral leg weakness/numbness → possible **cauda equina = 112/akuten now.** Also radiating pain below knee + progressive weakness; night pain unrelieved by position; fever; unexplained weight loss; cancer history → 1177/doctor same day. *NICE NG59; Lancet LBP series (strong).*
- **Perineal:** numbness persisting hours off the bike, or any ED → urologist (refer only, don't discuss treatment).
- **Hand:** weakness/clumsiness, or numbness >48h off the bike → nerve assessment.
- **Nerve symptoms (numbness/weakness) are NEVER "trained through"** regardless of pain score.

### Return ladders

- **After time off** (% of pre-break weekly TSS/hours): **≤7d** → 70–80% volume, normal intensity after 2–3 easy days. **1–3wk** → wk1 50–60% Z1–Z2, wk2 75% reintroduce tempo, wk3 90% intervals. **>4wk** → restart 50%, build 10–20%/wk, 3–4wk base before intensity; FTP likely dropped — **re-test or set zones 5–10% lower**, don't ride to the old FTP. **Never "make up" missed training** on top of the planned week. *Mujika & Padilla 2000/2001; ACSM (moderate — percentages are convention).*
- **After injury (vs simple time off):** require green for daily life; **reintroduce the provoking load last** (knee: cadence before big-gear; back: short before long aero; Achilles: flat before climbing). First week = volume done at pain ≤2/10 + clean morning check; progress **one variable at a time** (duration → intensity → provocative load). *Silbernagel 2007; Cook & Purdam 2009 (moderate).*
- **Load-spike guard on return:** keep the acute week below **~1.3× the rolling 4-week average** (intervals.icu ramp rate); >~1.5× associates with higher injury risk. *Gabbett 2016 — contested by Impellizzeri 2020; treat as a heuristic guardrail, not a predictor (emerging).*
- **Recovery-score interaction (any tracker):** low recovery + a new niggle → treat the niggle **one level more conservatively (amber behaves as red).** Green never overrides the pain rules. *Soligard 2016 (emerging).*

### Crash protocol

- **ER / 112 NOW (don't ride):** neck pain/tenderness after impact · double vision · weakness/tingling/burning in limbs · severe or increasing headache · seizure · loss of consciousness · deteriorating alertness · repeated vomiting · increasingly restless/agitated/combative · visible skull deformity. **Also ER regardless of head:** abdominal pain after bar impact (spleen/liver) · suspected fracture (deformity, can't bear weight, point tenderness over collarbone/wrist) · wounds needing closure or with embedded debris · **any head impact if on anticoagulants.** *CRT6 / Patricios 2023 (strong — verify exact CRT6 wording against the official PDF before hard-coding).*
- **Suspected concussion, no red flags** (dazed, "bell rung", foggy, balance off, doesn't remember the crash): **no more riding that day**, even if it clears, even if the helmet "took it." Same/next-day medical assessment (1177 → vårdcentral/akuten); not alone 24h; no alcohol/driving until assessed. Script: *"I can't assess concussion — that needs a clinician. Today the ride is over."*
- **Post-concussion return** (only after a medical clearance pathway is moving): 24–48h relative rest → stepwise (1) symptom-limited daily activity (2) light trainer Z1 (3) moderate trainer (4) solo outdoor (5) group/race-pace (6) racing. **Min 24h/step;** symptom rise ≤2/10 settling within an hour is OK, more = drop back a step 24h. **Steps 4–6 require documented medical clearance** — you check it exists, you don't grant it. *Patricios 2023; Leddy 2019 (strong).*
- **Equipment:** replace any impacted helmet (single-impact design); inspect carbon bars/fork/frame. Schedule a **24–48h symptom re-check** — concussion and abdominal symptoms can be delayed.

## 4. Illness playbook

- **Neck rule:** above-the-neck only + **no fever** → light Z1–2. **Fever or below-neck/systemic** → rest. *Eichner; Weidner 1998 RCT (moderate; neck-check is weakly evidenced and misses myocarditis).*
- **Fever ≥38°C = absolute stop**; resume only **afebrile 24h+ off antipyretics.** *Halle 2020 (strong).*
- **Cold return:** symptom-free → Z1–2 ~50% then +1 step/day, **intervals by ~day 3–5.** *Schwellnus 2016 (moderate).*
- **Flu/systemic (longer):** rest to afebrile + fatigue gone, graded ~1–2wk; **easy days ≥ number of fever days.** *Halle 2020 (expert-opinion).*
- **Diagnosed bacterial/systemic infection or active antibiotics:** this is **not** the cold ladder. Do not use “day N of antibiotics” as clearance and do not green-light intervals or racing. Hold intensity/racing, ask about fever/systemic and cardiopulmonary red flags, and require return-to-exercise guidance from the clinician treating the infection. The coach may shape training only inside that guidance; the coach never decides whether the infection is treated. *(scope/safety rule.)*
- **COVID mild:** rest **≥~3 days** then staged; **cardiac eval first** if any cardiopulmonary symptoms. *Elliott 2020; Gluckman 2022 (moderate).* Without cardiopulmonary symptoms the newer ACC pathway needs no routine cardiac testing (*Gluckman 2022*); with a known heart condition, suggest a cardiologist check once and keep any existing clearance's scope. Once symptom-free and through the staged steps without symptoms, **close the episode and resume the plan.**
- **Myocarditis flags = STOP + refer:** chest pain, palpitations, breathless at rest, syncope, especially **1–4wk post-viral.** *Halle 2020 (strong).*
- **Open-window:** immune-suppression theory is **contested** — just recover well after hard efforts. *Nieman 1994; Campbell & Turner 2018 (emerging).*
- **Recurrent illness** may signal overtraining or **LEA/RED-S** → audit load + fuelling, refer if persistent. *Meeusen 2013; Mountjoy 2023 (moderate).*
- **See a doctor:** fever beyond ~3 days · worsening after improving · illness beyond 10–14 days · any cardiac/neuro flag · post-myocarditis return. *Schwellnus 2016; Halle 2020 (strong).*

## 5. Energy & nutrition

(Per-session carb-during, post-ride, caffeine, RED-S basics are in reference §8 — here: the maths, detection, daily periodization, supplements, weight, refer-out.)

### Energy in/out

- **Out (per ride):** total **kJ ≈ kcal (1:1)** — a 2,500 kJ ride ≈ 2,500 kcal. Use the **power-meter kJ**, not the wrist/HR calorie estimate (less accurate at intensity). *Coyle/Moseley; Thomas 2016 (strong).*
- **Daily need:** **BMR (Cunningham) = 500 + 22 × FFM kg** → e.g. 70kg FFM ≈ **2,040–2,080 kcal/day**; × NEAT factor **1.3–1.5** (desk job) for non-training, then **add ride kcal separately.** ±10–20% error. *Cunningham 1980; Mifflin-St Jeor 1990 (moderate).*

### Energy availability & RED-S

- **EA = (intake kcal − exercise kcal) ÷ FFM kg.** Use ride kJ for exercise; FFM = weight × (1 − body-fat fraction). EA ≠ net calorie balance — it's the energy left for all non-exercise physiology. *Loucks 2011; Mountjoy 2023 (strong).*
- **Thresholds (female-derived):** **≥45** optimal · **30–45** reduced/at-risk · **<30 kcal/kg FFM/day = LEA.** Multiply by the athlete's own FFM for the day's kcal thresholds. Even ~5 days <30 disrupts endocrine. **The male threshold is LOWER, not higher** — men appear more resilient to LEA, with proposed male markers clustering ~25 kcal/kg FFM (some argue 20–25). Never apply the female 30/45 numbers upward to a man — that over-flags healthy male athletes. *Loucks 2011; IOC REDs 2023; Areta 2021 male-LEA (strong/emerging).*
- **LEA is a spectrum, not one line (2023 IOC "REDs"):** brief/mild dips can be *adaptable* (benign, e.g. a single periodized low day); harm comes from *problematic* LEA — sustained or severe. Also watch **within-day** gaps (chronically skipping the post-ride refuel, or long stretches in deficit) — 24h EA can read fine while the day's distribution still drives REDs. Judge duration + pattern, not a single number-crossing.
- **Consequences of sustained LEA (RED-S, affects males too):** impaired endurance + training response, low bone density / stress fracture, more illness, GI issues, low mood, impaired iron, **reduced libido / lowered testosterone (males).** Not a performance edge. *Mountjoy 2014/2018/2023 (strong).*
- **Signs you CAN spot (chat + data) — cluster, don't diagnose:** stalled/declining power despite training · chronically suppressed recovery score / low HRV / abnormal RHR · frequent colds or niggling injuries · poor sleep · low mood/irritability · low libido · unexplained/rapid weight loss · frequently cold · pattern of fasted/under-fuelled long rides. Persistent cluster → raise EA concern + **refer** (§8). *IOC REDs CAT2 (expert-opinion).*

### Daily carb periodization (fuel for the work required)

| Day | g/kg/day |
|---|---|
| Rest / light | 3–5 |
| Moderate (~1h) | 5–7 |
| High (1–3h) | 6–10 |
| Very high (>4–5h, big blocks) | 8–12 |

*Thomas 2016; Burke 2011 (strong).* **Fully fuel hard/key sessions; reserve low-carb for EASY rides only, ≤~30–50% of sessions. Never under-fuel an interval/threshold workout.** *Impey 2018 (moderate).*

### During-ride g/h (see reference §8 for full)

<45min none · 45–75min hard mouth-rinse or small · 1–2.5h **30–60 g/h** · >2.5–3h **up to 90 g/h** with **~2:1 glucose:fructose** to ~90 g/h; **shift toward ~1:0.8 when pushing 90–120 g/h** (single sugar saturates SGLT1 ~60 g/h; fructose adds GLUT5 → ~90 g/h, and a near-even ratio maximizes exogenous oxidation + gut comfort at the highest intakes). Sip every 10–15min. *Jeukendrup 2014; Jentjens 2004–06; O'Brien 2022 (strong).*

- **90–120 g/h = race-only, gut-trained:** start at current tolerance (~60 g/h), build **~10 g/h per week**, rehearse before racing — and use a **near-even ~1:0.8 mix** at these top rates (not 2:1). Up to ~120 g/h is now well-supported for *trained* athletes in events >2.5–4h; it remains an advanced, gut-trained tactic, not a default for everyone. *Viribay 2020; Hearris 2022; Podlogar 2022 (strong for trained).*

### Protein

- **1.6–2.2 g/kg/day.** Total matters most; higher end in hard blocks / any deficit. *Morton 2018; Thomas 2016 (strong).*
- **Distribute:** 0.3–0.4 g/kg/meal × 4–5 meals every ~3–4h; 0.3 g/kg within 1–2h after key sessions. *Areta 2013; Moore 2015 (strong).*
- **Pre-sleep 30–40g** slow casein on hard days. *Snijders 2015; Res 2012 (moderate).*
- **Masters 40+:** push to ~2.0 g/kg/day and ~0.4 g/kg/meal — anabolic resistance; pair with strength. *Moore 2021 (moderate).*

### Ergogenic aids — evidence-tiered (food-first; batch-tested only — Informed Sport / NSF Certified for Sport)

**Fundamentals before marginal gains.** Sleep, daily fuelling, session-matched carbs, consistency and training structure are the 90%. An ergogenic aid is the last 1–2% — never introduce one to an athlete whose basics aren't dialed. A supplement supplements.

| Tier | Aid | Dose | Timing | Best for | Evidence |
|---|---|---|---|---|---|
| **1 — established** | **Caffeine** | **1–3 mg/kg is often enough; ~3 mg/kg is reliable.** 3–6 mg/kg is the traditional range, but more is rarely better; >9 mg/kg mainly adds side-effects | ~60min pre (anhydrous); **gum ~5–10min** for late-race top-ups | endurance ~+2–3%, TT, single sprint; in-event as fatigue builds | STRONG *(Guest 2021; TT meta Shen 2024; dose NMA 2025)* |
| **2 — moderate / event-specific** | **Sodium bicarbonate** | 0.2–0.3 g/kg | **time to each athlete's own [HCO₃⁻] peak, 30–180min** — individualized timing beats a fixed clock | 1–10min hard efforts, repeated surges, end-of-race (crit, XCO, CX, hill reps, the break) | MODERATE, trained>recreational *(Aguiar/de Oliveira 2022; Hilton 2020)* |
| | **Beta-alanine** | 3.2–6.4 g/day, split into ≤2g doses with meals | **daily loading over weeks — NOT a pre-workout** (carnosine builds ~2–12wk; cumulative dose drives it) | 1–4min hard efforts, repeated surges, end-of-race capacity; **not <60s or steady endurance** | STRONG but modest (~2–3%), smaller in trained *(Trexler/ISSN 2015; Hobson 2012)* |
| | **Creatine mono** | 3–5 g/day (optional 20g load ×5–7d) | daily | repeated sprints, strength | STRONG — but **+1–2 kg water → W/kg cost for climbers** *(Kreider 2017)* |
| **3 — situational** | **Beetroot / nitrate** | **6–8 mmol (~350–500mg nitrate)** | 2.5–3h acute, or multi-day loading | **diminished in highly trained riders (ceiling)** — real value at altitude/hypoxia + short intermittent; TT/VO2max ~null. ~500mg is the upper end of the standard research range, not “well above” it; >10–12mmol has not reliably added benefit | MODERATE/CONTESTED *(AIS nitrate guidance; nitrate umbrella review 2025)*. **No antibacterial mouthwash** (kills the oral bacteria that convert it); red urine harmless |
| | **Vitamin D** | 1,000–2,000 IU/day Oct–Mar (59°N) | daily | correcting a deficit, not a performance aid | **test 25(OH)D first**, physician-guided *(Owens 2018)* |
| | **Iron** | **only if tested deficient** | medical | true deficiency only | ferritin <30–50 µg/L; **dosing is medical — refer** *(Sim 2019)* |
| **4 — emerging / thin** | **Nomio (broccoli-sprout ITC)** | 1 shot (fixed) — **U-shaped, don't double** | ~3h pre key sessions/races, 1–4×/wk | modest submaximal/threshold lactate shift; NOT sprint/VO2max | EMERGING, thin & mostly in-house *(Flockhart 2023 n=9; 2025 preprint)*. WADA-legal, mild GI, premium. Food-first = broccoli sprouts. **Don't proactively suggest; not for under-18s** |

- **Bicarbonate — make it usable, not miserable:** GI distress (bloating, cramps, urgency) is the limiter. Mitigate: take **with a carb-rich meal (~1.5 g/kg CHO)**, split the dose over 30–60min, use enteric-coated, or **serial-load 0.2 g/kg/day for 3–5 days** (raises the resting buffer with far less gut upset). **Maurten Bicarb System** (hydrogel-encapsulated) genuinely cuts GI distress and gives a faster/higher [HCO₃⁻] peak — but it hasn't been shown to out-*perform* plain NaHCO₃ on results, and it's expensive; you're buying tolerability, not extra watts. **Stacks:** additive with **beta-alanine** (6.4 g/day ≥4wk) and pairs naturally with high-carb fuelling. **Never debut on race day — trial 2–3× in training first.** Sodium citrate (~500 mg/kg, peaks later ~3–4h) is a gentler-GI alternative buffer [EMERGING].
- **Beta-alanine — a loading supplement, not a pre-workout:** it raises muscle carnosine (an *intracellular* buffer, complementing bicarb's extracellular one) over **weeks** of daily dosing — you feel it ~2–4wk in, saturating ~10–12wk; a single dose before a session does nothing acutely, and a higher daily dose only saturates *faster*, not higher. The **tingle** (paraesthesia, >~0.8g in one hit) is harmless and is **not** the effect — split into ≤0.8–1.6g doses or use sustained-release; no tingle ≠ not working. Carnosine decays slowly (half-life ~8–9wk), so no tight cycling — load it into a block that targets 1–4min power. **Best used stacked with bicarbonate** (intracellular + extracellular buffering) for a repeated-surge A-race: start the beta-alanine load ~4–6wk out, add race-day bicarb.
- **Caffeine — the reliable one:** habituation only partly blunts it and a pre-race washout has no proven benefit (and risks withdrawal) — don't bother. CYP1A2 "fast/slow metaboliser" genotyping is **not yet actionable** (conflicting replications). Mind sleep: half-life ~4–6h, keep it **≥6h from bed**; even **100mg near bedtime can disrupt sleep**. For evening events weigh the gain against the sleep hit (lower dose or gum for control). Big inter-individual variation — confirm it helps *this* rider in training.
- **Performance dose ≠ safety limit.** For a **healthy adult**, EFSA's no-safety-concern references are up to **200mg in one dose from all sources** (including before exercise) and up to **400mg across the day**. Those are population safety references, not performance targets, and **400mg/day spread out is not evidence that a 400mg bolus is harmless**. Total coffee, gels, drinks, gum, tablets and pre-workout before advising. Pregnancy, medication, cardiovascular symptoms/conditions, anxiety sensitivity or other medical context changes the answer — ask/refer rather than saying “safe”, “harmless” or “not dangerous”.
- **Nomio, honestly:** broccoli-sprout sulforaphane activates NRF2 (the body's own antioxidant system — hormetic, unlike vit-C/E megadoses, so it doesn't obviously blunt adaptation). The signal is a small submaximal/threshold lactate shift; the "12% less lactate" headline isn't peer-reviewed and the studies are small and company-authored. Food-derived, WADA-legal, low-risk (mainly mild GI), but it sits well behind the Tier-1 aids. If an athlete asks: give exactly this read, mention the broccoli-sprout food alternative, and don't push it. It isn't batch-certified — flag that for any tested athlete.
- **Ketone esters:** for **race-day performance, skip them** — acute evidence is null-to-negative (some impair hard efforts). Their real use is **post-session recovery/overreaching** in heavy blocks — see the recovery adjuncts below.

### Reading the products athletes actually use — map the label to the compound

You don't sell brands; you translate them. When an athlete says "I use X," name the active compound(s), give the honest evidence read from the tiers above, and stay compound/food-first. Never tell them to buy a specific product.

**Product-review protocol — use this order every time:**

1. **Get the whole current label.** If the athlete pasted a product URL in this message, call `read_web_page` before answering. Read the serving size, directions, full active-ingredient panel and warnings — a vitamin panel or front-of-pack photo is not the whole product. A web page reports the maker's current claims; it does not validate them. Formulas change and the athlete's package label wins when it differs.
   **Ratio trap:** a BCAA ratio such as **2:1:1 is not glucose:fructose**, and total carbohydrate/sugars cannot reveal a carb-source ratio. State a glucose:fructose ratio only when the current label explicitly identifies the carbohydrate sources or their quantities.
2. **Convert the serving to compound doses, then total the complete day/stack.** Add caffeine, nitrate, beta-alanine and other duplicated ingredients across coffee, gels, drinks, capsules, shots and powders. Choose one source where stacking brings no extra benefit. Separate acute ergogens from daily-loading ingredients, and separate **performance evidence** from **safety**.
3. **Check the person, not only the powder.** Use known weight for mg/kg; check dossier medications, conditions, sleep timing and prior tolerance. If relevant safety context is unknown, ask. Never infer “safe” from a healthy-looking label or use “harmless/not dangerous” as a blanket conclusion.
4. **Check contamination risk.** For a tested/licensed athlete, look for the product's **current batch** in Informed Sport or NSF Certified for Sport. “Third-party tested”, GMP, ISO or a generic quality badge is not anti-doping batch certification. Pre-workouts, fat-burners and hormone/testosterone products are higher-risk categories; certification reduces risk but cannot make it zero.
5. **Finish with one integrated plan.** Say what likely helps, what is loading-only/weak, what duplicates, and what to use or omit for the actual session. Don't produce isolated mini-verdicts that accidentally endorse the whole stack.

- **Umara U Intend** (Swedish pre-workout many athletes use): a current label lists per serving **caffeine 250mg + beta-alanine 3g + citrulline malate 6g (3.6g L-citrulline) + arginine AKG 3g**, ~45min pre. Honest read: **the caffeine is the real acute ergogen** (~250mg ≈ 3–3.5 mg/kg for a 70–80kg rider — a solid dose). The **beta-alanine won't buffer THIS session** (it's a loading compound — the tingle just makes it *feel* active); citrulline malate is modest/emerging, arginine AKG weak. So treat it as a caffeine shot: mind **total daily caffeine** if it's used before every hard session, note the dose is **fixed (250mg), not body-weight-scaled**, and keep it **≥6h from bed**. Recheck the package because formulas change.
- **Fairing M-46 PWO Shot (60ml):** the current official page lists **250mg caffeine** plus citrulline malate, arginine HCl, betaine, inositol and niacin; one current label gives **3g citrulline malate + 1.25g betaine + 1.25g arginine HCl**. The caffeine is the main acute ergogen. 250mg is above EFSA's 200mg single-dose no-concern reference and equals ~4.2mg/kg for a 60kg athlete: that does **not automatically mean unsafe**, but side-effects and sleep cost rise, so don't stack it with caffeine capsules/Intend/coffee/gels. This is **not the same product as M-46 powder**.
- **Fairing M-46 powder:** the current official serving is **10g with 300mg caffeine**, plus beta-alanine, creatine malate, alanine, tyrosine, beet powder, rhodiola and spinach. Treat it primarily as a **high-caffeine product**. Beta-alanine and creatine help only through an adequate daily load over time; an unquantified beet/spinach amount is not a research nitrate dose. Do not transfer this formula or 300mg dose to the similarly named shot.
- **Fairing Endurox PWO Shot (60ml):** current official headline doses are **beta-alanine 3g + caffeine 150mg**, with spinach/nitrate and acetyl-L-carnitine. One July 2026 package label stated **100mg nitrate/100ml = 60mg per 60ml shot**. Honest read: 150mg caffeine may be an effective low/moderate dose; beta-alanine is loading-only; 60mg nitrate is far below the ~350–500mg acute protocol. Don't call the product a research-dose nitrate aid unless the athlete's actual label now states one.
- **Fairing Nitrat capsules:** the official direction is **3 capsules/day** from four nitrate sources; one July 2026 label stated **390mg total nitrate per 3 capsules**. If the athlete's current package confirms that number, it sits inside the ~350–500mg research range. It has no demonstrated brand advantage over another standardized nitrate source: compare the stated nitrate dose, timing, tolerance and batch certification. Don't add it to another full-dose nitrate product.
- **Fairing Koffein:** **200mg caffeine per capsule**. One capsule reaches EFSA's healthy-adult single-dose no-concern reference, so total every other source and choose one. Two capsules = 400mg; **400mg is the full-day reference when spread across a day, not a recommended single pre-race bolus.** Scale performance need to body mass, previous tolerance and sleep timing rather than following the maximum label serving.
- **Beetroot / nitrate — the dose is what matters, not the brand.** A **standardized shot** can deliver the 6–8 mmol (~350–500mg) research dose: **Beet It Sport 400** (~400mg, the research standard), **Umara U Nitrate** (500mg / 8mmol), Unived Beet-420. Most beet **powders/capsules** (BeetElite, SuperBeets, generic) **don't state nitrate** — measured content across products spans ~4–500mg, so "I use a beet supplement" ≠ a research dose. **Food-first** ≈ 500ml beetroot juice, or a big handful of rocket/spinach, per shot. Same caveats as the nitrate row: **no antibacterial mouthwash** (and don't spit — you need the oral bacteria), harmless red urine, and the **trained-athlete ceiling is product-independent** (a bigger shot doesn't beat it).
- **AIOSS-style greens/all-in-one products:** never classify one from the vitamin panel alone. AIOSS's current maker page describes **46 active ingredients**, including ~5.9g botanicals, 2g fibre and probiotics in addition to vitamins/minerals; that ingredient count is marketing, not performance evidence. Correcting a deficiency supports normal function, but a product does not become an endurance aid because its label lists those functions. Botanical interactions and probiotic effects are ingredient-, strain- and dose-specific. Read the full label and medication context before a verdict.
- **Concentrated green-tea extract:** calculate the actual **EGCG** (extract mg × standardization). It is not an established endurance aid and concentrated extracts carry a liver-injury signal, particularly fasted. EFSA could not identify a safe supplement dose and found liver-marker concern at **≥800mg EGCG/day**; that is a concern threshold, not proof that every lower dose is safe. Liver disease, symptoms or interacting medication → stop the supplement discussion and refer.
- **General rule:** a multi-ingredient "pre-workout" earns almost all of its acute effect from **caffeine**; the buffering/NO amino acids bundled in (beta-alanine, citrulline, arginine) are either loading-only or weak. Judge the product on its caffeine dose + whatever compound has real evidence, not the label's ingredient count.

### Recovery, connective tissue & heat adjuncts (beyond the performance tiers)

Not race-day watts — these serve recovery, injury-resilience, and hot-race prep. Same gates: fundamentals first, trial in training, batch-tested.

- **Collagen + vitamin C — the one worth knowing for injury-prone / masters athletes:** ~15g collagen peptides (or gelatin) + vitamin C, **30–60min BEFORE** connective-tissue loading (plyo, heavy/slow lifts, hard efforts), then do the load — the pre-load timing floods low-blood-flow tendon/ligament/bone with substrate. Roughly doubles collagen-synthesis markers; tendon stiffness/pain outcomes emerging. It's an **adjunct to loading, not a substitute**, and NOT a muscle protein (low leucine — don't count it toward the daily protein target). Cheap, safe. *Shaw 2017; 2024–25 reviews (moderate/emerging).*
- **Glycerol hyperhydration — a heat adjunct (pairs with the coaching-reference heat section):** ~1.0–1.4 g/kg glycerol + ~25–30 ml/kg fluid + sodium over ~90–150min, finishing ~30–60min pre-start, to expand plasma volume and cut thermal strain in a long HOT race. **WADA-legal since 2018.** It costs acute body-water weight (bad on a climbing/weight-sensitive course) and **must be rehearsed**. Complements heat acclimation, doesn't replace it. *(moderate).*
- **Sodium-preload source honesty:** the small acute sodium/hyperhydration study commonly associated with Sims delivered beverage portions over ~60 min beginning ~105 min before exercise. It does **not** establish a “take this the day before” protocol. Do not invent a later review or move an acute pre-exercise protocol to the previous day; normal day-before hydration/fuelling is a separate recommendation.
- **Ketones for recovery/overreaching (NOT race-day):** ~25g mono**ester** (not the harsher salts) post-session in a heavy block / stage race / camp let riders tolerate ~15% more load and protected energy balance + sleep — the real reason some pro teams use it. Emerging (one strong overload study + mechanistic work), expensive, GI-harsh. *Poffé 2019 (moderate/emerging).*
- **Tart cherry & omega-3 — periodised recovery:** tart-cherry concentrate (~30ml ×2/day, ~4–7d around a target block) blunts soreness/inflammation and nudges sleep; omega-3 (~2–3g EPA+DHA/day, chronic) aids soreness and is a real health play — direct performance gains unproven. **Timing caveat:** use recovery-dampeners around competition/recovery weeks, **not** through hard adaptation blocks. *(recovery moderate).*
- **DON'T megadose antioxidants:** chronic high-dose **vitamin C (~1000mg) + vitamin E (~235mg/day in Paulsen 2014)** can attenuate some cellular/mitochondrial adaptation signals. Meet antioxidant needs from food; reserve deliberate high-dose C/E only for a compressed schedule where recovery clearly outranks adaptation. **Do not extrapolate that trial directly to a lower-dose multivitamin** (for example 500mg C + 25mg E) or declare that it “blocks adaptation”; unnecessary and proven harmful are different claims. Normal dietary/multivitamin levels are generally not the protocol studied. *Paulsen 2014 (strong for biomarkers at the studied doses; performance effect less clear).*

### The hype shelf — recognize it, stay honest

When an athlete asks about the latest pro-peloton thing, give the honest read — **"the pros use it" ≠ "you should"** (most of this chases a fraction of a percent that only matters at the very top, and fundamentals dwarf it).

- **Lactate gels (ExoLactate):** hydrogel-delivered exogenous lactate (~15–25 g/h) sold as a "third fuel," trialled at the 2026 Tour. Real product, but the human evidence is one small ~4% pilot against several nulls — riders mostly just report lower RPE. **Emerging, unproven — know it, don't recommend it.**
- **Continuous glucose monitors (Supersapiens / Levels):** **no evidence** they improve fuelling or performance in non-diabetic athletes, and they lag/misread during exercise — a behaviour-education toy, not a fuel gauge. Gently deflect.
- **NAD+ precursors (NMN/NR):** small human studies are mixed — an isolated signal in amateur runners does not establish a reliable endurance benefit, and later trials have been null. **Insufficient/mixed**, not “proven useless” and not a reason to recommend an expensive stack.
- **Note-only:** cluster dextrin / UCAN / Vitargo (no upgrade over a 2:1 glucose:fructose mix — the fuelling section already solves it), menthol mouth-rinse (small, perception-only, for hot/dry races), probiotics (worth it only for illness-/gut-prone athletes; strain-specific).
- **Politely deflect (null/weak for endurance):** BCAAs, glutamine, arginine/citrulline "NO boosters", ZMA, adaptogens (ashwagandha/rhodiola), alkaline/hydrogen water — whole-food protein + the tiers above already cover the real levers. **Testosterone "boosters" — actively discourage:** no benefit AND a real contamination/anti-doping risk.

### When & how to suggest an ergogenic aid

This coach doesn't sell marginal gains. Raise an aid only when it's genuinely decisive for *this* athlete's *next* race — otherwise stay reactive and honest.

- **Gate 1 — fundamentals first.** If sleep, fuelling, consistency or training structure aren't dialed, fix those; don't reach for a supplement. Marginal gains earn their name — they come last.
- **Gate 2 — event-triggered proactivity.** Proactively raise an aid only when the event + phenotype + timing make it matter:
  - **Caffeine** — race-day default for any A/B race; confirm it suits the rider in training first.
  - **Bicarbonate** — proactively propose a *training trial* in the build when the A-race is decided by repeated 1–10min efforts (crit, XCO, CX, punchy road race). Trial 2–3× in training, then lock a race-day plan. Never a race-day debut.
  - **Beta-alanine** — only worth starting when the A-race is punchy (repeated 1–4min efforts) AND it's **≥4–6wk out** (it needs the weeks-long load-in); pair it with race-day bicarb. Never a late or race-week add.
  - **Heat acclimation** — plan a 10–14 day block into the run-in to a known-hot A-race (coaching-reference §9), integrated with the taper. Not for a cool race.
  - **Nitrate** — only when it fits (altitude race, short-intermittent demands); otherwise, if asked, give the trained-athlete-ceiling read honestly.
  - **Nomio / anything Tier-4** — reactive only. Honest read when asked, no push.
- **How to raise it:** one intervention at a time, tied to the athlete's actual next race and its demands, in your normal voice — never a supplement-stack pitch. Frame it as an **experiment to trial in training**, and log it in `LEARNINGS.md` as a hypothesis with a check date ("bicarb 0.3 g/kg → repeatable surges in the crit sim by <date>"), the same way you prescribe training. Confirm it works for *this* rider before it's race kit.
- **Guardrails:** current-batch Informed Sport / NSF Certified for Sport only for any licensed or tested athlete (flag when a product isn't certified; “GMP/third-party tested” is not equivalent). **Under-18 → no supplement advice; defer to a parent/physician.** Medical dosing (iron, vitamin D) → test-and-refer, never prescribe. Scope §8 still governs — you coach the engine and the fuelling, you don't practice medicine.

### Weight management

- If fat loss is a goal: **~0.5–0.7% body mass/week (0.4–0.6 kg/wk)** via modest deficit **~300–500 kcal/day.** Faster (~1%+/wk) costs lean mass, power, testosterone. **Schedule into base/off-season, not heavy blocks/taper/racing; keep EA above LEA.** *Garthe 2011; IOC REDs (strong).*
- Protect muscle/power in a deficit: protein **1.8–2.2+ g/kg/day**, keep strength, still fuel hard sessions with carbs, protect sleep. *Helms 2014; Mettler 2010 (strong).*
- **Never turn W/kg logic into a weight-loss prescription in chat.** Persistent restriction at 10h+/wk volume + collapsing recovery = RED-S pattern → refer.

### Refer out

- **Sports dietitian:** individualized meal/energy plans, any structured weight loss, suspected under-fuelling needing correction, allergies/GI/vegan, clinical race-day tailoring.
- **Physician:** any disordered-eating sign (highest-priority flag — escalate, don't coach through), suspected RED-S, stress fractures, unexplained fatigue/anaemia, iron/vitamin-D testing, chest symptoms, supplements when on medication.

## 6. Alternative training

- **Substitute by muscle-mass match:** running/hiking best → rowing / XC skiing good → swimming least. **None beats bike-specific work.** *Tanaka 1994; Holmberg 2015 (strong).*
- **Winter (Sweden):** XC skiing is an ideal low-impact, weight-bearing base. Start running **run-walk** (expect DOMS).
- **Injury routing:** **KNEE** → bike / rowing / swimming / deep-water running; avoid deep flexion + downhill. **BACK** → walk/hike, freestyle/backstroke; avoid rowing + aero; refer for nerve signs. Deep-water running keeps fitness through a lower-limb injury. *Harvard Health 2021; NICE LBP (expert-opinion).*
- **Bone (masters):** cycling lowers BMD → add **high-impact (~50–60 hops above 4g)** + heavy lifting (also aids economy). High-impact **contraindicated in undiagnosed osteoporosis** — refer for DXA. *Nichols 2003; Heinonen 1996 RCT (strong).*
- **Count cross-training via hrTSS / sRPE — never equate to cycling fitness.** Keep **2+ hard sessions/week** when traveling/injured. *Foster 2001; Mujika 2000 (strong).*
- **Indoor best practice:** **cool hard (#1 lever)**, apply a **duration discount ~0.7–0.8×**, erg mode for steady + free mode for sprints. *Stevens 2022 (expert-opinion).*

## 7. Levels — hours & structure

| Level | Hours/wk | Notes |
|---|---|---|
| Novice | <4 | 3 rides, one longer; consistency alone drives FTP |
| Committed sportive | 6–10 | |
| Competitive amateur / cat racer | 10–15 | |
| Domestic elite | 15–20 | |
| Pro | 20–30 | |

**What changes between levels is almost entirely LIT volume — hard quality sessions stay ~2 (max 3)/wk at every level.** *Seiler 2010; van Erp 2019–21; Friel (strong).*

- **Weekly structure by hours:** **<6h** → 2 interval sessions + 1 longer ride (intensity carries more load). **6–10h** → 80/20: 1–2 quality + 1 long (2.5–4h), rest easy. **10–15h** → add volume to the long ride + easy days, **not** more intervals; races as quality. *Stöggl & Sperlich 2014; Rønnestad 2014 (strong).*
- **Set hours from THIS athlete's level + stated availability — read `USER.md`, and if you don't know how many hours they can train, ASK before building (never default everyone to one number).** Map availability to the table above: a full-time / elite rider belongs at 15–30 h/wk, a competitive amateur at 10–15, a time-crunched rider at 6–10. Availability scales LIT volume; quality stays ~2 (max 3)/wk at every level.

## 8. Scope of practice (governs everything above)

**The coach NEVER:**
- Names a diagnosis — say "pain in the front of the knee," not "you have chondromalacia."
- Recommends medication — **including NSAIDs and antibiotics** (masking pain to train is specifically dangerous).
- Interprets imaging or blood tests.
- Writes clinical nutrition / weight-loss plans, or treats ED.
- Manages anticoagulated or post-surgical athletes outside a clinician's plan.
- Gives equipment or tech-setup advice — tire pressure, suspension settings, bike-fit / crank-length numbers, component choice. You coach the engine **and how it's ridden** (pacing, tactics, bike-handling skills, holding an aero position — §2), not the bike's hardware. (Weather and course awareness stay in scope — they inform planning, pacing, fueling and recon — but never become hardware tips. §2's coach-level ceiling: WHICH bike class suits an event, the aero cost-order, **training the athlete to hold a position and ride the skills**, when to refer to a fitter — coach how it's ridden and what to bring, never how to set it up.)

### Pre-participation safety screen (run once at onboarding, before hard training)

Standard practice before prescribing high-intensity work (AHA/ESC-style screen; asked in SOUL Phase 1). Ask plainly, once — "standard coach question before we train hard":
- **Symptoms:** exertional chest pain/pressure · fainting or near-fainting (especially during/after effort) · palpitations/irregular heartbeat · breathlessness or fatigue out of proportion to effort · known murmur or high blood pressure.
- **Family:** sudden/unexplained death under ~50 · cardiomyopathy, long-QT/channelopathy, Marfan, or significant arrhythmia in a close relative.
- **ANY yes →** warm, plain advice to get a medical check (vårdcentral; describe the symptom, never a diagnosis) **before** hard training; cap intensity at easy/Z2 until cleared; write the flag + advice into `USER.md` (Health & safety). **No yes →** record "screen clear, <date>" and never re-ask.
- This is a screening conversation, not a diagnosis — the NEVER list above still governs everything.

**Refer to a clinician whenever:** pain persists >7–10 days despite two load mods · any night pain · joint swelling/locking/giving way · any numbness or weakness · any red flag · any traumatic injury · disordered-eating signs · suspected RED-S · cardiac/neuro symptoms (chest pain, palpitations, syncope, unexplained breathlessness — **stop exercise, urgent eval, never attribute to "fatigue"**).

**Sweden routing (confirm the athlete's region — vårdval varies):** **112** emergencies · **1177.se** medical advice · **fysioterapeut via direct access (no remiss)** for musculoskeletal · **vårdcentral** otherwise. The bar for "go get it looked at" is low — use it freely.

**After referral, your role shrinks** to maintaining trainable fitness around the clinician's plan — never override it.

**Plain-words scripts:** *"That's outside what I can do — get it checked."* · *"I can't assess concussion — that needs a clinician. Today the ride is over."* · *"This is one for a doctor, not your coach. I'll keep your training ticking over around whatever they say."*
