# L17 — Axial Compressors 4: Multistage and Radial Equilibrium

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 17 · **Date:** Wed 21 Oct 2026
**Book §:** 7.7 *Compressor Efficiency* (p. 319) · 7.8 *Degree of Reaction* (p. 330) — ✅ verified

> 📖 **Reconciled 2026-08-25.** §7.7–7.8 are **Compressor Efficiency** and **Degree of Reaction** —
> both written up on **[L15](L15-compressors-2.md)**, not here.
>
> ⚠️ **This page's original subject, radial equilibrium, is §7.9 — which the syllabus does not assign.**
>
> 🎓 **Updated 2026-09-05 — cross-referenced against lecture slides from a parallel offering**
> (EAS 4300, Section 5041, Spring 2026, a different instructor — Mr. Marcos). That course's own
> "Compressors 4" lecture is **not about radial equilibrium at all** — it's the **compressor
> stability audit**: destabilizing influences on the stall line and operating line (deterioration,
> tip-gap growth, inlet distortion, bleed/power extraction), and a worked "will this engine surge"
> calculation. This is real jet-engine industry practice (GE/P&W-style flow-parameter and
> corrected-flow bookkeeping), not standard textbook material, and it's a natural, high-value sequel
> to [L16](L16-compressors-3.md)'s surge/stall margin content. **§0 below is new** and is now this
> page's primary content; the original radial equilibrium material is kept afterward since it's valid
> book material (§7.9) even though it may not be examinable in your section — confirm with the
> instructor which is actually taught.
**Tags:** #radial-equilibrium #free-vortex #twisted-blades #multistage #annulus-design #work-done-factor #hub-tip-ratio #3d-flow #stage-stacking

*(Fri 23 Oct — no class, review)*

---

## Why this lecture matters

[L14](L14-compressors-1.md)–[L16](L16-compressors-3.md) treated the compressor as **2-D at the mean
radius**. Real blades are 100–500 mm tall and $U = \omega r$ varies by a factor of two from hub to tip.
This lecture is where the design becomes **three-dimensional** — and it explains the most visually
obvious feature of any real compressor blade: **the twist**.

---

## Core concepts

### 0. The compressor stability audit (cross-referenced content — likely this lecture's real subject)

[L16](L16-compressors-3.md) established surge and stall margin at a **single design point**. The
stability audit asks the harder question: **will this specific engine, at this specific flight
condition, with this many hours on it, actually surge?**

#### Basic stall line and basic operating line

Every compressor design has a **basic stall line** — set purely by the designer's choices (solidity,
reaction, blade tip gaps, seal clearances) for a fresh, just-broken-in engine. Plotted against
**corrected flow** $W_c = \dot m\sqrt\theta/\delta$ on the x-axis and pressure ratio $P_3/P_{25}$ on
the y-axis (station 25 = HPC face, station 3 = HPC exit — see
[station-numbering](../../concepts/station-numbering.md)), it is one fixed curve.

The **basic operating line** is a *different* fixed curve, set by the **choked first-stage turbine
nozzle** — recall from [L21](L21-turbines-3.md) that a choked NGV pins $\dot m\sqrt{T_{04}}/p_{04}$ to
a constant, which in turn fixes where the compressor must run for a given corrected speed. The
**basic stall margin** is simply the vertical (pressure-ratio) gap between these two curves at a given
corrected flow.

**The core design tension:** pushing the operating line up (higher OPR, better thermal efficiency,
lower fuel burn) eats directly into stall margin. Every gas turbine cycle decision from
[L06](L06-thermodynamics-of-jet-engines.md) onward is constrained by this picture, not just by
thermodynamics.

#### Destabilizing influences on the operating line

All of these **raise** the operating pressure ratio at a given corrected flow (bad — eats stall margin):

- **Variability** — engine-to-engine build tolerance differences
- **Deterioration** — airfoil/end-wall erosion and wider tip gaps mean the turbine needs a **higher
  $T_4$** to make the same power, and since the choked-NGV flow parameter
  $FP_4 = \dot m\sqrt{T_4}/(P_4 A_4)$ is fixed by geometry, higher $T_4$ forces higher $P_4$ — which
  forces the compressor up the operating line
