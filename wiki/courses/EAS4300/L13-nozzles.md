# L13 — Nozzles

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 13 · **Date:** Mon 12 Oct 2026
**Book §:** 6.7 *Exhaust Nozzles* (p. 264) — ✅ verified · **HW5 assigned** *(§6.6 Supersonic Combustion is skipped)*
**Tags:** #nozzle #convergent-divergent #expansion-ratio #overexpanded #underexpanded #thrust-coefficient #variable-geometry #thrust-vectoring #discharge-coefficient

**First lecture after Midterm 1** (exam 7 Oct, holiday 9 Oct).

---

## Why this lecture matters

The nozzle is where all the cycle's stored pressure and temperature finally becomes thrust. It's also
the component most directly governed by [L05](L05-gas-dynamics.md) — the operating regimes you learned
there are exactly what a nozzle does in service. And unlike the inlet, the nozzle's losses are small
but its *matching* to flight condition is decisive.

---

## Core concepts

### 1. What the nozzle does

Convert stagnation enthalpy at station 7 into directed kinetic energy at station 9. From the SFEE
([L02](L02-basic-concepts.md)) with no work and no heat:

$$
h_{07}=h_9 + \frac{u_9^2}{2}
\quad\Longrightarrow\quad
u_9 = \sqrt{2c_p\left(T_{07}-T_9\right)}
$$

With isentropic expansion to pressure $p_9$ — **the single most-used nozzle equation**:

$$
u_9 = \sqrt{2c_pT_{07}\left[1-\left(\frac{p_9}{p_{07}}\right)^{\frac{\gamma-1}{\gamma}}\right]}
$$

**Read the dependencies:** exit velocity rises with $T_{07}$ (hotter is better — hence the afterburner)
and with the pressure ratio $p_{07}/p_9$ (more expansion is better — up to a point, §4).

### 2. Convergent vs. convergent-divergent

**When is the nozzle choked?** From [L05](L05-gas-dynamics.md), a converging nozzle chokes when:

$$
\frac{p_{07}}{p_a} \ge \left(\frac{\gamma+1}{2}\right)^{\frac{\gamma}{\gamma-1}}
$$

$$
\gamma=1.4: \ 1.893 \qquad \gamma=1.33: \ 1.853
$$

**Convergent nozzle.** Simple, light, short. Exit Mach ≤ 1. Once choked, further pressure ratio is
"wasted" in the sense that the flow leaves at $M=1$ with $p_9 > p_a$ — but it isn't entirely lost,
because the **pressure thrust term** $(p_9-p_a)A_9$ recovers some of it.

**Used on:** essentially all subsonic civil turbofans. Their nozzle pressure ratios are ~2–3, so a C-D
nozzle would gain only 1–2% thrust — not worth the weight, length, and complexity.

**Convergent-divergent nozzle.** Needed when the pressure ratio is large enough that full expansion
buys real thrust. Exit Mach > 1.

**Used on:** supersonic military engines (with variable geometry), and **all rockets** (where NPR can be
100+).

**Rule of thumb:** C-D pays off above NPR ≈ 3–4, and becomes essential above ~6.

### 3. The area ratio and design point

For a C-D nozzle, the expansion (area) ratio sets the design exit Mach — the $A/A^*$ relation from
[L05](L05-gas-dynamics.md):

$$
\epsilon = \frac{A_9}{A_8}=\frac{1}{M_9}\left[\frac{2}{\gamma+1}\left(1+\frac{\gamma-1}{2}M_9^2\right)\right]^{\frac{\gamma+1}{2(\gamma-1)}}
$$

And the corresponding pressure ratio:

$$
\frac{p_{07}}{p_9}=\left(1+\frac{\gamma-1}{2}M_9^2\right)^{\frac{\gamma}{\gamma-1}}
$$

**A fixed geometry has exactly one perfectly-expanded condition.** Everywhere else it's over- or
underexpanded. Since flight altitude changes $p_a$ by orders of magnitude, **fixed nozzles are always
off-design somewhere** — which is §4.

