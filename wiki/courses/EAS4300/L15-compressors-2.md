# L15 — Axial Compressors 2: Reaction, Efficiency, and Losses

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 15 · **Date:** Fri 16 Oct 2026
**Book §:** 7.4 *Characteristic Performance of a Single Compressor Stage* (p. 288) · 7.5 *…of a
Multistage Axial Compressor* (p. 294) — ✅ verified against the book

> 📖 **Reconciled 2026-08-25.** §7.4–7.5 are about **stage and multistage characteristic
> performance** — i.e. **compressor maps, the onset of stall, and surge.** That material is written up
> on **[L16](L16-compressors-3.md)**, not here.
>
> This page covers **degree of reaction and compressor efficiency**, which the book puts in
> **§7.8 and §7.7** — the sections the syllabus assigns to **[L17](L17-compressors-4.md)**.
>
> **The compressor block's content is correct but shifted one page from the book's ordering.** For
> reading, pair this page with §7.7–7.8 and read [L16](L16-compressors-3.md) alongside §7.4–7.5.
> See [textbook-section-map](textbook-section-map.md).
**Tags:** #compressor #degree-of-reaction #polytropic-efficiency #small-stage-efficiency #losses #tip-clearance #secondary-flow #profile-loss #cascade #diffusion-factor

---

## Why this lecture matters

[L14](L14-compressors-1.md) gave you the work input. This lecture answers the two questions that follow:
**how should the pressure rise be split between rotor and stator (reaction), and how much of the work
actually becomes pressure (efficiency and losses)?** It also introduces polytropic efficiency, which is
the correct way to compare machines of different pressure ratios and a very common exam topic.

---

## Core concepts

### 1. Degree of reaction

**Definition** — the fraction of the stage's *static* enthalpy rise that occurs in the rotor:

$$
R = \frac{h_2 - h_1}{h_3 - h_1} = \frac{\Delta h_{\text{rotor}}}{\Delta h_{\text{stage}}}
$$

For a repeating stage ($C_3 = C_1$), $h_3 - h_1 = h_{03}-h_{01} = w$, so:

$$
R = \frac{h_2-h_1}{w}
$$

Using the rothalpy result from [L14](L14-compressors-1.md) ($h_1 + W_1^2/2 = h_2 + W_2^2/2$ for an
axial rotor):

$$
h_2 - h_1 = \frac{W_1^2 - W_2^2}{2} = \frac{W_{w1}^2-W_{w2}^2}{2}
$$

(since $C_a$ is common). With $w = U(C_{w2}-C_{w1}) = U(W_{w1}-W_{w2})$:

$$
R = \frac{W_{w1}^2 - W_{w2}^2}{2U(W_{w1}-W_{w2})} = \frac{W_{w1}+W_{w2}}{2U}
$$

**The two working forms — memorize both:**

$$
R = \frac{W_{w1}+W_{w2}}{2U} = \frac{C_a}{2U}\left(\tan\beta_1 + \tan\beta_2\right)
$$

$$
R = 1 - \frac{C_{w1}+C_{w2}}{2U}
$$

**Interpretation:** $R$ is essentially the *mean tangential velocity in the relative frame*, normalized
by blade speed. It tells you which blade row is doing the diffusing.

### 2. What different reactions mean

| $R$ | Behavior |
|---|---|
| **0** | **Impulse rotor** — no static pressure rise in rotor; all diffusion in the stator |
| **0.5** | **Symmetric** — rotor and stator share the diffusion equally |
| **1.0** | All pressure rise in the rotor; stator does no diffusing |
| **> 1 or < 0** | One row *accelerates* while the other over-diffuses — generally undesirable |

**50% reaction is the standard design choice.** Reasons:

1. **Velocity triangles are symmetric** (mirror images), so rotor and stator blades have the same shape —
   manufacturing and design economy.
2. **Diffusion is split evenly**, so neither row is pushed to its separation limit before the other.
   Since diffusion is the binding constraint ([L14](L14-compressors-1.md) §7), sharing it maximizes
   total achievable pressure rise.
3. **Best stage efficiency** empirically.

At $R = 0.5$ the triangles satisfy:

$$
\beta_1 = \alpha_2, \qquad \beta_2 = \alpha_1, \qquad C_1 = W_2, \qquad C_2 = W_1
$$

