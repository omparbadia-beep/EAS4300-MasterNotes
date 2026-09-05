# L09 — Engine / Aircraft Performance

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 9 · **Date:** Fri 25 Sep 2026
**Book §:** 5.7 *Typical Engine Performance* (p. 196) — and almost certainly **5.8
*Engine-Aircraft Matching*** (p. 202), which is what this lecture's title describes

> 📖 **Reconciled 2026-08-25.** The syllabus cites only 5.7, but the topic name "Engine/aircraft
> performance" matches **§5.8 Engine-Aircraft Matching** exactly. **Read 5.7–5.8 together** — 5.7 gives
> the performance data and trends, 5.8 does the matching analysis this page is built around.
> See [textbook-section-map](textbook-section-map.md).
**Tags:** #thrust-lapse #breguet #range-equation #thrust-matching #installed-thrust #flight-envelope #drag-polar #off-design

---

## Why this lecture matters

Lectures 6–8 treated the engine in isolation. This one **couples it to the airframe**. An engine that
looks excellent on a test stand can be the wrong engine for an aircraft, because thrust available and
thrust required vary differently with altitude and Mach. This is also the last lecture before the
component chapters, and the last one on Midterm 1.

---

## Core concepts

### 1. Thrust required — the airframe's demand

In steady level flight, thrust equals drag and lift equals weight:

$$
F = D, \qquad L = W
$$

With the standard parabolic **drag polar**:

$$
C_D = C_{D0} + \frac{C_L^2}{\pi e AR} = C_{D0} + K C_L^2
$$

$$
D = \tfrac{1}{2}\rho u^2 S\, C_{D0} + \frac{2KW^2}{\rho u^2 S}
$$

**Two competing terms — the classic U-shaped curve:**
- **Parasite drag** $\propto u^2$ — dominates at high speed
- **Induced drag** $\propto 1/u^2$ — dominates at low speed

**Minimum drag** occurs where they're equal, which gives the best lift-to-drag ratio:

$$
\left(\frac{L}{D}\right)_{\max} = \frac{1}{2\sqrt{K C_{D0}}}
$$

$$
u_{\text{min drag}} = \left(\frac{2W}{\rho S}\right)^{1/2}\left(\frac{K}{C_{D0}}\right)^{1/4}
$$

Typical $(L/D)_{max}$: airliner 17–20, fighter 8–10, glider 40–60.

### 2. Thrust available — thrust lapse

Engine thrust **falls with altitude** (lower density ⇒ lower mass flow) and **changes with Mach**
(ram drag vs. ram compression compete).

**Altitude lapse**, approximately:

$$
\frac{F}{F_{SL}} \approx \left(\frac{\rho}{\rho_{SL}}\right)^n, \qquad n \approx 0.7\text{–}1.0
$$

$n$ is closer to 1 in the troposphere and larger above the tropopause where temperature is constant.

**Mach dependence** — different for different engine types, and this is heavily examined:

| Engine | Thrust vs. $M_0$ |
|---|---|
| **Turbojet** | Roughly flat, slight rise at high $M$ (ram compression offsets ram drag) |
| **High-bypass turbofan** | **Falls significantly** — big slow bypass stream loses effectiveness fast as $u_0$ rises |
| **Ramjet** | Rises steeply then collapses (see [L07](L07-ramjets.md)) |
| **Turboprop** | Falls sharply — propeller efficiency drops with speed |
| **Rocket** | Independent of $M_0$ |

**Why turbofan thrust lapses with Mach:** bypass thrust is $\dot m_b(u_{19}-u_0)$. With $u_{19}$ only
~350–400 m/s, as $u_0$ climbs toward 250+ m/s the increment shrinks fast. The high-bypass turbofan is
optimized for one narrow speed band and degrades outside it.

**Corrected parameters** ([corrected-parameters](../../concepts/corrected-parameters.md)) collapse this
into standardized form:

