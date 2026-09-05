# L18 — Transonic Fan Stage

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 18 · **Date:** Mon 26 Oct 2026
**Book §:** 7.11 *Transonic Fan Stage* (p. 345) — ✅ verified · **HW7 assigned** *(§7.9 Radial Equilibrium and §7.10 Subsonic Compressor Design are skipped)*
**Tags:** #transonic-fan #relative-mach #shock-in-rotor #swept-blade #wide-chord #unique-incidence #flutter #blisk #fan-blade-off

---

## Why this lecture matters

The fan is the largest, most visible, and most thrust-critical component of a modern turbofan — it
produces ~80% of the thrust at $\alpha = 10$ ([L08b](L08b-turbofans.md)). And it is the one compressor
stage that runs **deliberately supersonic** in the relative frame. This lecture is where compressor
aerodynamics ([L14](L14-compressors-1.md)–[L17](L17-compressors-4.md)) meets the shock physics of
[L05](L05-gas-dynamics.md).

---

## Core concepts

### 1. Why fans go transonic

From Euler ([L14](L14-compressors-1.md)), work scales with $U$:

$$
w = U\Delta C_w
$$

A fan must produce $\pi_f \approx 1.5$–1.7 in a **single stage** (multiple fan stages would be heavy and
would defeat the point of a big, simple fan). That demands high $U$.

Fan tip speeds: **400–500 m/s**. With inlet air at 288 K ($a = 340$ m/s):

$$
M_{\text{rel,tip}} = \frac{\sqrt{C_a^2 + U_t^2}}{a} = \frac{\sqrt{200^2+450^2}}{340}=\frac{492}{340}=1.45
$$

**Supersonic in the relative frame.** Note the flow is comfortably **subsonic in the absolute frame**
($M \approx 0.6$) — the aircraft isn't supersonic, only the blade relative to the air is. Getting this
distinction right is essential.

**The spanwise variation** is the defining feature of a fan blade:

| Radius | $M_{rel}$ | Regime |
|---|---|---|
| Hub | 0.7–0.8 | **Subsonic** — conventional design |
| Mid | 1.0–1.1 | **Transonic** — mixed |
| Tip | 1.3–1.5 | **Supersonic** — shock-dominated |

**One blade must work in three different aerodynamic regimes simultaneously.** That's what makes fan
design uniquely hard, and why fan blades look so different from core compressor blades.

### 2. The shock structure in a transonic rotor

At supersonic relative inlet Mach, a shock system forms in the blade passage.

**At design (started) condition:**
- A **bow/leading-edge shock** from each blade, mostly swallowed into the passage
- A **passage shock** spanning between adjacent blades, roughly normal to the flow
- The flow behind the passage shock is **subsonic**, and the rear of the passage diffuses conventionally

**The design intent:** use the shock to do most of the compression (a shock is a very compact
compressor), then diffuse subsonically. The trade is the $p_0$ loss from
[L05](L05-gas-dynamics.md) §6.

**Shock loss depends steeply on the pre-shock Mach number:**

| $M_{rel}$ | $p_{02}/p_{01}$ | Loss |
|---|---|---|
| 1.1 | 0.9989 | Negligible |
| 1.3 | 0.979 | 2% |
| 1.5 | 0.930 | 7% |
| 1.7 | 0.856 | 14% |

**Which is why $M_{rel,tip}$ is kept ≲1.5** — beyond that, shock loss eats the benefit of the higher
work.

### 3. Unique incidence — the transonic operating constraint

**A key concept specific to supersonic cascades, and very examinable.**

In **subsonic** flow, a blade row accepts a range of incidence angles (the "loss bucket" of
[L15](L15-compressors-2.md)) because upstream influence lets the flow adjust to the blade.