**The radial problem.** $R$ depends on $U = \omega r$, which varies strongly from hub to tip. A stage
designed for $R=0.5$ at the mean radius will have **lower $R$ at the hub** (small $U$) and **higher $R$
at the tip**. If the hub reaction goes negative, the hub rotor *accelerates* the flow and the hub stator
must diffuse impossibly hard. This is a real design constraint on hub-tip ratio and is the motivation
for the twisted blades of [L17](L17-compressors-4.md).

### 3. Isentropic vs. polytropic efficiency

**Isentropic (adiabatic) efficiency**, from [L06](L06-thermodynamics-of-jet-engines.md):

$$
\eta_c = \frac{T_{03s}-T_{01}}{T_{03}-T_{01}}
= \frac{\pi_c^{\frac{\gamma-1}{\gamma}}-1}{\tau_c - 1}
$$

**The problem with it:** isentropic efficiency **depends on pressure ratio** even for stages of identical
aerodynamic quality. Comparing a 1.4:1 stage to a 20:1 machine on isentropic efficiency is comparing
apples to oranges.

**Why — the preheat effect.** In a multistage compressor, each stage's losses heat the gas, so the next
stage takes in hotter air. Since constant-pressure lines **diverge** on a $T$-$s$ diagram, that hotter
inlet means the next stage needs *more* work for the same pressure ratio. The losses compound. **The
whole is less efficient than each of its parts**, and increasingly so as pressure ratio rises.

**Polytropic (small-stage / infinitesimal-stage) efficiency** fixes this by defining efficiency for an
infinitesimal pressure rise:

$$
\eta_p = \frac{dh_s}{dh}=\frac{\frac{\gamma-1}{\gamma}\frac{dp}{p}}{\frac{dT}{T}}
$$

Integrating:

$$
\boxed{\ \eta_{p,c} = \frac{\frac{\gamma-1}{\gamma}\ln\pi_c}{\ln\tau_c}\ }
$$

Rearranged — the **relation you'll actually use**:

$$
\tau_c = \pi_c^{\frac{\gamma-1}{\gamma\,\eta_{p,c}}}
$$

**Conversion between the two:**

$$
\eta_c = \frac{\pi_c^{\frac{\gamma-1}{\gamma}}-1}{\pi_c^{\frac{\gamma-1}{\gamma\eta_{p,c}}}-1}
$$

**Key facts:**
- **For a compressor, $\eta_c < \eta_p$**, and the gap widens with $\pi_c$
- **For a turbine, $\eta_t > \eta_p$** — the sign flips, because reheat *helps* the downstream stages
  ([L20](L20-turbines-2.md))
- Polytropic efficiency measures **aerodynamic quality**; isentropic measures **overall machine
  performance**

**Illustration** — with $\eta_p = 0.90$, $\gamma = 1.4$:

| $\pi_c$ | $\eta_c$ |
|---|---|
| 1.4 | 0.894 |
| 5 | 0.878 |
| 20 | 0.855 |
| 40 | 0.842 |

**Same aerodynamic quality, 5 points of isentropic efficiency lost purely to pressure ratio.** This is
why manufacturers quote polytropic efficiency when comparing compressor technology.

### 4. Where the losses come from

Roughly the breakdown for a modern axial stage:

| Loss | Share | Cause |
|---|---|---|
| **Profile loss** | ~35% | Blade surface boundary layers and wake mixing |
| **Tip clearance loss** | ~25% | Leakage over unshrouded rotor tips |
| **Secondary flow (endwall)** | ~30% | Hub/casing boundary layers, passage vortices |
| **Shock loss** | 0–20% | Only in transonic stages ([L18](L18-transonic-fan-stage.md)) |

**Profile loss.** Boundary layers on suction and pressure surfaces, plus mixing of the wake downstream.
Grows sharply as diffusion approaches the separation limit — which is why the de Haller and diffusion-
factor limits exist.

**Tip clearance loss.** The rotor tip is unshrouded (for stress reasons) so there's a gap to the casing.
Pressure-side air leaks over the tip, forming a **tip leakage vortex** that both blocks the passage and
mixes losses in.

$$
\Delta\eta \approx 1.5\text{–}3\% \ \text{per 1\% of } \frac{\text{clearance}}{\text{blade height}}
$$