$$
\theta = \frac{T_{02}}{T_{\text{ref}}}, \qquad \delta = \frac{p_{02}}{p_{\text{ref}}}
$$

$$
\frac{F}{\delta} = \text{fn}\left(\frac{N}{\sqrt\theta}\right), \qquad
\frac{\dot m \sqrt\theta}{\delta} = \text{fn}\left(\frac{N}{\sqrt\theta}\right)
$$

### 3. Matching — where the curves cross

Plot **thrust available** and **thrust required** vs. flight speed at a given altitude:

- **Intersections** are the possible steady level flight speeds. There are usually **two**: a slow one
  (induced-drag-limited, on the "back side of the power curve") and a fast one.
- **The gap between them** is **excess thrust**, which is what buys climb rate and acceleration.
- **The highest altitude where the curves merely touch** is the **absolute ceiling** — excess thrust
  is zero, no climb possible.
- **Service ceiling** is conventionally where climb rate falls to 100 ft/min (0.5 m/s).

**Rate of climb** from an energy balance:

$$
\mathrm{RC} = \frac{(F-D)\,u}{W}
$$

**Specific excess power** — the fighter-pilot metric, which folds climb and acceleration together:

$$
P_s = \frac{(F-D)u}{W} = \frac{dh}{dt} + \frac{u}{g}\frac{du}{dt}
$$

$P_s$ contours on an altitude-Mach plot define the **flight envelope**, and the $P_s = 0$ contour is
its boundary. This is how air combat maneuvering performance is actually specified.

### 4. The Breguet range equation

**The most important result in the lecture.** Start from the weight loss rate:

$$
\frac{dW}{dt} = -\dot m_f g_0 = -\,\mathrm{TSFC}\cdot F \cdot g_0
$$

In cruise, $F = D = W/(L/D)$. Range is $\int u\,dt$:

$$
dR = u\,dt = -\frac{u\,(L/D)}{\mathrm{TSFC}\; g_0}\frac{dW}{W}
$$

Integrating with $u$, $L/D$, TSFC held constant:

$$
\boxed{\ R = \frac{u}{g_0\,\mathrm{TSFC}}\left(\frac{L}{D}\right)\ln\frac{W_i}{W_f}\ }
$$

In terms of $I_{sp}$ (equivalent, and the form that connects to rockets):

$$
R = I_{sp}\left(\frac{L}{D}\right) u \cdot \frac{1}{g_0}\cdot \ln\frac{W_i}{W_f}
\qquad\text{(with }I_{sp}=1/(g_0\mathrm{TSFC})\text{)}
$$

**The four factors, and who owns each:**

| Factor | Owner | Typical value |
|---|---|---|
| $u/\mathrm{TSFC}$ | **Propulsion** | Maximize — the whole reason for the turbofan |
| $L/D$ | **Aerodynamics** | 17–20 for airliners |
| $\ln(W_i/W_f)$ | **Structures** | Fuel fraction — lighter structure = more fuel |
| $1/g_0$ | Nature | — |

**The three disciplines multiply.** No amount of engine improvement rescues a bad airframe, and vice
versa. This equation is why aircraft design is inherently a multidisciplinary optimization, and it's
the single most quotable result in the course.

**Note the $u$ in the numerator.** Faster flight helps range *directly*, but from
[L06](L06-thermodynamics-of-jet-engines.md), $\mathrm{TSFC} = u_a/(\eta_o Q_R)$, so
$u/\mathrm{TSFC} = \eta_o Q_R$ — **speed cancels exactly**, and range depends on $\eta_o$, not on speed
per se. Faster is free *if* you can hold $\eta_o$ and $L/D$. In practice both degrade near and above
$M_{crit}$, which is what sets cruise Mach at ~0.85 for airliners.

**Endurance** (loiter time), by contrast, drops the $u$:

$$
E = \frac{1}{g_0\,\mathrm{TSFC}}\left(\frac{L}{D}\right)\ln\frac{W_i}{W_f}
$$