Choked mass flow through the throat (from [L05](L05-gas-dynamics.md) §4):

$$
\dot m = \frac{p_{07}A_8}{\sqrt{T_{07}}}\sqrt{\frac{\gamma}{R}}\left(\frac{2}{\gamma+1}\right)^{\frac{\gamma+1}{2(\gamma-1)}}
$$

**$A_8$ sets the engine's mass flow.** This is why the variable nozzle in
[L12](L12-afterburners-ramjet-combustors.md) is such a powerful control: changing $A_8$ rematches the
whole engine.

### 4. Off-design operation — over- and underexpansion

| Condition | Meaning | Consequence |
|---|---|---|
| **Underexpanded** $p_9 > p_a$ | Not enough area | Expansion fans outside; plume spreads. Thrust lost — you didn't extract available pressure. Partially recovered by pressure thrust. |
| **Perfectly expanded** $p_9 = p_a$ | Design | Maximum thrust for that $p_{07}$ |
| **Overexpanded** $p_9 < p_a$ | Too much area | Oblique shocks outside; plume contracts. Negative pressure-thrust term. |
| **Severely overexpanded** | $p_a/p_9 \gtrsim 2.5$ | **Flow separates inside the nozzle** — shock moves in, plus side loads |

**Flow separation is the dangerous one.** In a severely overexpanded nozzle the internal boundary layer
cannot sustain the adverse gradient and separates asymmetrically, producing large unsteady **side
loads** that can destroy the nozzle or gimbal actuators. This is the practical limit on rocket nozzle
area ratio at sea level.

**Summerfield criterion** — the classical rule of thumb for separation onset:

$$
p_9 \gtrsim 0.4\,p_a \quad\text{(separation-free)}
$$

**Altitude effect for rockets:** a nozzle sized for vacuum would separate catastrophically at sea level;
a nozzle sized for sea level is badly underexpanded in vacuum. First stages compromise (slightly
overexpanded at liftoff, near-optimum at altitude), and upper stages use huge area ratios ($\epsilon$ =
80–280) because they never see sea level. → [L24](L24-rocket-engines-2.md)

### 5. Nozzle performance parameters

**Isentropic (velocity) efficiency:**

$$
\eta_n = \frac{u_9^2}{u_{9,\text{ideal}}^2}=\frac{h_{07}-h_9}{h_{07}-h_{9s}}
$$

Typically **0.97–0.99** — nozzles are the *best* component in the engine, because accelerating flow has
a **favorable pressure gradient** that keeps boundary layers thin and attached. Compare to a diffuser,
where the adverse gradient makes life hard.

**Discharge coefficient** — actual vs. ideal mass flow, accounting for boundary layer blockage and
non-uniformity at the throat:

$$
C_D = \frac{\dot m_{\text{actual}}}{\dot m_{\text{ideal}}} \approx 0.97\text{–}0.99
$$

**Thrust coefficient** — the standard rocket/nozzle figure of merit:

$$
C_F = \frac{F}{p_{07}A_8}
$$

$$
C_F = \sqrt{\frac{2\gamma^2}{\gamma-1}\left(\frac{2}{\gamma+1}\right)^{\frac{\gamma+1}{\gamma-1}}
\left[1-\left(\frac{p_9}{p_{07}}\right)^{\frac{\gamma-1}{\gamma}}\right]}
+ \frac{(p_9-p_a)A_9}{p_{07}A_8}
$$

**$C_F$ measures how well the nozzle converts chamber pressure into thrust.** It separates cleanly from
$c^*$ (which measures the combustor) — see [L23](L23-rocket-engines-1.md). Typical values 1.3–1.9.

**Divergence (angularity) loss** — a conical nozzle's exit flow isn't axial, so only the axial component
produces thrust:

$$
\lambda = \frac{1+\cos\alpha}{2}
$$