**A hugely nonlinear payoff.** Typical clearances are 0.5–1% of span, and getting there is why engines
use **active clearance control** (blowing cooling air on the casing to shrink it at cruise). It's also
why the *last* compressor stages, with short blades, suffer most — the same absolute clearance is a
larger fraction of a 25 mm blade than of a 150 mm one. This directly limits how small the core of a
high-OPR engine can be.

**Secondary flows.** In the endwall boundary layer the axial momentum is low, so the same blade-to-blade
pressure gradient over-turns that fluid, generating **passage vortices** that migrate and mix.

**Shock loss.** Above relative Mach ~1, shocks appear on the blade. → [L18](L18-transonic-fan-stage.md)

### 5. Cascade testing and loss coefficients

A **cascade** is a linear row of blades in a wind tunnel — the standard way to measure 2-D blade
performance before building a machine.

**Total pressure loss coefficient:**

$$
\bar\omega = \frac{p_{01}-p_{02}}{p_{01}-p_1} = \frac{\Delta p_0}{\tfrac{1}{2}\rho W_1^2}
$$

**Static pressure rise coefficient:**

$$
C_p = \frac{p_2-p_1}{\tfrac{1}{2}\rho W_1^2}
$$

**Deviation.** Flow does **not** leave exactly along the blade metal angle — it under-turns. Carter's
rule:

$$
\delta = m\,\theta\sqrt{\frac{s}{c}}
$$

with $\theta$ the blade camber, $s/c$ the pitch-chord ratio, and $m \approx 0.23$–0.26 for compressors.
**Blades must therefore be cambered *more* than the desired turning.** Ignoring deviation gives an
under-performing stage — a classic design and exam trap.

**Incidence.** The difference between flow angle and blade inlet angle. There's a **loss bucket** — a
range of incidence with low loss, bounded by:
- **Positive stall** (too much incidence, suction-surface separation) — the compressor stall mechanism
- **Negative stall** (too little/negative incidence, pressure-surface separation)

The bucket's width sets the stage's operating range and is the microscopic origin of the surge margin
in [L16](L16-compressors-3.md).

### 6. Blade geometry

**Nomenclature:** chord $c$, pitch/spacing $s$, camber angle $\theta$, stagger angle $\xi$,
solidity $\sigma = c/s$, aspect ratio $h/c$, thickness-to-chord $t/c$.

**Design guidance:**
- **Solidity** 1.0–1.5 for compressors. Higher solidity spreads the loading (allows more turning per
  row via the diffusion factor) but adds wetted area, weight, and profile loss.
- **Zweifel / optimum pitch** — the classical criterion for choosing $s/c$ to balance those effects.
- **Aspect ratio** has fallen dramatically in modern designs (from ~4 to ~1.5). Low aspect ratio blades
  are more robust to foreign object damage, need fewer parts, and handle endwall flows better.
- **Blade profiles:** NACA 65-series and C-series historically; modern designs use **controlled
  diffusion airfoils (CDA)** with custom-tailored surface velocity distributions, and **3-D bowed/swept**
  stacking to manage endwall losses.

---

## Worked logic — a 50% reaction stage

**Given:** $U = 280$ m/s, $C_a = 160$ m/s, $R = 0.5$, target $\Delta T_0 = 25$ K,
$c_p = 1005$ J/(kg·K), $T_{01}=350$ K, $\eta_p = 0.90$, $\gamma=1.4$.

**Step 1 — required swirl change:**

$$
\Delta C_w = \frac{c_p \Delta T_0}{U}=\frac{1005\times25}{280}=89.7\ \mathrm{m/s}
$$

**Step 2 — apply $R = 0.5$:**

$$
R = 1 - \frac{C_{w1}+C_{w2}}{2U}=0.5
\quad\Longrightarrow\quad
C_{w1}+C_{w2}=U=280\ \mathrm{m/s}
$$

Combined with $C_{w2}-C_{w1}=89.7$:

$$
C_{w2}=\frac{280+89.7}{2}=184.9\ \mathrm{m/s}, \qquad C_{w1}=\frac{280-89.7}{2}=95.2\ \mathrm{m/s}
$$

**Step 3 — all four angles:**

