# L16 — Axial Compressors 3: Maps, Stall, and Surge

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 16 · **Date:** Mon 19 Oct 2026
**Book §:** 7.6 *Boundary Layer Limitations* (p. 303) — ✅ verified against the book · **HW6 assigned**

> 📖 **Reconciled 2026-08-25.** §7.6 is titled **"Boundary Layer Limitations."** It is the book's
> answer to *"how much pressure rise can one stage actually deliver before the flow separates?"* —
> de Haller, diffusion factor, and end-wall boundary layers. **A new §0 below covers exactly that**;
> it was the one genuinely missing piece in this course's compressor material.
>
> The **maps, stall, and surge** content that fills the rest of this page belongs to **§7.4–7.5**,
> which the syllabus assigns to [L15](L15-compressors-2.md). Read the two pages together.
> See [textbook-section-map](textbook-section-map.md).
**Tags:** #compressor-map #surge #rotating-stall #surge-margin #corrected-parameters #choke #operating-line #variable-stators #bleed-valve #stall-cell

---

## Why this lecture matters

A compressor map is how a real engine is actually characterized, controlled, and certified. Surge is
the compressor's characteristic failure mode and the reason variable stators, bleed valves, and
multiple spools exist. This lecture is where the aerodynamics of
[L14](L14-compressors-1.md)–[L15](L15-compressors-2.md) becomes engine *behavior*.

---

## Core concepts

### 0. Boundary layer limitations (§7.6 — the assigned section)

**The question this section answers:** a compressor stage can be given any velocity triangle you like
on paper. What actually stops you from asking for more pressure rise per stage?

**Answer: the blade and end-wall boundary layers separate.** A compressor blade passage is a
**diffuser** — it decelerates the flow to raise static pressure, so it runs against an **adverse
pressure gradient**. Boundary layers in adverse gradients thicken and eventually separate. Ask for too
much diffusion in one row and you get stall, not pressure.

This is the deepest asymmetry in the whole course, and §7.6 is where the book makes it quantitative:

> **A turbine blade passage accelerates the flow (favorable gradient) and can turn it 70–120° in one
> row. A compressor blade passage decelerates it (adverse gradient) and can manage only 20–45°.**
> Hence 10–15 compressor stages to undo what 1–2 turbine stages produce.

#### The de Haller number — the quick screen

The crudest and most-used criterion. Limit the **relative velocity ratio** across a blade row:

$$
\mathrm{DH} = \frac{W_2}{W_1} \ \ge\ 0.72
$$

Below ~0.72 the diffusion is too aggressive and separation is likely. **Check this on every compressor
row you design** — a triangle can be geometrically valid and aerodynamically impossible.

#### The diffusion factor — the better criterion

De Haller ignores blade loading and how many blades share it. Lieblein's **diffusion factor** adds
both, via the solidity $\sigma = c/s$ (chord over spacing):

$$
D = 1 - \frac{W_2}{W_1} + \frac{\Delta W_w}{2\,\sigma\,W_1} \ \le\ 0.6
$$

The second term is the **loading per blade**: the same total turning spread over more blades (higher
$\sigma$) is safer. **$D \le 0.6$ is the general limit; $D \le 0.45$ is prudent near the hub and tip**,
where end-wall boundary layers are already thick.

**The design lever:** if $D$ comes out too high, either reduce the turning (less work per stage, so
more stages) or increase solidity (more/longer blades, so more weight and more friction area).
That trade is the whole reason compressors have the blade counts they do.

#### End-wall boundary layers and the work-done factor

The blade surfaces aren't the only problem. Boundary layers on the **hub and casing** grow through the
machine, and by the rear stages they occupy a large fraction of a short blade's span. Consequences:

- **Axial velocity is not uniform** across the span — it's depressed near the walls and higher in the
  mid-span, so the real triangles differ from the design ones.
- **The stage delivers less work than Euler predicts.** Captured empirically by the **work-done
  factor** $\lambda$:

$$
\Delta T_0 = \frac{\lambda\, U \Delta C_w}{c_p}
$$

with $\lambda \approx 0.98$ in the first stage, falling to ~0.85–0.83 by the later stages as the end-wall
layers thicken. **It is a loss of work input, not an efficiency** — do not conflate the two.