For a 15° half-angle cone, $\lambda = 0.983$ — a **1.7% thrust loss** just from geometry. This is why
**bell nozzles** exist: contoured to turn the flow back to axial, recovering most of that loss in a
shorter length.

### 6. Variable geometry

**Why needed** (recapping [L12](L12-afterburners-ramjet-combustors.md)):
- **$A_8$ (throat)** sets engine mass flow and back-pressures the turbine. Must open ~50% when the
  afterburner lights, or the compressor surges.
- **$A_9$ (exit)** sets expansion ratio, which should track flight altitude and Mach.

**Mechanisms:**
- **Convergent iris** — overlapping petals, $A_8$ only. Simple.
- **C-D variable** — independently actuated convergent and divergent petals. Heavy and complex, but
  gives both $A_8$ and $A_9$.
- **Ejector nozzle** — secondary airflow forms an aerodynamic boundary that effectively varies the
  expansion. Used on the SR-71 and Concorde.

**Cost:** a variable C-D nozzle can be **~30% of total engine weight** and is a major maintenance and
reliability item. This is a large part of why civil engines use fixed convergent nozzles.

### 7. Thrust vectoring

Deflecting the jet to produce control forces.

- **Mechanical (gimbaled/pitch-vectoring petals)** — F-22 (2-D, pitch only), Su-30/35 (axisymmetric,
  all-axis). Enables post-stall maneuvering.
- **Fluidic** — inject secondary flow to deflect the jet asymmetrically. No moving parts, lighter, but
  limited authority and still maturing.
- **Rocket TVC** — gimbaled engines are standard for launch vehicle control (see
  [L24](L24-rocket-engines-2.md)).

**Cosine loss:** vectoring by angle $\delta$ costs axial thrust by $\cos\delta$. At 20°, that's a 6%
loss — acceptable transiently, not for cruise.

### 8. Advanced concepts

**Aerospike / plug nozzle.** The outer boundary is the ambient air itself, so the effective expansion
ratio **self-adjusts with altitude** — altitude compensation without moving parts. Excellent in theory;
the persistent problems are base drag at low altitude and cooling the spike. Studied for the X-33/RS-2200
and never flown operationally.

**Dual-bell nozzle.** Two contour sections with an inflection. At sea level flow separates cleanly and
stably at the inflection (small effective $\epsilon$); at altitude it attaches to the full contour
(large $\epsilon$). Two-point altitude compensation with no moving parts.

**Noise suppression.** Jet noise scales as $u_e^8$ ([L08b](L08b-turbofans.md)). **Chevrons** —
sawtooth serrations at the nozzle lip — generate streamwise vortices that enhance mixing of the fast
core with the slower bypass and ambient air, reducing low-frequency noise by 2–4 dB for a ~0.2–0.5%
thrust penalty. Visible on the 787 and 747-8.

**Thrust reversers.** Not for thrust *production* but for stopping. Cascade (translating cowl) types
dominate on high-bypass engines since reversing the *bypass* stream alone provides most of the effect.
Typically recover 30–50% of forward thrust in reverse.

---

## Worked logic — fixed C-D nozzle across altitude

**Given:** a C-D nozzle with $\epsilon = A_9/A_8 = 4.0$, $\gamma = 1.33$, $p_{07} = 250$ kPa,
$T_{07}=1000$ K, $A_8 = 0.20$ m².

**Step 1 — design exit Mach.** Solve $A/A^*=4.0$ for the **supersonic** root with $\gamma=1.33$:

$$
M_9 \approx 2.83
$$

**Step 2 — design exit pressure:**

$$
\frac{p_{07}}{p_9}=\left(1+0.165(2.83)^2\right)^{4.03}=\left(2.321\right)^{4.03}
$$

$$
\approx 29.6 \quad\Longrightarrow\quad p_9 = \frac{250}{29.6}=8.45\ \mathrm{kPa}
$$