- **Transient operating line** — during an acceleration, fuel is added faster than the compressor can
  spool up, so $T_4$ spikes momentarily far above its steady-state value at that corrected speed
- **Reynolds number effects** — at altitude, thicker boundary layers cost efficiency, pushing PR up
  for the same work
- **Extractions** — **horsepower extraction (HPX)** for generators/hydraulic pumps needs extra turbine
  work, so higher $T_4$ (small effect at takeoff, large at idle); **compressor bleed** for cabin/avionics
  cooling can go either direction depending on where it's tapped

#### Destabilizing influences on the stall line

All of these **lower** the stall pressure ratio (bad — same effect, opposite mechanism):

- **Variability**, **deterioration** (both as above, but now degrading the *stall* line instead of
  raising the *operating* line)
- **Transient tip gaps** — the single richest mechanism. At low power the tip gap is open; on a rapid
  acceleration the **rotor grows centrifugally and the gap closes almost instantly (seconds)**, but the
  **case grows thermally from compression heating far more slowly (minutes)** — so there's a transient
  window, tens of seconds to a few minutes long, where the gap is at its most open and stall margin is
  at its worst. This is a genuinely different mechanism from steady-state deterioration and is usually
  the single largest term in a takeoff stability audit.
- **Inlet pressure distortion** — a circumferential low-pressure sector (from high-AOA maneuvering,
  crosswinds, ground vortex, wingtip vortex ingestion) makes *that sector* of the compressor operate at
  a locally higher effective pressure ratio, so it stalls first even though the *average* reading looks
  fine
- **Inlet temperature distortion** — a hot sector (tailwind with reingested exhaust, reverser effluent,
  following another aircraft too closely) makes that sector run at a locally lower *corrected* speed,
  driving it toward stall almost instantly. Hard to quantify — the standard mitigation is procedural
  (e.g., a 10-knot tailwind certification limit), not a hardware fix.

#### The stability audit itself

The audit **sums stall-margin losses** (in percentage points) from every mechanism above, at a
specific operating point (typically takeoff), then subtracts from the basic stall margin:

$$
\mathrm{SM}_{\text{remaining}} = \mathrm{SM}_{\text{basic}}
- \sum(\text{operating-line losses}) - \sum(\text{stall-line losses})
- \text{variability} - \text{uncertainty}
$$

Variability and uncertainty are treated **statistically** — audits are commonly run at 2σ (95%
confidence) or 3σ (99.7%). **A positive result at the chosen confidence level means the engine is
predicted stall-free; negative means it will surge.**

---