- **Tip clearance leakage.** Flow escapes over the unshrouded rotor tip from pressure side to suction
  side, rolling into a vortex that blocks the passage and triggers stall early. Sensitivity is brutal:
  roughly **1.5–3% of stage efficiency lost per 1% of span in clearance.** Rear stages of a
  high-pressure compressor have blades only a few cm tall, so a fixed manufacturing clearance is a
  much larger *fractional* clearance there — which is why the rear stages set the surge line.

#### Why this section is the foundation of everything else on this page

**§7.6 explains where the surge line on the map comes from.** The map (§7.4–7.5) is the *measured*
consequence; boundary layer separation is the *mechanism*. When you push toward surge you are
increasing incidence on the blades, raising $D$ past its limit, and separating the suction surfaces.

Rotating stall, surge, and the stall margin discussed in §3–§7 below are all this same phenomenon at
different scales. Keep the causal chain straight:

$$
\text{adverse gradient} \to \text{high } D \to \text{separation} \to \text{rotating stall} \to \text{surge}
$$

### 1. Corrected parameters — why maps use them

A compressor's performance depends on inlet conditions, which vary enormously across the flight
envelope. **Corrected parameters** collapse that dependence so one map covers all conditions.

Reference conditions (standard sea-level day):

$$
\theta = \frac{T_{02}}{288.15\ \mathrm{K}}, \qquad
\delta = \frac{p_{02}}{101.325\ \mathrm{kPa}}
$$

**Corrected mass flow:**

$$
\dot m_{\text{corr}} = \frac{\dot m\sqrt\theta}{\delta}
$$

**Corrected speed:**

$$
N_{\text{corr}} = \frac{N}{\sqrt\theta}
$$

**Where these come from** — dimensional analysis, but the physical reading matters more:

- $\dot m\sqrt\theta/\delta$ is essentially the **inlet Mach number / flow function** from
  [L05](L05-gas-dynamics.md) §4. Same corrected flow ⇒ same $M$ at the compressor face ⇒ same
  velocity triangles.
- $N/\sqrt\theta$ is proportional to **$U/a$ — blade Mach number.** Same corrected speed ⇒ same
  $U/C_a$ ratio ⇒ same triangles again.

**The whole point:** hold the corrected parameters fixed and the *aerodynamics* are identical
regardless of altitude or day temperature. That's what makes a single map valid everywhere.

$$
\pi_c, \ \eta_c = \text{fn}\left(\dot m_{\text{corr}},\ N_{\text{corr}}\right)
$$

Full detail: [corrected-parameters](../../concepts/corrected-parameters.md).

### 2. Reading a compressor map

Axes: **corrected mass flow** (x) vs. **pressure ratio** (y).

**Features:**

- **Speed lines** — one curve per $N_{corr}$. At low speed they're shallow; at high speed nearly
  vertical.
- **Choke (vertical right end)** — the flow chokes somewhere in the machine and mass flow cannot
  increase regardless of how much you drop the back pressure. The speed line goes vertical.
- **Surge line** — the locus of surge onset, bounding the map on the **left** (low flow, high pressure
  ratio). **You cannot operate to the left of it.**
- **Efficiency islands** — closed contours of $\eta_c$, with the peak near the design point.
- **Operating line** — where the engine actually runs, set by the downstream components (turbine
  nozzle and exhaust nozzle areas), *not* by the compressor.

**Why speed lines steepen at high speed:** at high $N_{corr}$ the front stages approach choking, so
mass flow becomes nearly independent of pressure ratio.

### 3. Surge margin

$$
\mathrm{SM} = \frac{\left(\pi_c/\dot m_{\text{corr}}\right)_{\text{surge}} - \left(\pi_c/\dot m_{\text{corr}}\right)_{\text{op}}}
{\left(\pi_c/\dot m_{\text{corr}}\right)_{\text{op}}}\times100\%
$$

A simpler and very common definition at constant corrected flow:

$$
\mathrm{SM} = \frac{\pi_{\text{surge}}-\pi_{\text{op}}}{\pi_{\text{op}}}\times100\%
$$

**Typical requirement: 15–25% at all steady operating points.**

**What eats surge margin:**