**So this nozzle is perfectly expanded at $p_a = 8.45$ kPa — about 17.5 km altitude.**

**Step 3 — behavior at sea level ($p_a = 101.3$ kPa):**

$$
\frac{p_a}{p_9}=\frac{101.3}{8.45}=12.0
$$

**Massively overexpanded.** Far beyond the Summerfield criterion ($p_9 \ge 0.4p_a$ would need
$p_9 \ge 40.5$ kPa). **The flow will separate inside the divergent section**, with a shock system and
unsteady side loads. In practice the nozzle behaves as if it had a much smaller effective $\epsilon$.

**Step 4 — behavior in vacuum ($p_a=0$):**

$$
p_9 - p_a = 8.45\ \mathrm{kPa} > 0 \quad\Longrightarrow\quad \text{underexpanded}
$$

Thrust is *higher* than at design (the pressure term is fully positive), but not as high as a
larger-$\epsilon$ nozzle would give.

**Step 5 — the design lesson.** One fixed geometry cannot serve 0–17.5 km. Options:
- **Variable geometry** (military aircraft)
- **Accept the compromise** — size for a mid-altitude point (booster stages)
- **Altitude-compensating designs** — aerospike, dual-bell
- **Separate nozzles per stage** — small $\epsilon$ on boosters, huge $\epsilon$ on upper stages
  (the standard, and cheapest, answer)

---

## Common pitfalls

- **Assuming any C-D nozzle produces supersonic exit flow.** Only if choked *and* the back pressure is
  low enough — regimes 1–4 of [L05](L05-gas-dynamics.md) §5 are subsonic at exit.
- **Picking the subsonic root of $A/A^*$** for a supersonic nozzle.
- **Dropping the pressure-thrust term** when the nozzle isn't perfectly expanded. Choked convergent
  nozzles *always* have one.
- **Using $\gamma = 1.4$.** Nozzle gas is hot: 1.30–1.33.
- **Thinking overexpansion is merely suboptimal.** Severe overexpansion causes separation and
  destructive side loads.
- **Confusing $\eta_n$ (velocity efficiency) with $C_D$ (mass flow) or $C_F$ (thrust).** Three different
  quantities.
- **Forgetting divergence loss** for conical nozzles.
- **Assuming a bigger area ratio is always better.** Only until separation or weight dominates.
- **Ignoring that $A_8$ sets engine mass flow.** It's the primary control variable, not just a hole.

---

## Exam checklist

- [ ] Derive $u_9$ from the energy equation and the isentropic pressure ratio
- [ ] State the choking pressure ratio for $\gamma=1.4$ and $1.33$
- [ ] Explain when C-D is justified over convergent, and why civil engines use convergent
- [ ] Use $\epsilon = A_9/A_8$ to find design $M_9$ and $p_9$; pick the correct root
- [ ] **Classify under/perfect/overexpanded and describe the external wave pattern for each**
- [ ] State the Summerfield separation criterion and explain side loads
- [ ] Define $\eta_n$, $C_D$, $C_F$, and divergence loss $\lambda$
- [ ] Explain why nozzle efficiency exceeds diffuser efficiency (pressure gradient argument)
- [ ] Explain why $A_8$ must vary with the afterburner and estimate the ratio
- [ ] Describe aerospike and dual-bell altitude compensation
- [ ] Explain chevrons and the $u_e^8$ noise scaling

---

## Links

- Previous: [L12 — Afterburners & Ramjet Combustors](L12-afterburners-ramjet-combustors.md)
- Next: [L14 — Compressors 1](L14-compressors-1.md) — starts the turbomachinery block
- Gas dynamics foundation: [L05 — Gas Dynamics](L05-gas-dynamics.md)
- Rocket nozzles in depth: [L24 — Rocket Engines 2](L24-rocket-engines-2.md)
- Variable nozzle coupling: [L12](L12-afterburners-ramjet-combustors.md)
- Course hub: [EAS4300](../EAS4300.md)
