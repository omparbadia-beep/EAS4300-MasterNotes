# L21 — Axial Turbines 3: Maps and Component Matching

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 21 · **Date:** Mon 2 Nov 2026
**Book §:** 8.6 *Turbine Performance* (p. 400) — ✅ verified · **HW8 assigned**
*(§8.7 Turbine and Compressor Matching, p. 402, adjoins it and is what this page's matching material covers — the syllabus assigns 8.7 to L22 by apparent typo.)*
**Tags:** #turbine-map #choked-nozzle #component-matching #flow-function #operating-line #gas-generator #off-design #spool-dynamics

---

## Why this lecture matters

This lecture closes the loop. [L16](L16-compressors-3.md) established that the compressor's operating
line is set by *something downstream* — this is that something. **Component matching** is how the
individual maps of compressor, combustor, turbine, and nozzle combine into a single engine operating
point, and it's what a control system actually manipulates.

---

## Core concepts

### 1. The turbine map

Same corrected parameters as [L16](L16-compressors-3.md), but referenced to turbine inlet conditions:

$$
\dot m_{\text{corr}} = \frac{\dot m\sqrt{T_{04}}}{p_{04}}, \qquad N_{\text{corr}}=\frac{N}{\sqrt{T_{04}}}
$$

*(Some texts normalize by reference conditions as with compressors; either is fine as long as you're
consistent.)*

**Axes:** corrected flow vs. **expansion ratio** $p_{04}/p_{05}$, with speed lines and efficiency
contours.

**The turbine map looks completely different from a compressor map, and the reason is §2:**

- Speed lines **collapse onto one another** and go **vertical** at modest expansion ratio
- There is **no surge line** — a turbine cannot surge
- The efficiency contours are broad; turbines are efficient over a wide range

### 2. The choked turbine nozzle — the single most useful fact

**The NGV chokes at a low expansion ratio and stays choked over almost the entire operating range.**

From [L19](L19-turbines-1.md), the NGV accelerates the flow to $M \approx 0.9$–1.0 by design. Choking
occurs at:

$$
\frac{p_{04}}{p_{\text{throat}}} \ge \left(\frac{\gamma+1}{2}\right)^{\frac{\gamma}{\gamma-1}} \approx 1.85 \quad (\gamma=1.33)
$$

Typical HP turbine expansion ratios are 2–4, well above that. **So the NGV is choked at essentially all
power settings above idle.**

**Consequences — this is the heart of the lecture:**

$$
\frac{\dot m\sqrt{T_{04}}}{p_{04}} = \text{constant}
$$

- **The turbine behaves as a fixed-area flow restriction.** Its corrected flow is set purely by the NGV
  throat area $A_{\text{NGV}}$, and is independent of speed and of downstream conditions.
- **This single constraint fixes the compressor's operating line.**
- It's why turbine map speed lines collapse — corrected flow doesn't vary.
- **$A_{\text{NGV}}$ becomes a primary engine design/trim parameter.** Opening it moves the compressor
  operating line down and away from surge; closing it moves it up.

**Why a turbine cannot surge:** the flow is accelerating through a favorable pressure gradient
([L19](L19-turbines-1.md) §4). There's no diffusion, so there's no separation-driven instability. This
is the deep reason the two maps look so different.

### 3. Gas generator matching — the constraint set

For a single-spool gas generator, four conditions must hold simultaneously:

**(a) Work compatibility** — the turbine drives the compressor:

$$
c_{p,c}\left(T_{03}-T_{02}\right) = \eta_m(1+f)\,c_{p,h}\left(T_{04}-T_{05}\right)
$$

**(b) Flow compatibility** — same mass flow (plus fuel, minus bleed) through both:

$$
\dot m_4 = \dot m_2(1+f-b)
$$

Written in corrected form, this is the relation that ties the two maps together:

$$
\frac{\dot m_4\sqrt{T_{04}}}{p_{04}} = \frac{\dot m_2 \sqrt{T_{02}}}{p_{02}}
\cdot \frac{p_{02}}{p_{04}}\cdot\sqrt{\frac{T_{04}}{T_{02}}}\cdot(1+f-b)
$$

Since $p_{04}=\pi_b\pi_c\,p_{02}$:

$$
\frac{\dot m_4\sqrt{T_{04}}}{p_{04}} = \frac{\dot m_2\sqrt{T_{02}}}{p_{02}}\cdot\frac{(1+f-b)}{\pi_c\,\pi_b}\sqrt{\frac{T_{04}}{T_{02}}}
$$

**(c) Speed compatibility** — same shaft:

$$
N_c = N_t
$$

**(d) Pressure compatibility** — the expansion must match what's downstream (nozzle or next turbine).

**With the turbine choked, (b) becomes an algebraic constraint linking $\pi_c$, $\dot m_{corr,2}$, and
$T_{04}/T_{02}$** — and that *is* the compressor operating line.

### 4. Deriving the operating line

Set the turbine corrected flow to its choked constant $K$:

$$
\frac{\dot m_2 \sqrt{T_{02}}}{p_{02}}\cdot\frac{(1+f-b)}{\pi_c\pi_b}\sqrt{\frac{T_{04}}{T_{02}}} = K
$$

Rearranging for the compressor corrected flow:

$$
\frac{\dot m_2\sqrt{T_{02}}}{p_{02}} = \frac{K\,\pi_c\,\pi_b}{(1+f-b)}\sqrt{\frac{T_{02}}{T_{04}}}
$$

**Read this carefully — it's the answer to most matching questions:**

- **Corrected flow $\propto \pi_c$** — so the operating line rises to the right on the compressor map
- **Corrected flow $\propto \sqrt{T_{02}/T_{04}}$** — so at fixed $\pi_c$, **raising $T_{04}$ reduces the
  corrected flow the compressor can pass**, which moves the operating point **left** on the map —
  **toward surge**

**This is exactly why acceleration is the critical case for surge** ([L16](L16-compressors-3.md) §7):
snapping the throttle raises $T_{04}$ *before* the spool speeds up, so the operating point jumps left
toward the surge line.

**And why opening $A_8$ helps:** a larger exhaust nozzle lowers the back pressure on the turbine,
increasing $\pi_t$, which for fixed work lowers $\pi_c$ requirement and shifts the line down and right.

### 5. The turbine temperature ratio is nearly constant

A neat and useful result. With a choked NGV *and* a choked exhaust nozzle, the turbine expansion ratio
$\pi_t$ is essentially fixed by geometry:

$$
\pi_t \approx \text{const} \quad\Longrightarrow\quad \tau_t = \frac{T_{05}}{T_{04}} \approx \text{const}
$$

Combined with the work balance:

$$
\frac{T_{03}-T_{02}}{T_{02}} \propto \frac{T_{04}}{T_{02}}\left(1-\tau_t\right)
$$

$$
\Rightarrow \quad \tau_c - 1 \propto \frac{T_{04}}{T_{02}}
$$

**Interpretation:** the compressor temperature ratio is proportional to $T_{04}/T_{02}$. So the engine's
whole operating state is governed by essentially **one variable** — the cycle temperature ratio. This is
why $T_{04}/T_{02}$ (or its proxy, $N/\sqrt\theta$) is *the* engine operating parameter, and why
throttle position maps so directly onto it.

### 6. Two-spool matching

With two spools, there are two of everything and one extra constraint set:

- **HP spool:** HPC ↔ HPT work balance, both on the HP shaft, $N_H$
- **LP spool:** fan/LPC ↔ LPT work balance, both on the LP shaft, $N_L$
- **The spools are aerodynamically coupled but mechanically independent** — they find their own speed
  ratio $N_H/N_L$

**The self-matching benefit** ([L08a](L08a-turbojets.md) §6): at reduced power, the LP spool slows more
than the HP spool. That reduces the fan/LPC pressure ratio while the HP core keeps running relatively
fast, which naturally rematches the stage-loading problem of [L16](L16-compressors-3.md) §5. **The
speed ratio is an output, not an input** — it varies with power setting, and that variation is exactly
what makes multi-spool engines work off-design.

Typical: $N_H/N_L$ might be 2.5 at takeoff and 3.5 at idle.

**Both turbines are usually choked**, which decouples the analysis somewhat: the HPT's choked NGV
fixes the HPC operating line, and the LPT's choked NGV fixes the HPT's exit condition.

### 7. Off-design engine behavior

**Throttling (reducing fuel flow), in causal order:**

1. $T_{04}$ falls
2. Turbine work falls
3. Turbine work < compressor work momentarily ⇒ **spool decelerates**
4. Lower $N$ ⇒ lower $\dot m$, lower $\pi_c$
5. New equilibrium at lower everything

**Thrust falls faster than fuel flow**, so **TSFC worsens at part power**
([L09](L09-engine-aircraft-performance.md) §6).

**Altitude effects.** Falling $p_{02}$ reduces actual mass flow and thrust proportionally, but corrected
parameters and hence the *aerodynamic* operating point are preserved — which is the entire benefit of
corrected parameters ([corrected-parameters](../../concepts/corrected-parameters.md)).

**Hot day.** Higher $T_{02}$ ⇒ higher $\theta$ ⇒ **lower corrected speed** at the same physical speed
⇒ less corrected flow and lower $\pi_c$ ⇒ less thrust. To restore thrust, the control would have to
raise $N$ or $T_{04}$, both of which hit limits. **Flat rating** is the standard answer: the engine is
derated so it holds constant thrust up to a reference ambient temperature, above which thrust falls off.
This protects TIT and blade life ([L20](L20-turbines-2.md) §7) at the cost of takeoff performance on
very hot days.

### 8. Control variables

What a FADEC can actually manipulate, and what each does:

| Variable | Primary effect |
|---|---|
| **Fuel flow $\dot m_f$** | Sets $T_{04}$, hence power. The main control. |
| **Variable stator vanes** | Compressor matching, surge margin ([L16](L16-compressors-3.md)) |
| **Bleed valves** | Surge margin at low speed and during transients |
| **Nozzle area $A_8$** | Repositions the operating line; mandatory with afterburner ([L12](L12-afterburners-ramjet-combustors.md)) |
| **Variable turbine geometry** | Rare in aero engines; common in industrial and automotive turbochargers |

**Limits the control must respect:** maximum $T_{04}$ (blade life), maximum $N$ (disk stress), maximum
$p_{03}$ (casing), minimum surge margin, and flameout/relight boundaries.

---

## Worked logic — operating line shift during acceleration

**Given:** at steady cruise, $T_{02}=280$ K, $T_{04}=1400$ K, $\pi_c=15$, compressor corrected flow
40 kg/s. Throttle is snapped and $T_{04}$ jumps to 1,650 K before the spool responds (speed momentarily
unchanged).

**Step 1 — the flow compatibility relation.** From §4, at fixed corrected speed and turbine geometry:

$$
\dot m_{\text{corr},2} \propto \pi_c \sqrt{\frac{T_{02}}{T_{04}}}
$$

**Step 2 — the constraint.** The spool speed hasn't changed, so the compressor must stay on its
**same speed line**. On a high-speed line the corrected flow is nearly fixed (choked front stages,
[L16](L16-compressors-3.md) §2), so:

$$
\dot m_{\text{corr},2} \approx \text{const} \quad\Longrightarrow\quad \pi_c \sqrt{\frac{T_{02}}{T_{04}}} \approx \text{const}
$$

**Step 3 — solve for the new pressure ratio:**

$$
\pi_{c,\text{new}} = \pi_{c,\text{old}}\sqrt{\frac{T_{04,\text{new}}}{T_{04,\text{old}}}}
= 15\sqrt{\frac{1650}{1400}} = 15\sqrt{1.1786}=15(1.0856)=16.3
$$

**Step 4 — the surge margin consequence.** The operating point has jumped from $\pi_c = 15$ to
$\pi_c = 16.3$ at essentially the same corrected flow — **straight up the map, toward the surge line.**

If the surge line at 40 kg/s is $\pi_c = 18$:

$$
\mathrm{SM}_{\text{steady}}=\frac{18-15}{15}=20\%
$$

$$
\mathrm{SM}_{\text{transient}}=\frac{18-16.3}{16.3}=10.4\%
$$

**Half the surge margin consumed by one throttle snap** — and that's before accounting for inlet
distortion, which could take another 8 points and leave essentially nothing
([L16](L16-compressors-3.md) worked example).

**Step 5 — what the control does about it.** The **acceleration schedule** limits $d\dot m_f/dt$ so
$T_{04}$ rises no faster than the spool can follow. In practice the fuel controller schedules against
$\dot m_f/p_{03}$ or $N/\sqrt\theta$ with an explicit surge-margin allowance. Bleed valves may open
during the transient for extra margin.

**This is why a turbofan takes 5–8 seconds to spool from idle to takeoff thrust.** It isn't mechanical
inertia alone — it's a deliberate limit to stay off the surge line. This is exactly why go-around
procedures require spooling up before committing, and it's a good practical example to cite in an
exam answer.

---

## Common pitfalls

- **Forgetting the turbine NGV is choked.** It's the key simplification for every matching problem.
- **Thinking a turbine can surge.** It cannot — favorable pressure gradient, no diffusion.
- **Assuming the compressor sets its own operating line.** The turbine NGV and exhaust nozzle areas do.
- **Getting the $T_{04}$ direction wrong.** Higher $T_{04}$ at fixed speed moves the operating point
  **toward** surge.
- **Treating spool speed ratio as fixed** in a two-spool engine. It varies with power setting.
- **Using compressor reference conditions for turbine corrected parameters.** Reference to $T_{04}$,
  $p_{04}$.
- **Forgetting bleed in flow compatibility.** $(1+f-b)$, not $(1+f)$.
- **Thinking spool-up lag is purely mechanical inertia.** It's largely the acceleration schedule.

---

## Exam checklist

- [ ] Sketch a turbine map and explain why speed lines collapse and go vertical
- [ ] **Explain why the NGV chokes and what $\dot m\sqrt{T_{04}}/p_{04}=$ const implies**
- [ ] Explain why a turbine cannot surge
- [ ] State the four gas-generator matching conditions
- [ ] **Derive the operating line relation and read off the $\pi_c$ and $T_{04}$ dependencies**
- [ ] Explain why raising $T_{04}$ at fixed speed moves toward surge
- [ ] Explain why opening $A_8$ moves away from surge
- [ ] Show that $\tau_c - 1 \propto T_{04}/T_{02}$ with choked turbine and nozzle
- [ ] Explain two-spool self-matching and why $N_H/N_L$ varies
- [ ] Explain flat rating and hot-day thrust lapse
- [ ] **Compute the operating-line shift and surge margin loss during a throttle snap**
- [ ] List FADEC control variables and the limits they respect

---

## Links

- Previous: [L20 — Turbines 2](L20-turbines-2.md)
- Next: [L22 — Centrifugal Compressors](L22-centrifugal-compressors.md)
- **Midterm 2 review 6 Nov, exam 9 Nov** → [exam-midterm-2](exam-midterm-2.md)
- Compressor map side: [L16 — Compressors 3](L16-compressors-3.md)
- Nozzle area coupling: [L12](L12-afterburners-ramjet-combustors.md), [L13](L13-nozzles.md)
- Cycle context: [L06](L06-thermodynamics-of-jet-engines.md), [L08a](L08a-turbojets.md)
- Concept: [corrected-parameters](../../concepts/corrected-parameters.md)
- Course hub: [EAS4300](../EAS4300.md)
