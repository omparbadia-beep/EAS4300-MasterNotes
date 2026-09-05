# L10 — Inlets

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 10 · **Date:** Mon 28 Sep 2026
**Book §:** 6.1 *Introduction* · 6.2 *Subsonic Inlets* (p. 218) · 6.3 *Supersonic Inlets* (p. 226) — ✅ verified · **HW4 assigned**
**Tags:** #inlet #diffuser #pressure-recovery #spillage-drag #supersonic-inlet #shock-system #unstart #capture-area #buzz

---

## Why this lecture matters

The inlet does no work and burns no fuel, yet it can destroy more performance than any other component.
At Mach 3, a badly designed inlet throws away two-thirds of your stagnation pressure before the
compressor ever sees the air. This is the first component lecture, and it is where the gas dynamics of
[L05](L05-gas-dynamics.md) meets real hardware.

---

## Core concepts

### 1. What an inlet must do

Deliver air to the compressor face (station 2) at:

- **High stagnation pressure recovery** — every 1% of $p_{02}$ lost costs roughly 1–1.5% of thrust
- **Low Mach number** — $M_2 \approx 0.4$–0.6, because compressors cannot ingest supersonic flow
- **Uniform flow** — distortion (circumferential or radial non-uniformity) causes compressor stall
- **Low external drag** — spillage and cowl drag are charged against the engine
- **Across the whole flight envelope**, not just the design point

**The recurring theme: an inlet is a *variable* problem with (usually) *fixed* geometry.** Everything
difficult about inlet design follows from that mismatch.

### 2. Pressure recovery — the figure of merit

$$
\pi_d = \frac{p_{02}}{p_{00}}
$$

Recall from [L02](L02-basic-concepts.md): the inlet is adiabatic and does no work, so **$T_{02}=T_{00}$
always**. All the physics lives in $p_{02}$. Losses come from friction, shocks, and separation.

**Isentropic (ideal) recovery is 1.0** by definition. Realistic values:

| Condition | $\pi_d$ |
|---|---|
| Subsonic, well designed | 0.97–0.99 |
| $M_0 = 1.5$ | ~0.95 |
| $M_0 = 2.0$ | ~0.90 |
| $M_0 = 3.0$ | ~0.75–0.85 (good multi-shock design) |
| $M_0 = 3.0$, single normal shock | **0.33** |

**MIL-E-5008B standard** for supersonic inlet recovery, widely used in cycle analysis:

$$
\pi_d = \pi_{d,\max}\left[1 - 0.075\left(M_0 - 1\right)^{1.35}\right], \qquad M_0 > 1
$$

$$
\pi_d = \pi_{d,\max}, \qquad M_0 \le 1
$$

### 3. Subsonic inlets

At subsonic flight the inlet is a **diffuser**: it decelerates the flow (which raises static pressure).
From [L05](L05-gas-dynamics.md), subsonic deceleration requires a **diverging** duct.

**The core difficulty is the adverse pressure gradient.** Rising static pressure pushes against the
boundary layer, and if the diffusion is too aggressive the boundary layer **separates**, causing
large $p_0$ loss and severe distortion. Practical limits:

- **Divergence half-angle** ≲ 5–7°
- **Area ratio** limited by length available

**Off-design behavior is the real story.** The inlet must handle:

| Condition | Problem |
|---|---|
| **Takeoff/static** | Engine demands more air than the inlet captures ⇒ flow accelerates *into* the inlet, sharp turning around the lip. A **thick, rounded lip** is essential or the flow separates internally. |
| **Cruise** | Demand matches capture. Design point. Thin lip would be better for drag. |
| **High-speed descent, low power** | Engine demands *less* than the streamtube brings ⇒ **spillage** around the cowl. |
| **Crosswind on the ground** | Highly asymmetric flow into the lip; a classic distortion case. |

The **rounded vs. sharp lip** conflict is the canonical fixed-geometry compromise: rounded is
essential at static/low speed, but at supersonic speed a blunt lip generates a strong detached bow
shock. This is exactly why supersonic aircraft inlets have sharp lips and *terrible* static
performance, often needing auxiliary blow-in doors on the ground.

### 4. Capture area and spillage drag

The **stream tube** that ends up entering the inlet has area $A_0$ far upstream, and the inlet's
physical **capture area** is $A_1$.