Best **endurance** is at max $L/D$; best **range** is at max $u(L/D)$, which occurs at a *higher* speed —
about 1.32× the min-drag speed for a jet. **Loiter slow, cruise faster.**

### 5. Installed vs. uninstalled thrust

Everything in [L06](L06-thermodynamics-of-jet-engines.md)–[L08b](L08b-turbofans.md) was **uninstalled**
thrust — a bare engine on a test stand. Real installations lose some of it:

$$
F_{\text{installed}} = F_{\text{uninstalled}} - D_{\text{nacelle}} - D_{\text{spillage}} - D_{\text{bleed}} - D_{\text{interference}}
$$

- **Nacelle/cowl drag** — skin friction and pressure drag on the pod
- **Spillage drag** — when the inlet captures less air than its stream tube would suggest, the excess
  spills around and costs momentum ([L10](L10-inlets.md))
- **Bleed and power extraction** — cabin air, anti-ice, generators, hydraulics all take compressor air
  or shaft power, typically costing several percent of thrust
- **Interference drag** — pylon/wing interaction

Installation losses of **5–10%** are typical, and up to 15% for a poorly-integrated supersonic inlet.
**Never compare a manufacturer's uninstalled thrust rating to an airframe drag number directly.**

### 6. Off-design and throttle behavior

An engine spends almost all its life **off design point**. Key operating conditions:

| Condition | Characteristic |
|---|---|
| **Takeoff** | Max thrust, $M\approx0$–0.3, sea level. Sets TIT and mechanical limits. |
| **Climb** | High thrust, increasing altitude, roughly constant $M$ |
| **Cruise** | Design point for civil engines. ~85–90% of a long flight. |
| **Descent/idle** | Very low power, poor efficiency, stability concerns |
| **Loiter** | Endurance-optimized, max $L/D$ |

**Throttling** reduces fuel flow, which lowers $T_{04}$, which reduces turbine work, which slows the
spool, which reduces $\pi_c$ and $\dot m$. All coupled through the component maps
([L16](L16-compressors-3.md), [L21](L21-turbines-3.md)). Thrust falls faster than fuel flow, so
**TSFC gets worse at part power** — which is why airlines cruise at high power settings, and why
descent is thermodynamically wasteful.

### 7. Flight envelope limits

The boundaries of the altitude-Mach chart, and what sets each:

- **Low speed:** stall ($C_{L,max}$) — an airframe limit
- **High speed, low altitude:** dynamic pressure $q$ (structural) and skin temperature
- **High speed, high altitude:** thrust available = drag (propulsion limit)
- **High altitude:** absolute ceiling; also combustor stability and relight limits (low $p$ and $T$
  make the flame hard to sustain — see [L11](L11-combustors.md))
- **Temperature:** TIT limit at takeoff on a hot day — **flat rating** means the engine is derated so
  it delivers constant thrust up to a reference temperature, protecting TIT margin

---

## Worked logic — range of a transport aircraft

**Given:** $W_i = 350$ kN, $W_f = 250$ kN, cruise $M_0 = 0.85$ at 11 km ($T = 217$ K),
$L/D = 18$, TSFC $= 1.6\times10^{-5}$ kg/(N·s).

**Step 1 — cruise speed:**

$$
a = \sqrt{1.4\times287\times217}=295.2\ \mathrm{m/s}, \qquad u = 0.85\times295.2 = 251\ \mathrm{m/s}
$$

**Step 2 — Breguet:**

$$
R = \frac{251}{9.81\times1.6\times10^{-5}}\times 18 \times \ln\frac{350}{250}
$$

$$
\frac{251}{1.5696\times10^{-4}} = 1.599\times10^6\ \mathrm{m}
$$

$$
R = 1.599\times10^6 \times 18 \times \ln(1.4) = 1.599\times10^6\times18\times0.3365
$$

$$
R = 9.69\times10^6\ \mathrm{m} \approx 9{,}690\ \mathrm{km}
$$