$$
\alpha_1 = \arctan\frac{95.2}{160}=30.7°, \qquad \alpha_2 = \arctan\frac{184.9}{160}=49.1°
$$

$$
W_{w1}=280-95.2=184.8 \;\Rightarrow\; \beta_1 = \arctan\frac{184.8}{160}=49.1°
$$

$$
W_{w2}=280-184.9=95.1 \;\Rightarrow\; \beta_2 = \arctan\frac{95.1}{160}=30.7°
$$

**Check the 50%-reaction symmetry:** $\beta_1 = \alpha_2 = 49.1°$ and $\beta_2 = \alpha_1 = 30.7°$ ✓
Exactly as §2 predicts — the triangles are mirror images.

**Step 4 — de Haller check:**

$$
W_1 = \sqrt{160^2+184.8^2}=244.4, \qquad W_2=\sqrt{160^2+95.1^2}=186.1
$$

$$
\mathrm{DH}=\frac{186.1}{244.4}=0.761 \ \ge 0.72\ \checkmark
$$

And by symmetry the stator sees $C_2 \to C_3$ with the same ratio — both rows equally loaded, which is
precisely the benefit of $R = 0.5$.

**Step 5 — stage pressure ratio using polytropic efficiency:**

$$
\tau_{\text{stage}}=\frac{350+25}{350}=1.0714
$$

$$
\pi_{\text{stage}} = \tau^{\frac{\gamma\eta_p}{\gamma-1}} = (1.0714)^{\frac{1.4\times0.90}{0.4}}
= (1.0714)^{3.15} = 1.238
$$

**Step 6 — isentropic efficiency of this stage:**

$$
\eta_{\text{stage}} = \frac{\pi^{\frac{\gamma-1}{\gamma}}-1}{\tau-1}
=\frac{(1.238)^{0.2857}-1}{0.0714}=\frac{0.0632}{0.0714}=0.885
$$

**Note $\eta_{\text{stage}} = 0.885 < \eta_p = 0.90$** — the gap is small here because the stage pressure
ratio is small. Stack ten of these stages to $\pi_c = 8$ and the overall isentropic efficiency falls to
~0.87 while the polytropic stays at 0.90. **That growing gap is the preheat effect made concrete.**

---

## Common pitfalls

- **Confusing $R$ with efficiency.** Reaction is a *split of pressure rise*, not a quality measure.
- **Forgetting $R$ varies with radius.** Designed at the mean; check the hub.
- **Using isentropic efficiency to compare machines of different $\pi$.** Use polytropic.
- **Getting the compressor/turbine polytropic inequality backwards.** Compressor $\eta_c < \eta_p$;
  turbine $\eta_t > \eta_p$.
- **Ignoring deviation.** Blades must be over-cambered.
- **Assuming tip clearance loss is small.** It's ~25% of stage loss and highly nonlinear.
- **Applying the $R=0.5$ symmetry relations when $R \ne 0.5$.**
- **Forgetting to check de Haller** after setting the triangles.

---

## Exam checklist

- [ ] **Define degree of reaction and derive $R = (W_{w1}+W_{w2})/2U$**
- [ ] Write both working forms of $R$ and convert between them
- [ ] Explain why 50% reaction is standard (three reasons)
- [ ] State the $R=0.5$ angle symmetries and verify them on a triangle
- [ ] Explain why $R$ varies with radius and what goes wrong at the hub
- [ ] **Define polytropic efficiency and derive $\tau_c = \pi_c^{(\gamma-1)/(\gamma\eta_p)}$**
- [ ] Explain the preheat effect and why $\eta_c < \eta_p$ for compressors
- [ ] List the four loss mechanisms with approximate shares
- [ ] State the tip clearance sensitivity and explain why rear stages suffer most
- [ ] Define $\bar\omega$, $C_p$, deviation, incidence, and the loss bucket
- [ ] Design a 50% reaction stage from $U$, $C_a$, and target $\Delta T_0$

---

## Links

- Previous: [L14 — Compressors 1](L14-compressors-1.md)
- Next: [L16 — Compressors 3](L16-compressors-3.md) — maps, stall, surge
- Turbine counterpart: [L20 — Turbines 2](L20-turbines-2.md)
- Concept: [velocity-triangles](../../concepts/velocity-triangles.md)
- Course hub: [EAS4300](../EAS4300.md)