$$
\dot{m} = \rho_0 u_0 A_0
$$

**Mass flow ratio:**

$$
\mathrm{MFR} = \frac{A_0}{A_1}
$$

| Regime | Behavior |
|---|---|
| $A_0 > A_1$ | Engine demands more than the cowl frontal area — stream tube **contracts** (low speed, high power) |
| $A_0 = A_1$ | Matched — the design condition |
| $A_0 < A_1$ | Engine demands less — stream tube **expands** and air **spills** around the cowl |

**Spillage drag** arises because spilled air was partially compressed by the inlet's presence and then
diverted, so its momentum is not fully recovered. For subsonic inlets it's modest. For **supersonic**
inlets it's large, because spilled air has passed through the bow shock and paid the full $p_0$
penalty for nothing.

This is a genuine installation loss ([L09](L09-engine-aircraft-performance.md) §5) and must be
charged against installed thrust.

### 5. Supersonic inlets — the shock problem

The flow must be decelerated from supersonic to $M_2 \approx 0.5$. From [L05](L05-gas-dynamics.md) that
transition **cannot be smooth** — a shock is required somewhere. The design question is: *what shock
system minimizes $p_0$ loss?*

**Recall the key numbers ([L05](L05-gas-dynamics.md) §6):** a single normal shock at $M=3$ gives
$p_{02}/p_{01} = 0.33$. Unacceptable.

**The fix — multiple weak oblique shocks.** Because $M_{n1}=M_1\sin\beta$, an oblique shock does the
turning with a much smaller normal Mach component, and $p_0$ loss grows sharply with $M_n$. Splitting
the deceleration into several weak shocks followed by a weak terminal normal shock is dramatically
better.

**Illustration at $M_0=3$:**

| Design | $\pi_d$ |
|---|---|
| Single normal shock | 0.33 |
| 1 oblique + normal | ~0.66 |
| 2 oblique + normal | ~0.79 |
| 3 oblique + normal | ~0.85 |
| Isentropic (unachievable) | 1.00 |

**Diminishing returns are visible** — each added shock buys less, while adding weight, length, and
off-design sensitivity. Three or four shocks is the practical sweet spot.

**Oswatitsch's result:** for a given number of shocks, total $p_0$ loss is minimized when each oblique
shock has the **same normal Mach number**. Useful design rule and a plausible exam question.

### 6. Inlet configurations

**External compression** — all shocks ahead of the cowl lip (e.g. a wedge or cone ramp).
*Pro:* cannot unstart in the catastrophic sense; simple.
*Con:* the flow must be turned back to axial, generating high **cowl drag** at high Mach.

**Internal compression** — shocks inside the duct.
*Pro:* low external/cowl drag.
*Con:* **must be "started,"** and can **unstart** violently.

**Mixed compression** — some of each. Used on the SR-71 and the Concorde. Best overall recovery at
high Mach, most complex.

**Geometry families:**
- **Pitot (normal shock) inlet** — a plain hole. Fine to $M \approx 1.6$; simple and light.
- **2-D ramp** — wedge ramps, often variable. F-15, F-14, Concorde.
- **Axisymmetric spike** — a translating cone. SR-71, MiG-21, many missiles.
- **DSI (diverging/bump inlet)** — a fixed 3-D bump that diverts boundary layer and generates
  compression without moving parts. F-35, JF-17. A modern weight-and-signature win, at some
  peak-recovery cost.

### 7. Starting and unstart

**The starting problem (internal compression):** the Kantrowitz limit. When you first accelerate to
supersonic speed, a normal shock sits ahead of the inlet. To swallow it, the internal contraction
ratio must be small enough for the *subsonic* flow behind the shock to pass through the throat. But
the contraction ratio you *want* for good supersonic compression is much larger than that.

**Consequence:** a fixed-geometry internal-compression inlet with good design-point performance
**cannot start**. Solutions:
- **Variable geometry** — translate the spike or open bypass doors to swallow the shock, then close
- **Overspeed** — accelerate past design Mach to swallow the shock, then decelerate
- **Bleed** — remove boundary layer and mass flow to shift the limit