Roughly 5,230 nautical miles — a realistic long-haul figure.

**Step 3 — sensitivity, which is the real lesson.** Each factor enters linearly (or logarithmically):

- **10% better TSFC** ⇒ 10% more range ⇒ +970 km
- **10% better $L/D$** ⇒ 10% more range ⇒ +970 km
- **10% more fuel** ($W_f = 240$ kN) ⇒ $\ln(1.458)=0.377$ ⇒ +12% ⇒ +1,150 km

Note the fuel-fraction term is **logarithmic**, so it has diminishing returns — doubling fuel does not
double range. Aerodynamic and propulsive gains are linear and therefore more valuable per percent.
**This is why a 1% TSFC improvement is worth enormous engineering investment in this industry.**

---

## Worked logic — engine diameter's hidden cost to range

*Cross-referenced from a parallel offering's worked example. Counterintuitive result: a physically
bigger engine can **reduce** range even before you touch TSFC, purely through drag.*

**Given:** a transport aircraft, base engine nacelle 60″ fan diameter, engine drag = 7% of total
aircraft drag, base $L/D=11.9$, cruise TSFC $=0.55$ lbm/(lbf·hr), $M=0.81$ at 30,000 ft
($T_a=411.7°\mathrm R$), $W_i/W_e = 1.524$ (from fuel-burn accounting). **Base range** (Breguet, in
knots and hours):

$$
V = M\sqrt{\gamma R g_c T_a} = 806\ \mathrm{ft/s} = 477\ \mathrm{kt}
$$

$$
R_{\text{base}} = \frac{V}{\mathrm{TSFC}}\times\frac{L}{D}\times\ln\frac{W_i}{W_e}
= \frac{477}{0.55}\times11.9\times\ln(1.524) = 4{,}350\ \mathrm{NM}
$$

**Now propose an 80″ fan** (bigger, presumably more efficient core — but assume TSFC is *unchanged* to
isolate the drag effect). Nacelle drag scales roughly with **frontal area**, i.e. diameter squared:

$$
\left(\frac{80}{60}\right)^2 = 1.78
$$

$$
\text{New engine drag fraction} = \underbrace{(1-0.07)}_{\text{rest of A/C}} + 0.07\times1.78 = 1.0544
$$

**Total aircraft drag rises ~5.4%**, so $L/D$ falls proportionally: $L/D_{\text{new}} = 11.9/1.0544 =
11.29$. Recomputing range with the slightly heavier engine's mass also folded into $W_i/W_e$:

$$
R_{\text{new}} = \frac{477}{0.55}\times11.29\times\ln(1.514) \approx 4{,}278\ \mathrm{NM}
$$

**Range fell by ~72 NM (1.7%) from the diameter increase alone**, before any TSFC benefit is even
credited. This is the concrete version of the L18 §6b/§7 point: a bigger fan buys propulsive
efficiency ([propulsion-efficiencies](../../concepts/propulsion-efficiencies.md)) but the nacelle drag
and weight it drags along are a real, quantifiable tax — **the diameter decision is a system-level
optimization, not a "bigger fan is always better" rule.**

**A second real airline-economics wrinkle** (cross-referenced from a prior Anup Mannem-taught
offering, same problem family): drag can be modeled as scaling with **fan pressure ratio** rather than
diameter, e.g. $D \propto (0.92+0.08\,\mathrm{FPR}^2)$, and a full engine-selection recommendation has
to weigh range **against overhaul cost**, which itself scales with the **number of turbomachinery
stages** an engine needs to reach its OPR (see [L14](L14-compressors-1.md)'s "why 10 compressor
stages" argument — a higher-OPR engine literally needs more hardware, and more hardware means a more
expensive overhaul). In the source problem, engine B gives ~2.5% more range than engine A but at
~30 percentage points higher overhaul cost — the worked recommendation picks the **lower-range,
lower-maintenance-cost** engine unless the extra range unlocks routes the airline actually needs.
**The general lesson**: every engine performance number this course derives (range, TSFC, specific
thrust) eventually has to be weighed against a **cost of ownership** that a purely aerodynamic/
thermodynamic analysis never touches.