In **supersonic** relative inflow, **the flow cannot be influenced upstream** ([L05](L05-gas-dynamics.md)
§1). The inlet flow angle is therefore **determined by the blade geometry and the inlet Mach number
alone** — not by downstream conditions. This is the **unique incidence** (or "unique incidence
relation") condition.

**Consequences:**
- For a given $M_{rel}$, there is essentially **one** inlet flow angle the passage will accept
- The blade cannot adapt to off-design incidence the way a subsonic blade can
- **Mass flow becomes nearly independent of pressure ratio** at high corrected speed — this is exactly
  why the high-speed lines on a fan map are almost **vertical** ([L16](L16-compressors-3.md) §2)
- Back pressure changes move the passage shock's position, not the inlet condition

**Started vs. unstarted:** if the back pressure is too high, the passage shock is expelled ahead of the
blade row (an **unstarted** rotor), mass flow drops abruptly, and the fan surges. This is the same
Kantrowitz physics as the supersonic inlet ([L10](L10-inlets.md) §7), applied to a rotating cascade.

### 4. Blade design features

Transonic fan blades look nothing like core compressor blades, and each feature has a reason:

**Sharp, thin leading edge.** A blunt LE would generate a strong detached bow shock. Thickness-to-chord
at the tip is ~2%, versus ~8–10% at the hub. This makes the tip vulnerable to damage and erosion.

**Low camber at the tip.** Supersonic flow tolerates very little turning before the shock strengthens
unacceptably. The tip does most of its compression *through* the shock, not by turning.

**Sweep.** The stacking line is leaned axially so that the Mach component *normal to the shock* is
reduced — the same principle as a swept wing:

$$
M_{\text{normal}} = M_{\text{rel}}\cos\Lambda
$$

Forward sweep at the tip is common on modern fans. It reduces shock strength, shifts the shock
position, and improves stall margin.

**Wide chord.** Modern fan blades are **wide-chord** and un-snubbered. Older designs used a **part-span
shroud (snubber/clapper)** — a mid-span connection between blades for flutter stiffness — which cost
2–3% efficiency by sitting in the flow. Wide-chord blades are stiff enough without it. The efficiency
gain from deleting the snubber was worth the manufacturing difficulty.

**Hollow titanium / composite construction.** A wide-chord solid titanium blade would be far too heavy
(both for the blade and for the containment case and disk that must survive it). Solutions:
- **Hollow titanium** with an internal truss or honeycomb (diffusion-bonded, superplastically formed)
- **Carbon fibre composite** with a titanium leading-edge sheath for bird/erosion protection (GE90,
  GEnx, LEAP)

**Blisk (integrally bladed rotor).** Blades machined from a single disk forging — no dovetail roots.
Lighter and eliminates a leakage path, but a damaged blade means replacing the whole disk. Common in
core compressors and military fans, less so in large civil fans where repairability matters.

### 5. Aeroelasticity — flutter

Long, thin, fast blades are prone to **flutter** — a self-excited aeroelastic instability where blade
motion extracts energy from the flow, growing until failure.

**Types on a fan map:**

| Flutter type | Where it appears |
|---|---|
| **Subsonic/transonic stall flutter** | High incidence, near the surge line at part speed |
| **Choke flutter** | Negative incidence, at high flow / low pressure ratio |
| **Supersonic unstalled flutter** | High speed, high $M_{rel}$ |
| **Supersonic stall flutter** | High speed near surge |

**Flutter boundaries are plotted on the fan map alongside the surge line**, and the usable operating
region is bounded by both. A fan can be surge-limited in one region and flutter-limited in another.

**Mitigation:** wide chord (higher natural frequency), sweep, deliberate **mistuning** (slightly
different blade frequencies around the disk, which disrupts the coherent traveling-wave mode), and
friction dampers at the blade root.

**Forced response** is the related but distinct problem: blades passing through wakes from upstream
struts or vanes get periodic excitation. If an excitation frequency coincides with a blade natural
frequency, high-cycle fatigue follows. **Campbell diagrams** (frequency vs. rotor speed, with engine
order lines) are used to ensure resonances fall outside the operating range.

### 6. Fan blade off (FBO) — the structural design case

**A certification requirement that shapes the entire engine**: the engine must contain a released fan
blade at maximum speed without hazardous debris escaping, and must be safely shut down.

**Consequences that ripple through the design:**
- A **containment case** — Kevlar wrap or a thick metallic ring — heavy, and a significant fraction of
  nacelle weight
- The **imbalance loads** after blade loss are enormous, and the whole engine mount and pylon structure
  must survive spool-down through resonance
- **Fuse/decoupler bearings** are designed to fail in a controlled way to shed the imbalance load path

This is a major driver of fan blade material choice: composite blades are lighter, which makes the
containment problem smaller, which saves further weight — a compounding benefit.

### 6b. Certification testing beyond FBO (cross-referenced content)

*Cross-referenced against lecture slides from a parallel Spring 2026 offering (Section 5041,
Mr. Marcos) — real certification requirements, not standard textbook material, and a natural
complement to §6's structural design case.*

FBO is the best-known certification test, but a transonic fan carries several other design
requirements simultaneously:

- **Structural/unsteady inflow** — must tolerate crosswind- and vortex-induced flow distortion without
  snubbers (mid-span shrouds), which the transonic, high-solidity blade shape already helps avoid
  (§4).
- **Crosswinds** — certified up to **35 knots**, via a crosswind generator rig at takeoff power,
  checked against both the fan's stall limit and blade vibratory-stress limits. Crosswind-induced
  inlet flow separation is a distortion mechanism, not merely an aerodynamic nuisance — see
  [L17 §0](L17-compressors-4.md) on inlet distortion's effect on stall margin.
- **Ground vortex ingestion** — at high power near the ground, a low-pressure vortex can pull debris
  and unsteady air into the inlet, exciting blade vibration resonances. Certification tests include a
  representative ground plane to let the vortex form.
- **Water and hail ingestion** — a structural concern for the fan (impact, erosion — one reason many
  wide-chord fan leading edges are titanium even when the rest of the blade is composite) and an
  **operability** concern downstream (compressor stall, combustor blowout at high enough
  concentration). Typical requirement: reliable operation up to **20 g/m³** water concentration; the
  engine must recover to **≥75% power within 3 minutes** of the test.
- **Bird strike (14 CFR Part 33.76)** — two distinct tests. A **flocking-bird test** (up to 7
  medium birds or 16 small birds ingested simultaneously) requires **≤25% thrust loss** and continued
  operation for **≥20 minutes**. A **large-bird test** (~5.5 lb, single bird) only requires a **safe
  shutdown** — no fire, no uncontained failure, no departure from the wing; thrust after impact is not
  required.
- **Fan blade out (14 CFR Part 33.94)** — the quantitative version of §6: blade(s) released at redline
  via an explosive bolt at the root must be **contained**, and the engine must run **≥15 s** or shut
  down safely.

**The pattern across all of these:** certification draws a hard line between tests that require
*continued safe operation* (bird flock, crosswind, water/hail) and tests that only require *safe
failure* (large bird, blade-out). Knowing which category a given threat falls into is a common
conceptual exam question.

### 7. The fan as a two-part machine

Because the fan feeds two different destinations, the hub and tip do genuinely different jobs:

- **Fan tip (bypass stream)** — supersonic relative flow, moderate pressure ratio, feeds the bypass
  duct and the majority of thrust
- **Fan hub (core stream)** — subsonic relative flow, feeds the LP compressor/booster and then the core

Their pressure ratios differ, and the hub often needs a **different pressure ratio** than the tip to
match the core's requirements. This is one more reason fan blades are so heavily twisted and
custom-tailored spanwise, beyond the simple vortex laws of [L17](L17-compressors-4.md).

**OGVs (Outlet Guide Vanes)** downstream of the fan remove the swirl before the bypass nozzle — residual
swirl would be wasted kinetic energy and would not contribute axial thrust. OGV count and spacing are
also acoustically tuned: the fan/OGV blade-count ratio is chosen to make the fundamental
rotor-stator interaction tone **cut off** (non-propagating) in the duct.

---

## Worked logic — transonic fan stage at the tip

**Given:** $r_t = 1.0$ m, $N = 4{,}000$ rpm, $C_a = 200$ m/s, axial inlet ($C_{w1}=0$), sea-level
static ($T_{01}=288$ K, $p_{01}=101.3$ kPa), target $\pi_f = 1.6$ at the tip, $\eta_p=0.90$.

**Step 1 — tip speed:**

$$
\omega = \frac{2\pi(4000)}{60}=418.9\ \mathrm{rad/s}, \qquad U_t = 418.9\times1.0=418.9\ \mathrm{m/s}
$$

**Step 2 — relative inlet velocity and Mach.** With $C_{w1}=0$, $W_{w1}=U_t$:

$$
W_1 = \sqrt{C_a^2+U_t^2}=\sqrt{200^2+418.9^2}=464.2\ \mathrm{m/s}
$$

Static temperature at inlet (need it for $a$):

$$
C_1 = C_a = 200\ \mathrm{m/s} \;\Rightarrow\; T_1 = 288 - \frac{200^2}{2(1005)}=288-19.9=268.1\ \mathrm{K}
$$

$$
a_1 = \sqrt{1.4(287)(268.1)}=328.2\ \mathrm{m/s}
$$

$$
M_{\text{rel},1}=\frac{464.2}{328.2}=1.41
$$

**Supersonic relative flow — this is a transonic fan tip.** (Absolute Mach is only
$200/328.2 = 0.61$ — subsonic, as expected.)

$$
\beta_1 = \arctan\frac{418.9}{200}=64.5°
$$

**Step 3 — required work for $\pi_f = 1.6$:**

$$
\tau_f = \pi_f^{\frac{\gamma-1}{\gamma\eta_p}}=(1.6)^{\frac{0.4}{1.4\times0.9}}=(1.6)^{0.3175}=1.1590
$$

$$
\Delta T_0 = 288(1.1590-1)=45.8\ \mathrm{K}
$$

$$
\Delta C_w = \frac{c_p\Delta T_0}{U_t}=\frac{1005\times45.8}{418.9}=109.9\ \mathrm{m/s}
$$

**Step 4 — exit triangle:**

$$
C_{w2}=109.9\ \mathrm{m/s}, \qquad W_{w2}=418.9-109.9=309.0\ \mathrm{m/s}
$$

$$
W_2 = \sqrt{200^2+309.0^2}=367.9\ \mathrm{m/s}, \qquad \beta_2 = \arctan\frac{309.0}{200}=57.1°
$$

**Step 5 — de Haller check:**

$$
\mathrm{DH}=\frac{367.9}{464.2}=0.793 \ \ge 0.72\ \checkmark
$$

**Note the turning is only $\beta_1 - \beta_2 = 64.5° - 57.1° = 7.4°$** — very low camber, exactly as
§4 describes. The tip achieves its pressure ratio mostly *through the shock*, not by turning the flow.

**Step 6 — estimate shock loss.** Treating the passage shock as normal at $M_{rel}=1.41$:

$$
\frac{p_{02}}{p_{01}}\bigg|_{\text{shock}} \approx 0.952
$$

**~4.8% stagnation pressure loss from the shock alone.** That is a substantial part of the stage's total
loss budget and explains why $\eta_p$ for a transonic fan tip (~0.88–0.90) is lower than for a good
subsonic stage (~0.92).

**Step 7 — what sweep buys.** With 30° of tip sweep:

$$
M_{\text{normal}}=1.41\cos(30°)=1.22
$$

$$
\frac{p_{02}}{p_{01}}\bigg|_{\text{shock}} \approx 0.9884
$$

**Shock loss falls from 4.8% to 1.2%.** That single geometric change recovers ~3.5 points of stagnation
pressure — which is why every modern fan blade is swept, and why the swept fan was one of the most
significant turbomachinery advances of the 1990s.

---

## Common pitfalls

- **Confusing relative and absolute Mach number.** The aircraft is subsonic; the *blade relative* flow
  is supersonic. State which you mean.
- **Applying subsonic incidence reasoning to a supersonic cascade.** Unique incidence removes the
  freedom.
- **Assuming a fan blade has one aerodynamic regime.** Hub subsonic, tip supersonic, on the same blade.
- **Expecting high camber at the tip.** It's nearly flat — 5–10° of turning.
- **Forgetting the $\cos\Lambda$ sweep benefit.**
- **Treating flutter as the same thing as surge.** Different physics; separate boundaries on the map.
- **Ignoring that fan hub and tip may need different pressure ratios** (core vs. bypass).
- **Assuming blisks are always better.** They're lighter but not repairable blade-by-blade.
- **Neglecting the fan-blade-off case** when asked why the fan drives engine structural design.

---

## Exam checklist

- [ ] **Compute $M_{rel,tip}$ and distinguish it from absolute Mach**
- [ ] Explain why fans must run transonic (Euler + single-stage $\pi_f$ requirement)
- [ ] Describe the shock structure in a transonic rotor passage
- [ ] Give shock $p_0$ loss vs. $M_{rel}$ and explain the ~1.5 design ceiling
- [ ] **Explain unique incidence and why it makes high-speed map lines vertical**
- [ ] List transonic blade design features (thin LE, low tip camber, sweep, wide chord) with reasons
- [ ] **Compute the sweep benefit via $M_n = M_{rel}\cos\Lambda$**
- [ ] Name the flutter types and where each sits on the map
- [ ] Explain mistuning and Campbell diagrams
- [ ] Explain why fan blade off drives containment, materials, and mounts
- [ ] Explain why the fan hub and tip do different jobs

---

## Links

- Previous: [L17 — Compressors 4](L17-compressors-4.md)
- Next: [L19 — Turbines 1](L19-turbines-1.md) — turbomachinery, but with a favorable gradient
- Fan in the cycle: [L08b — Turbofans](L08b-turbofans.md)
- Shock physics: [L05 — Gas Dynamics](L05-gas-dynamics.md)
- Map behavior: [L16 — Compressors 3](L16-compressors-3.md)
- Concept: [velocity-triangles](../../concepts/velocity-triangles.md)
- Course hub: [EAS4300](../EAS4300.md)