**Unstart** is the reverse and is violent: the terminal shock is expelled forward, mass flow collapses,
thrust drops abruptly, and large asymmetric side loads appear. Causes: too much back pressure (excess
fuel, thermal choking per [L07](L07-ramjets.md)), angle of attack, or gusts.

The **SR-71** unstart was notorious — an abrupt yaw violent enough to bang crew helmets against the
canopy. Its automatic restart system existed precisely for this.

**Inlet buzz** — a related but distinct instability: a self-sustained oscillation of the shock system,
usually at low mass flow ratio, driven by shock/boundary-layer interaction. It produces high-amplitude
pressure fluctuations that can damage the engine and is a hard limit on the low-flow side of the
operating range.

### 8. Boundary layer management

Boundary layers cause two problems in supersonic inlets:
1. **Shock/boundary-layer interaction** — the adverse pressure jump separates the boundary layer,
   thickening it and creating distortion
2. **Fuselage boundary layer ingestion** — for inlets mounted on the airframe

**Fixes:**
- **Boundary layer diverter** — a physical gap between fuselage and inlet (visible on the F-4, F-15)
- **Bleed slots/perforations** — suck low-momentum air off the ramp; costs mass flow and adds drag
- **DSI bump** — passively pushes the boundary layer aside (F-35)

**Distortion** is quantified by indices such as $DC(60)$ — the worst 60° sector's pressure deficit
relative to the face average. High distortion narrows the compressor surge margin
([L16](L16-compressors-3.md)); the inlet and compressor cannot be designed independently.

---

## Worked logic — two-shock inlet at M 2.5

**Given:** $M_0 = 2.5$, a 10° compression ramp, then a normal shock. $\gamma=1.4$.

**Step 1 — oblique shock.** From the θ-β-M relation with $\theta=10°$, $M_0=2.5$, the weak solution is
$\beta \approx 31.9°$.

$$
M_{n1} = M_0\sin\beta = 2.5\sin(31.9°)=2.5(0.5284)=1.321
$$

**Step 2 — normal-shock relations on $M_{n1}$:**

$$
M_{n2}^2 = \frac{1+0.2(1.321)^2}{1.4(1.321)^2-0.2} = \frac{1.3491}{2.2432}=0.6014
\;\Rightarrow\; M_{n2}=0.7755
$$

$$
M_1 = \frac{M_{n2}}{\sin(\beta-\theta)} = \frac{0.7755}{\sin(21.9°)}=\frac{0.7755}{0.3730}=2.079
$$