| Consumer | Effect |
|---|---|
| **Inlet distortion** ([L10](L10-inlets.md)) | 5–10% — the biggest single item |
| **Transient acceleration** | Fuel added before the spool speeds up ⇒ operating line jumps up |
| **Deterioration** (tip clearance opening with age) | Several % over engine life |
| **Manufacturing tolerances** | A few % |
| **Bleed extraction, power offtake** | Varies |
| **Reingestion, crosswind, hot gas** | Transient spikes |

**Surge margin is a budget**, and it's spent on all of these simultaneously. This is why engines are
designed with more margin than the steady operating point appears to need.

### 4. Rotating stall vs. surge — the distinction that gets examined

These are **different phenomena** and confusing them is a classic error.

**Rotating stall** — a *local*, *circumferential* instability.

- One or more **stall cells** (regions of separated, blocked flow) form and **rotate around the annulus
  at 20–70% of rotor speed** — always slower than the rotor, and in the same direction.
- **Annulus-averaged flow remains steady and forward.** The engine may keep running.
- Mechanism: a locally stalled passage blocks flow, diverting it to neighbouring passages. That
  *increases* incidence on the passage ahead (stalling it) and *decreases* it on the passage behind
  (unstalling it) — so the cell propagates.
- **Consequence:** severe blade vibration (each blade is excited once per cell passage), efficiency
  collapse, and rapid overheating downstream. It can be **stable** and self-sustaining, which is why
  "rotating stall" can persist rather than immediately clearing.

**Surge** — a *global*, *axial*, system-level instability.

- The **entire annulus** oscillates axially. Flow can **reverse** through the whole compressor.
- Frequency 3–10 Hz (a Helmholtz oscillation of the compressor + downstream volume — the combustor
  plenum acts as the compliance).
- Accompanied by loud bangs, flames from the inlet or tailpipe, and severe blade and thrust-bearing
  loads.
- **Can destroy an engine in seconds** and always requires immediate throttle reduction.

**Relationship:** rotating stall is often the *precursor* — a stall cell grows until the machine can no
longer sustain the pressure rise, and the system surges. Whether a compressor goes into stable
rotating stall or straight into surge depends on the downstream volume and the shape of the
characteristic.

**Mild surge vs. deep surge:** mild surge is a pressure oscillation without flow reversal; deep surge
includes full reversal. Both are unacceptable in service.

### 5. The stage matching problem — why multistage compressors are hard

**This is the deep reason for variable geometry, and a favorite exam question.**

Density rises through the compressor, so to keep axial velocity roughly constant, annulus area must
shrink:

$$
\rho C_a A = \text{const}
$$

The area is fixed by the hardware at the **design point**. Off-design, it's wrong:

**At low speed (starting, idle):**
- Pressure ratio is far below design, so density in the rear stages is **much lower** than design
- The rear annulus (sized for high density) is now **too large** ⇒ $C_a$ in the rear is too **low**
- Low $C_a$ at fixed $U$ means high incidence in the rear... but the *front* stages see the opposite

More precisely, the classic result:

| Speed | Front stages | Rear stages |
|---|---|---|
| **Below design** | **Stalled** (too much incidence, low $C_a/U$) | **Choked/windmilling** (too little incidence) |
| **Above design** | Choked | Stalled |

**Both ends are in trouble, in opposite ways, simultaneously.** A single-spool fixed-geometry compressor
with high pressure ratio simply cannot be started or accelerated.

**The three fixes:**

1. **Variable stator vanes (VSVs).** Rotate the IGV and front stator vanes to reduce pre-swirl at low
   speed, restoring acceptable incidence on the front rotors. Standard on all modern HP compressors —
   typically the first 3–5 rows are variable.
2. **Bleed valves.** Dump air from the middle of the compressor overboard at low speed. This
   *increases* the flow through the front stages (unstalling them) while reducing what the rear stages
   must swallow. Wasteful, but effective and simple. Used mainly during starting and acceleration.
3. **Multiple spools.** Let the front (LP) and rear (HP) groups run at *different* speeds. At low
   power the HP spool stays relatively fast while the LP slows down, which naturally rematches them.
   This is the most elegant fix and the reason essentially all modern engines are 2- or 3-spool
   ([L08a](L08a-turbojets.md) §6).

Real engines use **all three together**.

### 6. The operating line and where it comes from

