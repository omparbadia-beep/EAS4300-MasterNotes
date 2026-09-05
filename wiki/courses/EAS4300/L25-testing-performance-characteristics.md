# L25 — Testing and Performance Characteristics

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 25 · **Date:** Wed 18 Nov 2026
**Book §:** 9.5 *Performance Characteristics* (p. 451) — **of the centrifugal compressor**, since
Chapter 9 is *The Centrifugal Compressor*

> 🚨 **Reconciled 2026-08-25 — read this before studying the page.**
>
> §9.5 is **"Performance Characteristics" inside Chapter 9, *The Centrifugal Compressor.*** It is
> about centrifugal compressor **maps, surge, and choke** — *not* gas turbine engine test cells.
>
> The syllabus topic name, "Testing and Performance Characteristics," suggests engine testing. The
> section reference says centrifugal compressor maps. **These are different subjects, and the
> reference points at the narrower one.** Reinforcing that reading: L22 and L26 also cite Chapter 9,
> so the last block of the course appears to be Chapter 9 material with rockets (Ch. 10) inserted.
>
> **This page now covers both.** §0 below is the literal §9.5 reading (centrifugal performance
> characteristics); §1 onward is engine-level testing, which the topic name implies and which is
> genuinely useful regardless.
>
> 🎓 **Updated 2026-09-05 — the engine-testing reading (§1 onward) now has real corroboration.**
> Cross-referenced against a parallel offering's (Section 5041, Spring 2026, Mr. Marcos) "Controls,
> Test, and Analysis" lecture: its content is almost exactly §1–§8 below — test stand types
> (ground/altitude/flying test bed), instrumentation categories (health-and-safety, production,
> performance rakes, dynamic, structural), airflow measurement via pitot/bellmouth, and data
> reduction/calibration analysis. **This doesn't settle which reading your Fall 2026 syllabus intends**
> (the parallel course's version of this content sits at a different lecture number, L22, alongside
> engine-controls material that doesn't appear anywhere in your syllabus at all), but it's real
> evidence that "engine-level testing" is a genuine, substantial topic this course family covers, not
> just a guess from the topic name. Two worked examples from that lecture are added below
> (§3 and a new §8b). **Still ask the instructor which reading applies to your final.**
> See [textbook-section-map](textbook-section-map.md).
**Tags:** #engine-testing #test-cell #instrumentation #uncertainty #certification #altitude-test #health-monitoring #gas-path-analysis #performance-deterioration

---

## Why this lecture matters

The syllabus lists "systems testing" alongside components and systems analysis as one of the course's
three declared focus areas. Everything computed in the previous 24 lectures has to be **measured** to
be believed — and measuring thrust to 0.5% on a 400 kN engine is genuinely hard. This lecture also
introduces the engine-health tools that turn the component maps of
[L16](L16-compressors-3.md)/[L21](L21-turbines-3.md) into a diagnostic method.

---

## Core concepts

### 0. Centrifugal compressor performance characteristics (§9.5 — the literal assigned section)

Read this alongside [L22](L22-centrifugal-compressors.md), which covers §9.1–9.4.

#### The map, and how it differs from an axial map

Same axes as any compressor map ([corrected-parameters](../../concepts/corrected-parameters.md)):
pressure ratio vs. corrected mass flow, with constant corrected-speed lines and efficiency islands,
bounded by **surge** on the left and **choke** on the right.

$$
\pi_c,\ \eta_c = \mathrm{fn}\left(\frac{\dot m\sqrt\theta}{\delta},\ \frac{N}{\sqrt\theta}\right)
$$

But the *shape* is characteristically different:

| | **Axial** | **Centrifugal** |
|---|---|---|
| Speed lines | Shallow, closely spaced | **Steep, widely spaced** |
| Pressure ratio per stage | 1.3–1.4 | **3–8** |
| Flow range at fixed speed | Narrow | **Wider** |
| Efficiency (peak) | 0.90–0.92 | 0.76–0.84 |
| Flow per frontal area | High | Low |

**Why the speed lines are steep:** a large share of the pressure rise comes from the
$U_2^2$ centrifugal term in the Euler equation, which is nearly independent of flow rate. So pressure
ratio stays high as flow varies — the line is steep and the **stable operating range is wide**. That
wide range, not efficiency, is why centrifugal stages dominate **helicopter engines, APUs, and
turbochargers**, where the throttle sweeps constantly.

#### The two boundaries

**Choke ("stonewall") — the right-hand limit.** Set by the **inducer throat** reaching $M = 1$ in the
relative frame. Once choked, flow cannot increase and the speed line drops vertically. Because the
inducer tip has the highest relative velocity, it chokes first — which is exactly why inducer design
([L22](L22-centrifugal-compressors.md) §2) governs the high-flow end.

**Surge — the left-hand limit.** Usually initiated in the **diffuser**, not the impeller. As flow
falls, the absolute flow angle leaving the impeller swings more tangential; if it exceeds what the
diffuser can accept, the diffuser stalls and the stage surges. Mild flow reduction gives **rotating
stall**; further reduction gives full **surge** — the same distinction as in the axial case
([L16](L16-compressors-3.md) §4).

#### The diffuser trade — the design decision §9.5 exists to inform

$$
\text{vaneless diffuser: wide range, lower peak } \eta
\quad\longleftrightarrow\quad
\text{vaned diffuser: higher peak } \eta,\ \text{narrow range}
$$

- **Vaneless** — flow spirals out conserving angular momentum ($C_w r$ = const). Tolerates a wide range
  of incoming flow angles, so the map is broad. Bulky, and diffusion is less effective.
- **Vaned** (or pipe/wedge diffusers) — recovers more pressure in less radius and raises peak
  efficiency by several points, but the vanes have a preferred incidence, so **range narrows sharply**.

**Choose by application:** turbochargers and APUs want range → vaneless or lightly vaned. A fixed-point
industrial compressor wants efficiency → vaned. This is the same range-vs-efficiency trade that
recurs across the whole course.

#### Why it matters for the exam

If the final treats §9.5 literally, expect: *sketch a centrifugal compressor map, label surge and
choke, identify which component sets each boundary, and explain the vaned/vaneless trade.* All four
are on this page.

### 1. Why testing is unavoidable

- **Component interactions** can't be fully predicted. Matching ([L21](L21-turbines-3.md)) involves
  maps whose off-design regions are themselves empirical.
- **Certification requires it.** FAA/EASA demand demonstrated bird ingestion, fan blade off
  ([L18](L18-transonic-fan-stage.md) §6), icing, rain/hail ingestion, and a 150-hour endurance block.
- **Instability is not reliably predictable.** Surge, flutter, and combustion instability
  ([L11](L11-combustors.md), [L24](L24-rocket-engines-2.md)) are still found on the test stand.
- **Deterioration** must be characterized over life, not just at delivery.

### 2. Types of test facility

| Facility | Capability | Limitation |
|---|---|---|
| **Sea-level test bed** | Static thrust, fuel flow, basic performance, endurance | No forward speed or altitude |
| **Altitude test cell** | Conditioned inlet air ($p_{02}$, $T_{02}$) and exhaust vacuum ⇒ simulates any point in the envelope | Expensive; no true ram/inlet flow field |
| **Flying test bed** | Real installed conditions on an aircraft | Very expensive, limited instrumentation |
| **Wind tunnel (component)** | Cascades, inlets ([L10](L10-inlets.md)), nozzles | Component only |
| **Rig test** | A single compressor or turbine, electrically or air driven | Component maps in isolation |

**Altitude test cells** are the workhorse for performance validation. They condition the inlet air to
the $p_{02}$ and $T_{02}$ corresponding to a flight condition, and pump down the exhaust to the
corresponding $p_a$. Because the **corrected parameters** ([corrected-parameters](../../concepts/corrected-parameters.md))
fully determine the aerodynamics, matching $\theta$ and $\delta$ on the ground reproduces the flight
aerodynamic state exactly — **this is the practical payoff of the whole corrected-parameter framework.**

**Direct connect vs. free jet.** A direct-connect cell pipes conditioned air straight to the engine
face (clean, repeatable, but bypasses the inlet). A free-jet cell blows a supersonic jet over a
complete inlet + engine, capturing inlet/engine interaction ([L10](L10-inlets.md) §8) at much greater
cost.

### 3. Measuring thrust

**The hardest primary measurement.** The engine is mounted on a **thrust frame/stand** that floats on
flexures, and the reaction force is measured by **load cells**.

**Corrections required** — each is a real error source, and the list is a likely exam item:

| Correction | Cause |
|---|---|
| **Tare force** | Fuel, oil, instrumentation lines crossing the floating frame |
| **Cell pressure / scavenging** | Airflow induced through the cell by the jet creates a pressure differential across the engine |
| **Bellmouth momentum** | The inlet momentum of air drawn into the cell |
| **Buoyancy** | Ambient pressure acting on the frame |
| **Thermal growth** | Frame expansion during a long run |

**Achievable uncertainty: ±0.25–0.5%** on a well-instrumented stand. That sounds loose until you note
that a **1% TSFC** improvement is a major program achievement
([L09](L09-engine-aircraft-performance.md) §7) — so the measurement uncertainty is comparable to the
effect being measured. This is why back-to-back testing (same stand, same day, before/after a change)
is far more trusted than absolute numbers.

### 4. Measuring mass flow and fuel flow

**Airflow:**
- **Bellmouth** — a calibrated contoured inlet with static pressure taps. The workhorse: accurate
  (±0.5%) and simple, because the flow is well-behaved and the discharge coefficient is well
  characterized.
- **Venturi / orifice plate** — for ducted rigs
- **Compressor face rakes** — total pressure/temperature rakes, integrated over the annulus

**Fuel flow:**
- **Turbine flowmeter** — most common, ±0.5%
- **Coriolis meter** — measures **mass** flow directly (no density correction needed), ±0.1–0.2%. The
  modern choice, because fuel density varies with temperature and batch.

**Why this matters for TSFC:** TSFC $= \dot m_f/F$, so its uncertainty combines both:

$$
\frac{\delta(\mathrm{TSFC})}{\mathrm{TSFC}}=\sqrt{\left(\frac{\delta \dot m_f}{\dot m_f}\right)^2+\left(\frac{\delta F}{F}\right)^2}
$$

With ±0.3% on fuel and ±0.4% on thrust, TSFC uncertainty is **±0.5%** — again, comparable to the size
of an improvement worth pursuing.

**Worked example — airflow from a bellmouth pitot measurement** (cross-referenced from a parallel
offering's in-class problem). A sea-level static test stand has a 4 ft diameter bellmouth duct with
1/8″ boundary-layer allowance. $P_a=14.7$ psia, $T_a = 59°\mathrm F$, measured static pressure in the
duct $p_s = 13.2$ psia, $\gamma=1.4$, $R=53.4\ \mathrm{ft\,lbf/(lbm\,°R)}$.

Since $V_0=0$ (static stand), $P_{02}=P_a$, $T_{02}=T_a$. Get Mach number from the static/stagnation
pressure ratio, then everything else follows:

$$
\frac{p_{02}}{p_s} = \left(1+\frac{\gamma-1}{2}M^2\right)^{\gamma/(\gamma-1)}
\;\Rightarrow\; M = 0.395
$$

$$
T_s = \frac{T_{02}}{1+\frac{\gamma-1}{2}M^2} = 503.0°\mathrm R,
\qquad V = M\sqrt{\gamma R T_s\, g_c} = 434.4\ \mathrm{ft/s}
$$

$$
\rho = \frac{p_s}{RT_s} = 0.071\ \mathrm{lbm/ft^3}, \qquad
A_{\text{eff}} = \pi\left(\frac{D}{2}-\delta_{BL}\right)^2 = 12.43\ \mathrm{ft^2}
$$

$$
\dot m = \rho A V = 382.5\ \mathrm{lbm/s}
$$

Since this is a sea-level standard-day point, $\theta_2=\delta_2=1$, so the corrected flow equals the
physical flow exactly — **the correction only bites at altitude or off-standard temperature**, which
is the entire point of doing corrected-parameter bookkeeping in the first place
([corrected-parameters](../../concepts/corrected-parameters.md)).

**Contrast — the same calculation at altitude** (cross-referenced from a parallel offering's homework,
0.8 $M_n$ / 30,000 ft): here $P_2=6.7$ psia, $T_2=-20°\mathrm F=439.7°\mathrm R$, so
$\theta_2 = 439.7/518.67 = 0.848$ and $\delta_2 = 6.7/14.696 = 0.456$ — both **far from 1**. The same
pitot-probe method gives physical $\dot m_2 = 127.7$ lbm/s but **corrected** $W_{2c}=257.8$ pps — nearly
**double** the physical flow, because $W_{2c}=\dot m\sqrt\theta_2/\delta_2$ and $\delta_2$ is small.
This is the concrete answer to "why bother correcting at all": two engines running the same *physical*
airflow at different altitudes are doing very different amounts of aerodynamic work, and only the
corrected number lets you compare them, or compare either to a sea-level map.

### 5. Gas path instrumentation

Standard measurement stations ([station-numbering](../../concepts/station-numbering.md)):

| Station | Typical measurements |
|---|---|
| 2 | $p_{02}$, $T_{02}$ (rakes), inlet distortion screens |
| 2.5 / 13 | LPC/fan exit $p_0$, $T_0$ |
| 3 | $p_{03}$, $T_{03}$ — compressor discharge; the key cycle point |
| 4 | **Rarely measured directly** — too hot for probes |
| 4.5 / 5 | Turbine exit $p_0$, $T_0$ — **EGT** is measured here |
| 8 / 9 | Nozzle pressures |

**The TIT problem.** $T_{04}$ is the most important parameter in the engine
([L04](L04-combustion-thermodynamics-2.md), [L20](L20-turbines-2.md)) and is **essentially never
measured directly in service** — no probe survives 1,800 K in the gas path for thousands of hours.
Instead it's **inferred** from EGT (measured at station 4.5 or 5) plus the turbine work balance:

$$
T_{04} = T_{05} + \frac{c_{p,c}\left(T_{03}-T_{02}\right)}{\eta_m(1+f-b)\,c_{p,h}}
$$

This is exactly the relation from [L06](L06-thermodynamics-of-jet-engines.md) §7, used **backwards** as
a measurement technique. It's a nice illustration of why the work balance is worth knowing cold.

**Other instrumentation:** shaft speeds ($N_1$, $N_2$), vibration (accelerometers, for blade and
bearing health), strain gauges and tip-timing on rotating blades, and high-response pressure
transducers for surge and instability detection.

### 6. Performance analysis and correction to standard day

Raw test data is taken at whatever the ambient conditions were. To compare tests, everything is
**corrected to standard sea-level conditions**:

$$
F_{\text{corr}}=\frac{F}{\delta}, \qquad
\dot m_{\text{corr}}=\frac{\dot m\sqrt\theta}{\delta}, \qquad
N_{\text{corr}}=\frac{N}{\sqrt\theta}, \qquad
\mathrm{TSFC}_{\text{corr}}=\frac{\mathrm{TSFC}}{\sqrt\theta}
$$

$$
\theta = \frac{T_{02}}{288.15}, \qquad \delta = \frac{p_{02}}{101.325\ \mathrm{kPa}}
$$

**Note the TSFC correction is $1/\sqrt\theta$**, not $1/\delta$ — a common slip. It follows from
$\mathrm{TSFC}=\dot m_f/F$ with $\dot m_f \propto \delta\sqrt\theta$ and $F \propto \delta$.

**Engine performance is then plotted as corrected thrust vs. corrected speed or corrected fuel flow**,
and these curves are what get compared across builds, across the fleet, and against the model.

### 7. Engine health monitoring and gas path analysis

**The diagnostic idea:** each component's deterioration produces a **characteristic signature** in the
measured gas path parameters. Match the pattern, identify the fault.

| Fault | $N_2$ | EGT | Fuel flow | $p_{03}$ |
|---|---|---|---|---|
| **Compressor fouling** (dirt on blades) | ↓ | ↑ | ↑ | ↓ |
| **Compressor erosion** (tip clearance opening) | ↑ | ↑ | ↑ | ↓ |
| **Turbine damage** (eroded NGV, larger throat) | ↓ | ↑ | ↑ | ↓ |
| **Combustor liner distress** | ~ | ↑ or uneven | ~ | ~ |
| **Bleed leak** | ↑ | ↑ | ↑ | ~ |

**EGT margin** — the difference between the current EGT at takeoff and the certified redline. It is
**the** health metric for a commercial engine:

- A new engine has healthy EGT margin
- Deterioration (fouling, clearance opening, seal wear) erodes it over thousands of cycles
- **When EGT margin reaches zero, the engine must come off wing** for overhaul, regardless of whether
  anything is broken

**Why:** running past redline directly destroys turbine blade life by the Larson-Miller relation
([L20](L20-turbines-2.md) §7) — remember, +15 K halves blade life. EGT margin is a proxy for remaining
turbine life, and shop visit scheduling is built around it.

**Other monitoring tools:**
- **Vibration tracking** — bearing and rotor health, blade damage
- **Oil debris monitoring** — magnetic chip detectors and spectrometric oil analysis catch bearing and
  gear wear
- **Borescope inspection** — direct visual inspection of blades through access ports
- **Trend monitoring / FADEC data** — continuous parameter recording, with modern engines transmitting
  data in flight

### 8. Measurement uncertainty

**Bias (systematic)** — calibration errors, installation effects. Repeats don't reduce it; only better
calibration does.
**Precision (random)** — scatter. Reduced by averaging over $N$ samples as $1/\sqrt N$.

**Root-sum-square combination:**

$$
U = \sqrt{B^2 + \left(t_{95}\,S\right)^2}
$$

**Propagation through a derived quantity** $y = f(x_1,\ldots,x_n)$:

$$
U_y = \sqrt{\sum_i \left(\frac{\partial y}{\partial x_i}U_{x_i}\right)^2}
$$

**Why back-to-back testing works:** systematic biases largely cancel when you compare two configurations
on the same stand with the same instrumentation on the same day. The *difference* is far more accurate
than either *absolute* value. This is standard practice for evaluating a design change and is a good
answer to "how do you detect a 0.5% improvement with 0.5% uncertainty?"

---

## Worked logic — inferring TIT from measured data

**Given (test cell measurements):** $T_{02}=288$ K, $p_{02}=101.3$ kPa, $T_{03}=750$ K,
$p_{03}=2.03$ MPa, $T_{05}=1{,}050$ K (EGT), $\dot m_a = 60$ kg/s, $\dot m_f = 1.35$ kg/s,
bleed $b = 0.12$, $\eta_m = 0.99$, $c_{p,c}=1005$, $c_{p,h}=1150$ J/(kg·K).

**Step 1 — compressor work:**

$$
w_c = c_{p,c}\left(T_{03}-T_{02}\right)=1005(750-288)=464{,}310\ \mathrm{J/kg\ of\ core\ air}
$$

**Step 2 — fuel-air ratio:**

$$
f = \frac{1.35}{60}=0.0225
$$

**Step 3 — infer $T_{04}$ from the work balance:**

$$
T_{04}=T_{05}+\frac{c_{p,c}\left(T_{03}-T_{02}\right)}{\eta_m(1+f-b)\,c_{p,h}}
$$

$$
=1050 + \frac{464{,}310}{0.99(1+0.0225-0.12)(1150)} = 1050+\frac{464{,}310}{0.99(0.9025)(1150)}
$$

$$
=1050+\frac{464{,}310}{1027.5}=1050+451.9 = 1{,}502\ \mathrm{K}
$$

**Step 4 — cross-check with the combustor energy balance.** Independent route, using
$Q_R = 43$ MJ/kg, $\eta_b=0.99$:

$$
T_{04}=T_{03}+\frac{f\,\eta_b\,Q_R}{(1+f)c_{p,h}}=750+\frac{0.0225(0.99)(43\times10^6)}{1.0225(1150)}
$$

$$
=750+\frac{957{,}825}{1175.9}=750+814.5=1{,}565\ \mathrm{K}
$$

**Step 5 — reconcile the 63 K discrepancy.** Two independent estimates disagree by ~4%. That's not a
failure — it's **diagnostic information**, and interpreting it is the point of the exercise:

- The combustor balance ignores that **bleed air rejoins downstream**, diluting the gas before the
  turbine. The **rotor inlet temperature** is genuinely lower than the combustor exit temperature
  ([L20](L20-turbines-2.md) §6) — so the work-balance number (1,502 K) is closer to the *effective*
  turbine inlet temperature, while 1,565 K is closer to the true combustor exit.
- Constant $c_p$ values are approximations across a 750 K span.
- $\eta_b$ and $\eta_m$ are assumed, not measured.

**Step 6 — the engineering takeaway.** Two independent estimates that agree to 4% is a **good** result
and is exactly how test data is validated. If they disagreed by 15%, you'd suspect an instrumentation
fault, a bleed measurement error, or an incorrect $\eta_b$ — and you'd investigate before trusting
either number.

**This cross-checking discipline — computing the same quantity two ways and interrogating the gap — is
the core skill of experimental engine work**, and a very defensible thing to say in an exam answer.

---

## Worked logic — full data reduction from an altitude test point

*Cross-referenced from a parallel offering's in-class problem — this is the complete pipeline a real
altitude-cell calibration runs, condensed.* A turbojet is tested at 0.2 $M_n$, sea level, with measured
$P_2=15.11$ psia, $T_2=522.8°\mathrm R$, thrust $=17{,}100$ lbf, fuel LHV $=18{,}400$ Btu/lbm,
$P_{25}=45.0$ psia, $T_{25}=660°\mathrm R$, fuel flow $=2.56$ pps, $T_3=1309.7°\mathrm R$,
$P_3=400$ psia, $P_5=42.0$ psia, $T_5=1939.7°\mathrm R$, $FP_4=12.0$, cooling/leakage fractions 27%
(1st turbine) + 8% (bore/2nd turbine/leakage), burner loss 5%, burner $c_p=0.264$ Btu/(lbm·°R).

**The chain of derivation — note that nothing here is measured directly except pressures, temperatures,
fuel flow, and thrust; everything else is calculated:**

1. **Inlet airflow** from the pitot/bellmouth method (§4 above): $\dot m_2 = 238.7$ lbm/s,
   $W_{2c}=233.1$ pps.
2. **Combustor temperature rise** from the fuel-air ratio and LHV
   ([L03](L03-combustion-thermodynamics-1.md) §6): $\Delta T = f\,\mathrm{LHV}/[(1+f)c_p] = 1{,}766°\mathrm F$,
   giving $T_4 = T_3+\Delta T$.
3. **Core airflow from the choked-NGV flow parameter**, worked *backwards* from what
   [corrected-parameters](../../concepts/corrected-parameters.md) uses forwards for matching:
   $\dot m_4 = FP_4\, P_4/\sqrt{T_4}$, then correct forward through the known cooling/leakage
   fractions to get $\dot m_3$, $\dot m_{2.5}$.
4. **Pressure ratios**: $\mathrm{OPR}=P_3/P_2=26.5$, $\mathrm{CPR}=P_3/P_{25}=8.89$,
   $\mathrm{EPR}=P_5/P_2=2.78$.
5. **Component efficiencies**, from the same isentropic-efficiency definitions as
   [propulsion-efficiencies](../../concepts/propulsion-efficiencies.md):
   $\eta_c = \left[(\mathrm{CPR})^{(\gamma-1)/\gamma}-1\right]/(\mathrm{CTR}-1) = 0.82$,
   $\eta_t = \left[1-T_5/T_4\right]/\left[1-(P_5/P_4)^{(\gamma-1)/\gamma}\right] = 0.88$.
6. **Nozzle exit velocity** from the isentropic expansion relation
   ([L13](L13-nozzles.md)): $V_e \approx 2{,}446$ ft/s.
7. **The performance triad**: specific thrust $F_s=71.0$ lbf/(lbm/s), TSFC $=0.54$ lbm/(lbf·hr),
   thermal efficiency $\eta_{th}=0.25$, propulsive efficiency $\eta_p=0.16$ (low — this is a low-bypass
   turbojet at only $M=0.2$, exactly the regime where Froude efficiency is worst — see
   [propulsion-efficiencies](../../concepts/propulsion-efficiencies.md)), overall $\eta_o=0.04$.

**Why this example matters more than its arithmetic:** it demonstrates that essentially **every cycle
quantity from L06–L21 is, in practice, an *inferred* quantity** — built from a handful of directly
measured pressures/temperatures/flows through exactly the relations this wiki has been deriving all
semester. Testing isn't a separate topic tacked onto the end of the course; it's the empirical
validation of every equation that came before it.

---

## Common pitfalls

- **Forgetting thrust stand corrections.** Tare, cell pressure, and buoyancy are all significant.
- **Correcting TSFC by $\delta$ instead of $\sqrt\theta$.**
- **Believing $T_{04}$ is measured directly.** It's inferred.
- **Confusing bias with precision uncertainty.** Averaging fixes only the latter.
- **Comparing absolute values across facilities.** Use back-to-back testing.
- **Assuming an altitude cell reproduces inlet flow.** Direct-connect bypasses the inlet entirely.
- **Treating EGT margin as an efficiency metric.** It's a *life* metric.
- **Reporting more significant figures than the uncertainty supports.**
- **Ignoring bleed in the work balance.** $(1+f-b)$, not $(1+f)$.

---

## Exam checklist

- [ ] List reasons engine testing is unavoidable, including certification requirements
- [ ] Compare sea-level, altitude cell, flying test bed, and rig testing
- [ ] **Explain why matching $\theta$ and $\delta$ on the ground reproduces flight aerodynamics**
- [ ] List thrust stand corrections and state typical achievable uncertainty
- [ ] Describe bellmouth airflow measurement and Coriolis fuel measurement
- [ ] Combine measurement uncertainties by root-sum-square through TSFC
- [ ] **Explain why $T_{04}$ is inferred rather than measured, and do the inference**
- [ ] Write the standard-day correction factors, including the $1/\sqrt\theta$ on TSFC
- [ ] **Give the gas path signature of compressor fouling vs. turbine damage**
- [ ] **Define EGT margin and explain why it drives shop visits** (link to Larson-Miller)
- [ ] Distinguish bias from precision; explain why back-to-back testing beats absolute measurement

---

## Links

- Previous: [L24 — Rocket Engines 2](L24-rocket-engines-2.md)
- Next: [L26 — Course Takeaways](L26-course-takeaways.md)
- Corrected parameters: [L16](L16-compressors-3.md), [L21](L21-turbines-3.md), [corrected-parameters](../../concepts/corrected-parameters.md)
- Work balance used backwards: [L06](L06-thermodynamics-of-jet-engines.md)
- Blade life: [L20 — Turbines 2](L20-turbines-2.md)
- Concept: [station-numbering](../../concepts/station-numbering.md)
- Course hub: [EAS4300](../EAS4300.md)