**Worked example — takeoff stability audit** (adapted from a parallel offering's in-class problem)

A transport engine's HP compressor has **20% basic stall margin** at takeoff, with corrected flow
$W_{25c} = 122.8$ pps, $P_{25}=40$ psia, $T_{25}=280°\mathrm F$, compressor $\gamma=1.35$, combustor
$\Delta T = 1440°\mathrm F$, burner pressure loss 6%, cooling air 27%, $FP_4 = 24$, and a known
sensitivity of **4% stall margin per 0.010″ of additional tip-gap opening**.

**Step 1 — basic engine, from the choked-turbine flow parameter:**

$$
\theta_{25} = \frac{T_{25}+459.67}{518.67} = 1.43, \qquad \delta_{25} = \frac{P_{25}}{14.696} = 2.72
$$

$$
T_3 = 1040°\mathrm F = 1500°\mathrm R, \quad T_4 = T_3 + 1440°\mathrm F = 2940°\mathrm R
$$

$$
P_4 = \frac{\dot m\sqrt{T_4}}{FP_4} = 461.8\ \mathrm{psia}
\;\Rightarrow\;
P_3 = \frac{P_4}{1-0.06} = 491.2\ \mathrm{psia}
$$

$$
\mathrm{CPR} = \frac{P_3}{P_{25}} = 12.28, \qquad \mathrm{CTR} = \frac{T_3}{T_{25}} = 2.03
$$

$$
\eta_c = \frac{\mathrm{CPR}^{(\gamma-1)/\gamma}-1}{\mathrm{CTR}-1} = 0.89
$$

With a transient tip-gap opening of 0.025″ at this point: stall-margin loss $= 4.0 \times 2.5 = 10.0\%$.
Adding 2% variability + 2% uncertainty: **remaining margin $= 20 - 10 - 2 - 2 = 6\%$.** Positive — this
engine is fine new.

**Step 2 — after 10,000 hours**, with $T_3$ up 50°F and $T_4$ up 150°F at the same corrected flow, the
same procedure gives $\mathrm{CPR}=12.69$, $\eta_c = 0.85$ (**4 points lower** — deterioration costs
real efficiency, not just stall margin). The *steady-state* tip gap has also grown 0.008″, costing
another $4.0\times0.8=3.2\%$ on top of the same 10% transient loss:

$$
\mathrm{SM}_{\text{remaining}} = 20 - 10 - 3.2 - 2 - 2 = 2.8\%\; \text{...trending toward } {-0.5\%}
$$

depending on exactly which losses stack — **the audit concludes that at 95% confidence, this
deteriorated engine will surge on a future takeoff.** That single number — not a vague sense that
"the engine is getting old" — is what grounds a fleet or triggers a compressor overhaul program.

### 1. The radial problem

Blade speed varies linearly with radius:

$$
U(r) = \omega r
$$

For a typical hub-tip ratio of 0.5, **the tip moves twice as fast as the hub**. From
[L14](L14-compressors-1.md), the velocity triangles depend on $U$, so a blade designed correctly at the
mean radius is wrong everywhere else:

| Radius | $U$ | Relative flow angle $\beta_1$ | Reaction $R$ |
|---|---|---|---|
| **Hub** | Low | Small | Low (can go negative) |
| **Mean** | Design | Design | ~0.5 |
| **Tip** | High | Large | High |

**Two consequences:**
1. **Blades must be twisted** so the leading edge matches the local flow angle at every radius.
   Untwisted blades would run at huge positive incidence at the hub and negative at the tip.
2. **Reaction must be checked at the hub.** If $R_{hub} < 0$, the hub rotor *accelerates* the relative
   flow (it's acting as a turbine locally) while the hub stator must diffuse impossibly hard.

### 2. Radial equilibrium

Flow with swirl requires a radial pressure gradient to supply the centripetal acceleration. For a fluid
element moving in a circle of radius $r$ with tangential velocity $C_w$:

$$
\frac{1}{\rho}\frac{dp}{dr}=\frac{C_w^2}{r}
$$

**Simple radial equilibrium** — combine this with the definition of stagnation enthalpy and the entropy
relation, assuming no radial velocity component and axisymmetric flow:

$$
\boxed{\ \frac{dh_0}{dr} = T\frac{ds}{dr} + C_a\frac{dC_a}{dr}+\frac{C_w}{r}\frac{d(rC_w)}{dr}\ }
$$

**This is the radial equilibrium equation.** It couples the spanwise distributions of work
($h_0$), axial velocity, and swirl. **You cannot specify all three independently** — pick two and the
third follows.

Assuming uniform work input and uniform entropy (isentropic, $dh_0/dr = 0$, $ds/dr=0$):

$$
C_a\frac{dC_a}{dr} + \frac{C_w}{r}\frac{d(rC_w)}{dr}=0
$$

### 3. Free vortex design

**The classical solution.** Choose the swirl distribution:

$$
C_w\, r = \text{constant} \quad\Longrightarrow\quad C_w \propto \frac{1}{r}
$$

Then $d(rC_w)/dr = 0$, and the equilibrium equation gives:

$$
C_a\frac{dC_a}{dr}=0 \quad\Longrightarrow\quad C_a = \text{constant with radius}
$$

**Why this is elegant:** the axial velocity is uniform across the span, which simplifies the annulus
design enormously. And the work is automatically uniform:

$$
w = U\Delta C_w = \omega r \left(C_{w2}-C_{w1}\right) = \omega\left[(rC_{w2})-(rC_{w1})\right] = \text{const}
$$

Since $rC_w$ is constant at each station, **the work is the same at every radius** — exactly what you
want, because non-uniform work would produce radial temperature gradients and mixing losses.

**Free vortex reaction:**

$$
R(r) = 1 - \frac{k}{r^2}, \qquad k = \frac{C_{w1}+C_{w2}}{2}\bigg|_{\text{mean}} r_m
$$

**The problem:** $R$ falls sharply toward the hub, and for a low hub-tip ratio it can go **negative**.
Also, $C_w \propto 1/r$ means very high swirl at the hub, giving large hub Mach numbers and turning.

**Limits:** free vortex works well for hub-tip ratios above ~0.6–0.7. Below that, hub reaction becomes
unacceptable.

### 4. Alternative vortex designs

Because free vortex has hub problems, other swirl distributions are used:

| Design | Swirl law | Character |
|---|---|---|
| **Free vortex** | $C_w \propto 1/r$ | Uniform work, uniform $C_a$; poor hub reaction |
| **Forced vortex** (solid body) | $C_w \propto r$ | Good hub reaction; **non-uniform work**, needs $C_a$ variation |
| **Constant reaction** | chosen to hold $R$ | Best hub behavior; complex, non-uniform work |
| **Exponential** | $C_w = a \pm b/r$ | A tunable compromise — common in practice |

**The general trade:** free vortex optimizes the *thermodynamics* (uniform work) at the cost of *hub
aerodynamics*. The others sacrifice work uniformity to fix the hub. Modern designs use custom
distributions computed numerically, but free vortex remains the analytical baseline and the one you'll
be examined on.

### 5. Annulus design through the machine

Density rises through the compressor, so the flow area must shrink to keep $C_a$ roughly constant:

$$
A = \frac{\dot m}{\rho C_a}
$$

**Three geometric strategies:**

| Type | Description | Used when |
|---|---|---|
| **Constant tip diameter** | Hub rises through the machine | Common; good for casing manufacture, keeps $U_{tip}$ high |
| **Constant hub diameter** | Tip falls | Keeps hub stresses uniform |
| **Constant mean diameter** | Both converge | Compromise; keeps $U_{mean}$ constant so stage designs are similar |

**Consequences of the shrinking annulus:**
- **Blade height falls dramatically** — a first-stage blade might be 150 mm, a last-stage blade 25 mm
- **Tip clearance becomes a larger fraction of span** ⇒ rear-stage efficiency suffers
  ([L15](L15-compressors-2.md) §4)
- **Aspect ratio and Reynolds number drop** in the rear stages

**This is the fundamental limit on small high-OPR cores.** Scale an engine down and the rear blades get
so short that clearance and Reynolds effects dominate. It's why small engines have lower achievable OPR
than large ones, and why business-jet engines don't simply scale down widebody cores.

### 6. Work-done factor

**A correction you must apply, and a common exam item.**

Euler's equation predicts more work than a real stage delivers. The reason: **endwall boundary layers
grow through the machine**, so the axial velocity profile becomes increasingly non-uniform — peaked in
the middle, deficient near hub and casing. Where $C_a$ is low, incidence rises and the blade actually
turns the flow *less* than intended.

$$
\Delta T_0 = \frac{\lambda\, U \Delta C_w}{c_p}
$$

with $\lambda$ the **work-done factor**:

| Stage | $\lambda$ |
|---|---|
| 1st | 0.98 |
| 2nd | 0.93 |
| 3rd | 0.88 |
| 4th | 0.85 |
| 5th and beyond | 0.83 |

**Note it decreases** as the boundary layers thicken and then stabilizes. Neglecting $\lambda$ makes a
multistage design over-predict pressure ratio by 10–15% — a large error.

**Distinguish it from efficiency.** $\lambda$ reduces the *work actually input* (a flow non-uniformity
effect). $\eta$ describes how efficiently that work becomes pressure (a loss effect). They are
independent corrections and both apply.

### 7. Stage stacking and multistage design

**The design procedure**, which is a plausible exam walkthrough:

1. Fix overall requirements: $\dot m$, $\pi_c$, $N$
2. Choose $U_{tip}$ from mechanical limits (stress) and aerodynamic limits (tip $M_{rel}$)
3. Choose hub-tip ratio at inlet (typically 0.4–0.5 for the first stage)
4. Estimate stage count from an average stage $\Delta T_0$ (25–35 K typical), including $\lambda$
5. Distribute work between stages — **usually less in the first and last stages**, more in the middle
6. Design each stage's mean-radius triangles ([L14](L14-compressors-1.md), [L15](L15-compressors-2.md))
7. Apply a vortex law to get the spanwise variation (§3–4)
8. Check de Haller / diffusion factor **at hub, mean, and tip**
9. Size the annulus stage by stage from density
10. Check tip relative Mach ([L18](L18-transonic-fan-stage.md)) and hub reaction
11. Iterate

**Why the first and last stages take less work:** the first stage has the highest relative Mach number
(cold, and full $U$), so it's Mach-limited. The last stage has the shortest blades and worst clearance
and endwall effects, so it's efficiency-limited.

### 8. Blade stress — the mechanical limit on $U$

Since work scales with $U^2$ ([L14](L14-compressors-1.md)), you always want more blade speed. Stress
stops you.

Centrifugal stress at the blade root of a constant-area blade:

$$
\sigma_{\text{root}} = \rho_m \omega^2 \frac{r_t^2 - r_h^2}{2} = \rho_m \frac{U_t^2}{2}\left[1-\left(\frac{r_h}{r_t}\right)^2\right]
$$

A common and useful form using annulus area:

$$
\sigma_{\text{root}} = \frac{\rho_m\, \omega^2 A}{4\pi}\, K
$$

with $K$ a taper factor (≈0.5–0.7 for tapered blades; 1.0 for constant section).

**Reading it:** stress depends on **$U_t^2$** and on the annulus area, *not* on the number of blades or
chord. Mitigation is by **tapering** the blade (less mass at the tip) and by material choice (titanium
for the front, nickel alloys where it's hot).

**Typical limits:** $U_{tip} \approx 350$–450 m/s for subsonic stages, up to 450–500 m/s for transonic
fans ([L18](L18-transonic-fan-stage.md)). Beyond that, either the disk or the blade root fails.

**The competing limit is aerodynamic:** tip relative Mach number

$$
M_{\text{rel,tip}} = \frac{\sqrt{C_a^2 + U_t^2}}{\sqrt{\gamma R T_1}}
$$

Above $M_{rel} \approx 1$, shock losses appear. Modern fans deliberately exceed this
([L18](L18-transonic-fan-stage.md)); core compressor stages usually don't.

### 9. Modern 3-D blading

Contemporary designs go beyond simple vortex laws:

- **Sweep** — leaning the stacking line axially, which reduces the *component* of Mach number normal to
  the shock and weakens it (the same principle as a swept wing)
- **Lean/bow** — leaning circumferentially to control the spanwise pressure gradient and push
  low-momentum endwall fluid away from the corners
- **End-bend** — extra turning near the endwalls to compensate for the boundary layer
- **Non-axisymmetric endwall contouring** — sculpting the hub surface between blades to weaken the
  passage vortex

These are CFD-driven and yield 1–2% efficiency gains — which, at the scale of a commercial engine
fleet, is worth enormous investment.

---

## Worked logic — free vortex blade twist

**Given:** first stage, $r_h = 0.20$ m, $r_t = 0.40$ m, $r_m = 0.30$ m, $N = 9{,}000$ rpm,
$C_a = 160$ m/s (constant), axial inlet ($C_{w1}=0$), and $\Delta T_0 = 30$ K with
$c_p = 1005$ J/(kg·K).

**Step 1 — blade speeds:**

$$
\omega = \frac{2\pi(9000)}{60}=942.5\ \mathrm{rad/s}
$$

$$
U_h = 942.5(0.20)=188.5, \quad U_m = 942.5(0.30)=282.7, \quad U_t=942.5(0.40)=377.0\ \mathrm{m/s}
$$

**Step 2 — mean-radius swirl requirement:**

$$
\Delta C_{w,m}=\frac{c_p\Delta T_0}{U_m}=\frac{1005\times30}{282.7}=106.6\ \mathrm{m/s}
$$

Since $C_{w1}=0$: $C_{w2,m}=106.6$ m/s.

**Step 3 — free vortex distribution, $rC_{w2}=$ const:**

$$
r_m C_{w2,m} = 0.30\times106.6 = 31.98\ \mathrm{m^2/s}
$$

$$
C_{w2,h}=\frac{31.98}{0.20}=159.9\ \mathrm{m/s}, \qquad C_{w2,t}=\frac{31.98}{0.40}=79.9\ \mathrm{m/s}
$$

**Step 4 — verify uniform work:**

$$
w_h = U_h C_{w2,h}=188.5\times159.9=30{,}141\ \mathrm{J/kg}
$$

$$
w_t = U_t C_{w2,t}=377.0\times79.9=30{,}122\ \mathrm{J/kg}
$$

**Equal to within rounding ✓** — exactly as §3 predicts.

**Step 5 — the twist.** Rotor inlet relative angle at each radius ($C_{w1}=0$, so $W_{w1}=U$):

$$
\beta_{1,h}=\arctan\frac{188.5}{160}=49.7°
$$

$$
\beta_{1,m}=\arctan\frac{282.7}{160}=60.5°
$$

$$
\beta_{1,t}=\arctan\frac{377.0}{160}=67.0°
$$

**The blade must twist by 17.3° from hub to tip** just to match the incoming flow. That's the visible
twist on every compressor blade you've ever seen.

**Step 6 — reaction check:**

$$
R_h = 1 - \frac{C_{w1}+C_{w2,h}}{2U_h}=1-\frac{0+159.9}{2(188.5)}=1-0.424=0.576
$$

$$
R_m = 1 - \frac{106.6}{2(282.7)}=1-0.189=0.811
$$

$$
R_t = 1 - \frac{79.9}{2(377.0)}=1-0.106=0.894
$$

**Hub reaction is acceptable here (0.576 > 0)**, but note it's the lowest — confirming §1. With a lower
hub-tip ratio (say $r_h/r_t = 0.4$), $U_h$ would drop and $C_{w2,h}$ would rise, driving $R_h$ toward
zero. **That's the free-vortex hub limit in action.**

**Step 7 — tip relative Mach number** (with $T_1 = 288$ K):

$$
W_{1,t}=\sqrt{160^2+377^2}=409.5\ \mathrm{m/s}, \qquad a_1 = \sqrt{1.4(287)(288)}=340.2\ \mathrm{m/s}
$$

$$
M_{\text{rel,tip}}=\frac{409.5}{340.2}=1.20
$$

**Transonic** — this stage has shocks at the tip and needs the treatment of
[L18](L18-transonic-fan-stage.md).

---

## Common pitfalls

- **Designing only at the mean radius.** Always check hub and tip.
- **Forgetting hub reaction can go negative** at low hub-tip ratio.
- **Omitting the work-done factor** in multistage estimates — a 10–15% error.
- **Confusing work-done factor with efficiency.** Different corrections, both needed.
- **Assuming $C_a$ is uniform for non-free-vortex designs.** Only free vortex gives that.
- **Thinking blade twist is for structural reasons.** It's aerodynamic — matching local flow angle.
- **Forgetting the annulus must contract** as density rises.
- **Ignoring the rear-stage blade height problem** when scaling engines down.
- **Assuming $U_{tip}$ is limited only by stress.** Tip relative Mach is often the binding constraint.

---

## Exam checklist

- [ ] Explain why $U$ varies with radius and what that does to the triangles
- [ ] **Write the simple radial equilibrium equation and state what it couples**
- [ ] **Derive the free vortex result: $C_w \propto 1/r$ ⇒ $C_a$ uniform ⇒ work uniform**
- [ ] Show $R = 1 - k/r^2$ for free vortex and explain the hub problem
- [ ] Compare free vortex, forced vortex, and constant-reaction designs
- [ ] Explain why blades are twisted and compute the twist angle from hub to tip
- [ ] Define the work-done factor, give typical values, and explain its physical origin
- [ ] Explain why the annulus contracts and what that does to rear-stage efficiency
- [ ] Write the blade root centrifugal stress relation and identify the governing variable
- [ ] Compute tip relative Mach number and say whether the stage is transonic
- [ ] Outline the multistage design procedure

---

## Links

- Previous: [L16 — Compressors 3](L16-compressors-3.md)
- Next: [L18 — Transonic Fan Stage](L18-transonic-fan-stage.md)
- Foundations: [L14 — Compressors 1](L14-compressors-1.md), [L15 — Compressors 2](L15-compressors-2.md)
- Turbine 3-D counterpart: [L20 — Turbines 2](L20-turbines-2.md)
- Concept: [velocity-triangles](../../concepts/velocity-triangles.md)
- Course hub: [EAS4300](../EAS4300.md)