**Crucially, the compressor does not choose its own operating point.** It's set by what's downstream.

For a gas generator with a **choked turbine nozzle** (the usual case at power), the turbine acts as a
fixed flow restriction. Flow compatibility between compressor and turbine gives:

$$
\frac{\dot m_3\sqrt{T_{03}}}{p_{03}} = \text{const (choked turbine nozzle)}
$$

Combined with the work balance from [L06](L06-thermodynamics-of-jet-engines.md), this pins the
operating line. Consequences:

- **Raising $T_{04}$** (more fuel) at fixed speed pushes the operating point **up and left** — toward
  surge. This is why acceleration is the critical case.
- **Opening the exhaust nozzle $A_8$** pulls the operating line **down and right** — away from surge.
  This is exactly why lighting an afterburner requires opening $A_8$
  ([L12](L12-afterburners-ramjet-combustors.md)) — otherwise the operating line would jump toward
  surge.
- **Turbine nozzle area** is thus a primary matching parameter and is sometimes trimmed in
  development to reposition the operating line.

**Acceleration schedule.** The control system limits fuel flow rate during acceleration precisely so the
operating line excursion doesn't cross the surge line. Too-fast fuel addition = surge. This is why
turbine engines have a noticeable spool-up lag — it's deliberate.

### 7. Stall recovery and protection

**Detection:** rapid loss of compressor discharge pressure, EGT spike, N1/N2 divergence, audible bangs.

**Recovery:** reduce fuel (throttle to idle) → open bleed valves → reset VSVs → relight if flamed out.
Modern FADEC systems do this automatically within milliseconds.

**Design protection:** casing treatments (circumferential grooves or axial slots over the rotor tips)
can extend the stall margin by 5–15% by disrupting the tip leakage vortex, at a small efficiency cost.
An accepted trade in high-distortion applications.

---

## Worked logic — surge margin during acceleration

**Given:** at 90% corrected speed, steady operating point $\dot m_{corr}=45$ kg/s, $\pi_c = 12$. The
surge line at 45 kg/s is $\pi_c = 14.4$.

**Step 1 — steady surge margin:**

$$
\mathrm{SM}=\frac{14.4-12}{12}\times100\% = 20\%
$$

Comfortably within the 15–25% target.

**Step 2 — apply the distortion penalty.** A supersonic inlet at angle of attack costs ~8% of margin:

$$
\mathrm{SM}_{\text{eff}} = 20\% - 8\% = 12\%
$$

**Step 3 — add a transient.** During a snap acceleration, fuel is added faster than the spool responds.
$T_{04}$ rises before $N$ does, and the operating point moves up the constant-speed line. Suppose the
transient operating $\pi_c$ reaches 13.2:

$$
\mathrm{SM}_{\text{transient}}=\frac{14.4-13.2}{13.2}\times100\%=9.1\%
$$

Now subtract distortion:

$$
9.1\% - 8\% = 1.1\%
$$

**Essentially zero margin — this engine would surge.** The combination of distortion and aggressive
acceleration exhausts the budget.

**Step 4 — the fixes, and what each buys:**

| Action | Margin recovered |
|---|---|
| Slow the acceleration schedule (limit fuel rate) | Keeps $\pi_c$ transient below ~12.5 ⇒ +5% |
| Open a bleed valve during the transient | +5–10% |
| Reschedule VSVs closed | +3–8% |
| Casing treatment (design change) | +5–15% |

**The engineering lesson:** surge margin is a **budget** consumed by distortion, transients,
deterioration, and tolerances *simultaneously*. Designing to the steady-state number alone guarantees
surges in service. This is why the acceleration schedule exists and why turbofans don't respond
instantly to throttle.

---

## Worked logic — a real accel stall margin check (choked-turbine method)

*Cross-referenced from a parallel offering — the same idea as above, but computed directly from the
choked-turbine flow parameter rather than an assumed transient $\pi_c$, and checked against an
empirical stall-line curve fit.* This is the calculation [L17 §0](L17-compressors-4.md) generalizes
into a full stability audit — read this one first.