$$
\left(\frac{p_0'}{p_{00}}\right)_{\text{oblique}} \approx 0.9746 \quad\text{(from normal-shock tables at }M_n=1.321)
$$

**Step 3 — terminal normal shock at $M=2.079$:**

$$
\left(\frac{p_0''}{p_0'}\right)_{\text{normal}} \approx 0.6975
$$

**Step 4 — total recovery:**

$$
\pi_d = 0.9746 \times 0.6975 \approx 0.680
$$

**Compare with a single normal shock at $M_0 = 2.5$:** $\pi_d = 0.499$.

**The 10° ramp bought a 36% relative improvement in recovery** — from 0.499 to 0.680 — for the cost of
one wedge. Add a second ramp and you approach 0.75+. **This calculation is the entire justification
for supersonic inlet complexity**, and it is a very likely exam problem.

---

## Worked logic — subsonic diffuser static-pressure-recovery fraction

*Cross-referenced from a prior Anup Mannem-taught offering.* A metric distinct from $\pi_d$: what
fraction of the **dynamic pressure** at the inlet lip actually converts to a static pressure rise by
the compressor face, versus being lost to friction and separation?

**Given:** $M_0=0.9$ at 45,000 ft ($T_a=390°\mathrm R$, $P_a=2.14$ psia), $\dot m=210$ lbm/s,
lip area $A_1=30$ ft², diffuser efficiency $\eta_d=0.9$, compressor-face $M_2=0.4$.

**Step 1 — freestream stagnation conditions**, then solve continuity implicitly for the lip Mach
number $M_1$ (since $\dot m$, $A_1$, and $P_{t0}$ are known but $M_1$ isn't):

$$
P_{t0} = P_a\left(1+0.2M_0^2\right)^{3.5} = 3.62\ \mathrm{psia}, \qquad
T_{ta}=T_a\left(1+0.2M_0^2\right)=453.18°\mathrm R
$$

Solving $\dot m = \rho_1 A_1 V_1$ with $P_1$ and $T_1$ both expressed via $M_1$ and the known
stagnation values gives $M_1=0.56$, hence $P_1=2.93$ psia, $T_1=426.43°\mathrm R$.

**Step 2 — diffuser efficiency gives the stagnation temperature "reached" at the compressor face**,
then the compressor-face stagnation and static pressures at $M_2=0.4$:

$$
\eta_d = \frac{T_{t2,s}-T_a}{T_{t1}-T_a} \;\Rightarrow\; T_{t2,s}=446.86°\mathrm R
\;\Rightarrow\;
P_{t2}=P_a\left(\frac{T_{t2,s}}{T_a}\right)^{\gamma/(\gamma-1)}=3.45\ \mathrm{psia}
$$

$$
P_2 = P_{t2}\left(1+0.2M_2^2\right)^{-3.5} = 3.086\ \mathrm{psia}
$$

**Step 3 — the recovery-fraction metric:**

$$
\text{dynamic pressure at lip} = P_{t0}-P_1 = 3.62-2.93=0.69\ \mathrm{psi}
$$

$$
\text{fraction converted to static pressure} = \frac{P_2-P_1}{\text{dynamic pressure}}
= \frac{3.086-2.93}{0.69} \approx 0.226
$$

**Only ~23% of the available dynamic pressure became useful static pressure rise** — the rest is the
diffuser's internal losses (friction, any separation), distinct from $\pi_d$ (which compares
stagnation pressures end to end). **Two different "how good is this diffuser" numbers, both real**:
$\pi_d$ answers "how much total pressure did I keep," this recovery fraction answers "how efficiently
did I convert the *kinetic* energy I decelerated into *useful* static pressure rise." A subsonic inlet
can score reasonably on one and poorly on the other.

---

## Common pitfalls

- **Forgetting $T_{02}=T_{00}$ across the inlet.** Only $p_0$ changes. Students routinely "heat" the
  flow in an inlet.
- **Applying isentropic relations across the shock system.** Use shock relations, then resume
  isentropic from the reduced $p_0$.
- **Using $M_1$ instead of $M_{n1}=M_1\sin\beta$** in oblique shock relations. The single most common
  error on this topic.
- **Taking the strong oblique solution.** Nature picks weak unless back pressure forces otherwise.
- **Ignoring spillage drag.** It's a real installed-thrust penalty.
- **Assuming a fixed-geometry internal-compression inlet will start.** It generally won't (Kantrowitz).
- **Designing the inlet in isolation from the compressor.** Distortion couples them directly.
- **Assuming more shocks is always better.** Diminishing returns plus weight and off-design penalties.
- **Confusing unstart with buzz.** Unstart = shock expelled, flow collapse. Buzz = oscillating shock
  system at low mass flow.

---

## Exam checklist

- [ ] State the four requirements on an inlet and the figure of merit $\pi_d$
- [ ] Explain why $T_{02}=T_{00}$ but $p_{02}<p_{00}$
- [ ] Explain the subsonic lip-shape compromise (static vs. cruise vs. supersonic)
- [ ] Define capture area, mass flow ratio, and spillage drag
- [ ] Explain why a single normal shock is unacceptable above $M\approx1.6$, with numbers
- [ ] **Compute total $\pi_d$ for a multi-shock inlet** (oblique(s) + normal)
- [ ] State Oswatitsch's equal-normal-Mach design rule
- [ ] Compare external / internal / mixed compression on drag, recovery, and unstart risk
- [ ] Explain the Kantrowitz starting problem and three ways around it
- [ ] Describe unstart, its causes and consequences; distinguish it from buzz
- [ ] Explain distortion, how it's measured, and why it constrains the compressor

---

## Links

- Previous: [L09 — Engine/Aircraft Performance](L09-engine-aircraft-performance.md)
- Next: [L11 — Combustors](L11-combustors.md)
- Gas dynamics behind this: [L05 — Gas Dynamics](L05-gas-dynamics.md)
- Ramjet coupling: [L07 — Ramjets](L07-ramjets.md)
- Compressor surge margin: [L16 — Compressors 3](L16-compressors-3.md)
- Course hub: [EAS4300](../EAS4300.md)