## Worked logic — why a more "efficient" engine doesn't always mean more range

*Cross-referenced from the same worked example set — isolates the opposite failure mode: better TSFC
that still loses.*

**Given:** a much larger aircraft (illustrating the same principle at any scale), base configuration
with $L/D=11.9$, TSFC $=0.56$ lbm/(lbf·hr), giving $R_{\text{base}} = 2{,}505$ NM. A **re-engined**
version has **1% better TSFC** ($0.5544$) but each of the 4 engines is **heavier** (the extra weight
comes straight out of the fuel-fraction term, since more structural/engine weight at a fixed takeoff
weight means less usable fuel):

$$
R_{\text{re-engined}} = \frac{488}{0.5544}\times11.9\times\ln(1.269) \approx 2{,}494\ \mathrm{NM}
$$

**Range went down**, despite a real, certified 1% TSFC improvement — because the heavier engines ate
into the fuel fraction $\ln(W_i/W_e)$ by more than TSFC gave back. **The takeaway the instructor
explicitly draws: "more efficient engines do not [necessarily] increase range."** Every engine
performance metric in this course — TSFC, propulsive efficiency, specific thrust — is only ever *one*
input to an aircraft-level trade that also includes weight and drag. This is the single best
illustration in the whole course of why L09 is titled "Engine/**Aircraft**" performance, not just
"Engine performance."

---

## Common pitfalls

- **Forgetting thrust lapses with altitude.** Sea-level static thrust is not cruise thrust; the ratio
  can be 4–5:1.
- **Assuming turbofan thrust is Mach-independent.** It falls substantially — more than a turbojet's.
- **Using uninstalled thrust in an aircraft performance calculation.** Subtract installation losses.
- **Mixing up range and endurance conditions.** Range: max $u(L/D)$. Endurance: max $L/D$, slower.
- **Unit errors in Breguet.** TSFC in kg/(N·s) with $g_0$ present, or in 1/s without — pick one and be
  consistent. This is the most common numerical error on this topic.
- **Assuming constant $L/D$ over a long cruise.** As fuel burns, weight drops and optimum altitude
  rises — hence step climbs and cruise-climb profiles.
- **Treating the two thrust-required intersections as equivalent.** The slow one is on the back side of
  the power curve and is speed-unstable.
- **Ignoring bleed and power extraction.** They're a real thrust and TSFC penalty.

---

## Exam checklist

- [ ] Write the parabolic drag polar and derive $(L/D)_{max}$
- [ ] Sketch thrust required vs. speed, identify parasite/induced regimes and min drag
- [ ] Sketch thrust available for turbojet, turbofan, ramjet, rocket vs. Mach and explain each
- [ ] Explain thrust lapse with altitude and give the approximate density exponent
- [ ] Identify matching points, excess thrust, absolute vs. service ceiling
- [ ] **Derive the Breguet range equation from $dW/dt = -\mathrm{TSFC}\cdot F\cdot g_0$**
- [ ] Name the three engineering disciplines owning the three Breguet factors
- [ ] Explain why range is nearly speed-independent via $u/\mathrm{TSFC} = \eta_o Q_R$
- [ ] Distinguish range-optimal from endurance-optimal flight
- [ ] List installation losses and give a typical magnitude
- [ ] Explain why TSFC worsens at part power

---

## Links

- Previous: [L08b — Turbofans](L08b-turbofans.md)
- **Last topic on Midterm 1** → [exam-midterm-1](exam-midterm-1.md)
- Next: [L10 — Inlets](L10-inlets.md) — starts the component half of the course
- Concept: [corrected-parameters](../../concepts/corrected-parameters.md)
- Concept: [propulsion-efficiencies](../../concepts/propulsion-efficiencies.md)
- Course hub: [EAS4300](../EAS4300.md)