**Given:** idle $T_4 = 1{,}360°\mathrm R$, $FP_4=20.7$, $P_{25}=17$ psia, corrected flow
$W_{25c}=25$ pps. On acceleration, $T_4$ jumps by $+700°\mathrm R$ (fuel added faster than the spool
responds — exactly [L17 §0](L17-compressors-4.md)'s transient-operating-line mechanism). The stall
line at this corrected flow is given by a quadratic curve fit:
$\pi_{\text{stall}} = -0.0008\,W_{25c}^2+0.2074\,W_{25c}-0.9335$.

**Step 1 — accelerated operating pressure ratio**, from the choked-turbine flow parameter (identical
method to [L17 §0](L17-compressors-4.md)'s worked example):

$$
T_{4,\text{accel}} = 1{,}360+700 = 2{,}060°\mathrm R
$$

$$
P_4 = \frac{\dot m\sqrt{T_4}}{FP_4} \;\Rightarrow\;
P_3 = \frac{P_4}{1-\text{burner loss}}, \qquad
\mathrm{CPR}_{\text{accel}} = \frac{P_3}{P_{25}} = 3.69
$$

**Step 2 — evaluate the stall-line curve fit at the same corrected flow:**

$$
\pi_{\text{stall}}(25) = -0.0008(25)^2+0.2074(25)-0.9335 = 3.77
$$

**Step 3 — compare:**

$$
3.69 < 3.77 \;\Rightarrow\; \textbf{no stall — margin remaining} \approx \frac{3.77-3.69}{3.69}\times100\% \approx 2\%
$$

**Why this matters as a method, not just a result:** this is the same $FP_4$-balance trick used
throughout [L25](L25-testing-performance-characteristics.md) for *measuring* airflow, now used
*predictively* to check operability before the engine ever runs. **The choked turbine nozzle relation
is the single most load-bearing equation in this course's back half** — it links the compressor
operating line ([L17 §0](L17-compressors-4.md)), engine controls
([L22 §0](L22-centrifugal-compressors.md)), and test data reduction ([L25](L25-testing-performance-characteristics.md))
all to the same physical constraint.

---

## Common pitfalls

- **Confusing rotating stall with surge.** Local/circumferential/steady-average vs.
  global/axial/oscillating with reversal.
- **Thinking stall cells rotate at rotor speed.** They rotate at 20–70% of it.
- **Using uncorrected parameters on a map.** Maps are *always* in corrected quantities.
- **Thinking the compressor sets its own operating line.** Downstream areas do.
- **Forgetting that opening $A_8$ moves the operating line away from surge.**
- **Assuming steady surge margin is sufficient.** Budget for distortion + transients + deterioration.
- **Believing variable stators are only about efficiency.** They're primarily about *matching* and
  startability.
- **Missing that front and rear stages mismatch in opposite directions off-design.**
- **Thinking bleed valves are pure waste.** They're the difference between starting and not starting.

---

## Exam checklist

- [ ] **Define corrected mass flow and corrected speed and explain physically why they collapse the map**
- [ ] Sketch a compressor map with speed lines, surge line, choke, efficiency islands, operating line
- [ ] Explain why speed lines go vertical at high speed
- [ ] Define surge margin and list what consumes it
- [ ] **Distinguish rotating stall from surge on mechanism, direction, frequency, and consequence**
- [ ] Explain the stall-cell propagation mechanism
- [ ] **Explain the stage matching problem and why front and rear mismatch oppositely off-design**
- [ ] Describe VSVs, bleed valves, and multi-spool as fixes, and what each does
- [ ] Explain how a choked turbine nozzle sets the operating line
- [ ] Explain why opening $A_8$ improves surge margin
- [ ] Explain why an acceleration schedule is needed
- [ ] Compute surge margin including distortion and transient effects

---

## Links

- Previous: [L15 — Compressors 2](L15-compressors-2.md)
- Next: [L17 — Compressors 4](L17-compressors-4.md) — multistage and radial equilibrium
- Distortion source: [L10 — Inlets](L10-inlets.md)
- Nozzle area coupling: [L12 — Afterburners](L12-afterburners-ramjet-combustors.md), [L13 — Nozzles](L13-nozzles.md)
- Turbine matching counterpart: [L21 — Turbines 3](L21-turbines-3.md)
- Concept: [corrected-parameters](../../concepts/corrected-parameters.md)
- Course hub: [EAS4300](../EAS4300.md)
