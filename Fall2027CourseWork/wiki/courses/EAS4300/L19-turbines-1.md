# L19 — Axial Turbines 1: Velocity Triangles and Stage Work

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 19 · **Date:** Wed 28 Oct 2026
**Book §:** 8.1 *Introduction* (p. 367) · 8.2 *The Axial Turbine Stage* (p. 370) · 8.3 *Stage Efficiency* (p. 377) — ✅ verified
**Tags:** #turbine #axial #velocity-triangles #nozzle-guide-vane #impulse #reaction #stage-loading #smith-chart #favorable-gradient

---

## Why this lecture matters

The turbine is the compressor run backwards — same Euler equation, same velocity triangles, opposite
sign. But the **favorable pressure gradient** changes everything about what's achievable: a turbine can
do in 2 stages what a compressor needs 15 for. This lecture establishes the turbine triangles and the
impulse/reaction spectrum.

---

## Core concepts

### 1. Turbine stage layout — note the order reverses

```
[ Nozzle Guide Vane (stator) ] → [ Rotor ]
              ↑                      ↑
      accelerates + swirls     extracts work
```

**Compare with a compressor** ([L14](L14-compressors-1.md)): rotor first, then stator. In a turbine the
**stationary row comes first**. That's not arbitrary — the NGV's job is to accelerate the flow and give
it swirl *before* the rotor can extract it.

**Nozzle Guide Vane (NGV) / stator.**
- **Accelerates** the flow (converging passage, falling pressure)
- Adds large swirl — typically turning to $\alpha_1 = 65$–75° from axial
- **No work:** $T_{01} = T_{00}$ across it, but $p_0$ drops slightly (loss)
- Sees the hottest gas in the engine — station 4, directly out of the combustor

**Rotor.**
- **Extracts work.** $T_0$ and $p_0$ both fall
- Removes the swirl the NGV added
- In the relative frame, the flow **accelerates** (favorable gradient) — the opposite of a compressor
  rotor

### 2. Turbine velocity triangles

Same notation as [L14](L14-compressors-1.md): $C$ absolute, $W$ relative, $U = \omega r$ blade speed,
$C_a$ axial, subscript convention here:

| Station | Location |
|---|---|
| 0 | NGV inlet |
| 1 | NGV exit = rotor inlet |
| 2 | Rotor exit |

$$
C_w = C_a\tan\alpha, \qquad W_w = C_a\tan\beta, \qquad U = C_{w} - W_{w}
$$

**Note the sign convention differs from the compressor** because the swirl and blade speed are in the
same direction at rotor inlet. Many texts write $U = C_{w1} + W_{w1}$ with $W_{w1}$ defined negative.
**Pick a convention, draw the triangle, and stay consistent** — this is where most turbine errors come
from.

**What happens across the stage:**
- **NGV (0→1):** $C_1 \gg C_0$, large swirl added, $\alpha_1 \approx 70°$
- **Rotor (1→2):** $C_2 < C_1$ (absolute — energy extracted), $W_2 > W_1$ (relative — accelerating),
  swirl removed so $\alpha_2 \approx 0$ ideally

### 3. Euler's equation — same equation, opposite sign

$$
w = U\left(C_{w1}-C_{w2}\right) = U\,\Delta C_w
$$

$$
\Delta T_0 = \frac{U\Delta C_w}{c_p}
$$

**Sign convention:** for a turbine, $C_{w1} > C_{w2}$, so $w > 0$ means **work out**. The compressor
formula $w = U(C_{w2}-C_{w1})$ gives work *in*. Same physics, opposite direction.

For the common design case of **axial exit** ($C_{w2}=0$, no residual swirl):

$$
w = U\,C_{w1}
$$

Maximum work for a given blade speed and NGV exit swirl.

### 4. The favorable pressure gradient — why turbines are easy

**The single most important qualitative contrast in the course.**

| | **Compressor** | **Turbine** |
|---|---|---|
| Pressure gradient | Adverse (rising $p$) | **Favorable** (falling $p$) |
| Boundary layer | Wants to separate | Stays attached, thin |
| Turning per row | 20–45° | **70–120°** |
| $\Delta T_0$ per stage | 25–35 K | **150–300 K** |
| Stages for a gas generator | 10–15 | **1–2** |
| Blade shape | Thin, low camber | Thick, highly cambered |

**A turbine blade can turn the flow through 100°+ without separating**, because the accelerating flow
continuously thins the boundary layer. A compressor blade attempting the same would separate
catastrophically.

**The design consequence:** a modern two-spool engine might have 1 HP turbine stage driving 10 HP
compressor stages, and 5 LP turbine stages driving a fan. The turbine is compact and the compressor is
long — go look at any engine cutaway and this asymmetry is visually obvious.

**Corollary for the exam:** if asked "why does a turbine need fewer stages," the answer is *not* "because
it's hotter" or "because the gas is expanding." It's the **boundary layer behavior under a favorable
pressure gradient.**

### 5. Degree of reaction for turbines

Same definition as [L15](L15-compressors-2.md) — the share of the *static* enthalpy drop in the rotor:

$$
R = \frac{h_1 - h_2}{h_0 - h_2} = \frac{\text{static drop in rotor}}{\text{static drop in stage}}
$$

Working form:

$$
R = \frac{C_a}{2U}\left(\tan\beta_2 - \tan\beta_1\right)
$$

**The impulse-reaction spectrum:**

| $R$ | Name | Character |
|---|---|---|
| **0** | **Impulse** | All pressure drop in the NGV. Rotor only turns the flow; $W_1 = W_2$, no relative acceleration. |
| **0.5** | **50% reaction** | Split evenly. Symmetric triangles. |
| **~0.3–0.5** | Typical aero design | |

**Impulse turbines ($R=0$).**
- All expansion in the NGV ⇒ very high $C_1$ ⇒ high work per stage
- No pressure difference across the rotor ⇒ **no tip leakage driving force** ⇒ shrouding less critical
- **But:** high $C_1$ means high losses ($\propto C^2$), and the exit KE is large
- Used in: steam turbine control stages, rocket turbopump turbines (where compactness beats efficiency),
  and historically in some aero HP stages

**50% reaction turbines.**
- Symmetric triangles ($\beta_1 = \alpha_2$, $\beta_2 = \alpha_1$), same blade shapes
- **Highest efficiency** — losses split evenly, neither row pushed hard
- Lower velocities throughout
- **But:** pressure difference across the rotor drives tip leakage ⇒ needs shrouding
- Standard for aero LP turbines

**Modern aero practice:** HP turbines use $R \approx 0.2$–0.4 at the mean (higher work per stage, and
$R$ rises toward the tip anyway); LP turbines use $R \approx 0.5$.

**As with compressors, $R$ varies with radius** ([L17](L17-compressors-4.md)) — designed at the mean, it
falls at the hub. Turbines have large hub-tip variation because the blades are long in the LP stages.

### 6. Stage loading and the Smith chart

**Stage loading coefficient:**

$$
\psi = \frac{\Delta h_0}{U^2} = \frac{c_p\Delta T_0}{U^2} = \frac{\Delta C_w}{U}
$$

**Flow coefficient:**

$$
\phi = \frac{C_a}{U}
$$

Turbine values are much higher than compressors: $\psi \approx 1$–2.5 (vs. 0.3–0.5 for compressors),
$\phi \approx 0.5$–1.0.

**The Smith chart** plots contours of turbine stage efficiency on $\psi$ vs. $\phi$ axes. Its message:

- **Peak efficiency at low $\psi$ and low $\phi$** — lightly loaded stages with low axial velocity are
  the most efficient
- **But low $\psi$ means more stages** for a given total work, so more weight and length
- **The design choice is an efficiency/weight trade**, and it's made differently for different engines:
  - **Civil LP turbines:** low $\psi$ (~1–1.5), more stages, chase efficiency
  - **Military / rocket turbopumps:** high $\psi$ (~2–4), few stages, chase compactness

**This chart is a very likely exam item** — know the axes, the direction of the efficiency gradient, and
the weight trade.

### 7. Useful relations for impulse and 50% reaction

**Impulse stage ($R=0$), axial exit:**

$$
W_1 = W_2, \qquad \beta_1 = \beta_2 \ \text{(magnitudes)}
$$

$$
w = U\,C_{w1} = U(U + W_{w1}) \quad\text{and with axial exit}\quad C_{w1}=2U \ \Rightarrow\ w = 2U^2
$$

giving $\psi = 2$ — the classic impulse loading.

**Optimum blade speed ratio for an impulse stage:**

$$
\frac{U}{C_1}\bigg|_{\text{opt}} = \frac{\cos\alpha_1}{2}
$$

This maximizes **utilization** — the fraction of the NGV's kinetic energy that becomes shaft work.
For $\alpha_1 = 70°$, $U/C_1 = 0.171$.

**50% reaction, axial exit:**

$$
w = U\,C_{w1}, \qquad C_{w1}=U \ \Rightarrow\ w = U^2 \ \Rightarrow\ \psi = 1
$$

**Half the work per stage of an impulse turbine** at the same blade speed — the price of the higher
efficiency.

---

## Worked logic — a single-stage HP turbine

**Given:** $T_{00} = 1600$ K (turbine inlet, from [L04](L04-combustion-thermodynamics-2.md)),
$U = 400$ m/s, $C_a = 250$ m/s (constant), NGV exit angle $\alpha_1 = 68°$, axial rotor exit
($C_{w2}=0$), $c_{p,h}=1150$ J/(kg·K), $\gamma_h=1.33$, $\eta_t = 0.90$.

**Step 1 — NGV exit triangle:**

$$
C_{w1}=C_a\tan\alpha_1 = 250\tan(68°)=250(2.475)=618.8\ \mathrm{m/s}
$$

$$
C_1 = \sqrt{250^2+618.8^2}=667.4\ \mathrm{m/s}
$$

**Note how fast this is** — the NGV has accelerated the flow to 667 m/s. Check the Mach number:

$$
T_1 = T_{00}-\frac{C_1^2}{2c_p}=1600-\frac{667.4^2}{2(1150)}=1600-193.7=1406\ \mathrm{K}
$$

$$
a_1 = \sqrt{1.33(287)(1406)}=732\ \mathrm{m/s} \quad\Longrightarrow\quad M_1 = \frac{667.4}{732}=0.91
$$

**NGVs typically run choked or near-choked** — this one is at $M \approx 0.91$ and would choke at
slightly higher pressure ratio. That choking is exactly what fixes the engine's operating line
([L16](L16-compressors-3.md) §6, [L21](L21-turbines-3.md)).

**Step 2 — rotor inlet relative triangle:**

$$
W_{w1}=C_{w1}-U = 618.8-400=218.8\ \mathrm{m/s}
$$

$$
\beta_1 = \arctan\frac{218.8}{250}=41.2°, \qquad W_1 = \sqrt{250^2+218.8^2}=332.3\ \mathrm{m/s}
$$

**Step 3 — rotor exit (axial absolute exit):**

$$
C_{w2}=0 \quad\Longrightarrow\quad W_{w2}=-U = -400\ \mathrm{m/s}
$$

$$
\beta_2 = \arctan\frac{400}{250}=58.0°, \qquad W_2 = \sqrt{250^2+400^2}=471.7\ \mathrm{m/s}
$$

**Note $W_2 > W_1$ (471.7 vs. 332.3)** — the relative flow **accelerates** through the rotor. This is
the favorable gradient of §4, and it's why no de Haller check is needed. A compressor rotor with this
ratio would be impossible.

**Total turning in the relative frame:**

$$
\beta_1 + \beta_2 = 41.2° + 58.0° = 99.2°
$$

**Nearly 100° of turning in a single blade row** — compare the ~20° of the compressor stage in
[L14](L14-compressors-1.md).

**Step 4 — work and temperature drop:**

$$
w = U\,\Delta C_w = 400(618.8-0)=247{,}520\ \mathrm{J/kg}
$$

$$
\Delta T_0 = \frac{247{,}520}{1150}=215.2\ \mathrm{K}
$$

$$
T_{02}=1600-215.2=1384.8\ \mathrm{K}
$$

**215 K in one stage** — versus ~30 K for a compressor stage. **Seven compressor stages' worth of work
from a single turbine stage.**

**Step 5 — stage loading and reaction:**

$$
\psi = \frac{\Delta C_w}{U}=\frac{618.8}{400}=1.55
$$

$$
R = \frac{C_a}{2U}\left(\tan\beta_2-\tan\beta_1\right)=\frac{250}{800}\left(1.600-0.875\right)=0.3125(0.725)=0.227
$$

**$R \approx 0.23$** — a fairly impulse-like HP stage, typical for a high-work first stage.

**Step 6 — pressure ratio:**

$$
\frac{T_{02s}}{T_{00}}=1-\frac{\Delta T_0}{\eta_t T_{00}}=1-\frac{215.2}{0.90(1600)}=1-0.1494=0.8506
$$

$$
\pi_t = (0.8506)^{\frac{\gamma_h}{\gamma_h-1}}=(0.8506)^{4.03}=0.523
$$

**Expansion ratio ≈ 1.9:1 in one stage.** Compare a compressor stage's 1.3:1 — and remember the
compressor needed 10 stages to reach 20:1.

---

## Worked logic — a 50%-reaction stage via flow and work coefficients

*Cross-referenced from a parallel offering — a different, faster route to the same kind of answer,
using the **flow coefficient $\phi=C_a/U$** and **work coefficient $\psi=\Delta h_0/U^2$**
non-dimensional groups instead of computing $\Delta T_0$ directly first.*

**Given:** $\alpha_2=60°$ (nozzle exit swirl angle), $\beta_2=20°$, $\beta_3=60°$ (rotor exit relative
angle), $U=1{,}050$ ft/s, $T_1=1{,}700°\mathrm F=2{,}160°\mathrm R$, $\gamma=1.33$,
$c_p=0.275$ Btu/(lbm·°R). Since $\alpha_2=\beta_3=60°$, this is (by
[velocity-triangles](../../concepts/velocity-triangles.md)) a **50%-reaction stage**.

**Step 1 — solve the triangle for $C_a$**, using $U = C_{w2}-W_{\theta2}$ with
$C_{w2}=C_a\tan\alpha_2$ and $W_{\theta2}=C_a\tan\beta_2$:

$$
U = C_a\left(\tan\alpha_2-\tan\beta_2\right)
\;\Rightarrow\;
C_a = \frac{U}{\tan60°-\tan20°} = \frac{1{,}050}{1.732-0.364} = 767.5\ \mathrm{ft/s}
$$

**Step 2 — flow and work coefficients:**

$$
\phi = \frac{C_a}{U} = \frac{767.5}{1{,}050} = 0.731
$$

$$
\psi = \frac{\Delta h_0}{U^2} = 2\phi\tan\alpha_2 - 1 = 2(0.731)(1.732)-1 = 1.532
$$

**This $\psi = 2\phi\tan\alpha_2-1$ form is a genuinely useful shortcut**: at 50% reaction, the work
coefficient collapses to a function of $\phi$ and $\alpha_2$ alone — no need to separately track both
velocity triangles once you know the stage is 50% reaction.

**Step 3 — stage work and temperature drop:**

$$
\Delta h_0 = U^2\psi = (1{,}050)^2(1.532) = 1{,}689{,}128\ \mathrm{ft^2/s^2} = 67.5\ \mathrm{Btu/lbm}
$$

$$
\Delta T_0 = \frac{\Delta h_0}{c_p} = \frac{67.5}{0.275} = 245.3°\mathrm R
$$

**Step 4 — isentropic pressure ratio** (best/ideal operating value, since $\eta_t$ isn't given here):

$$
T_3 = T_1-\Delta T_0 = 1{,}914.7°\mathrm R, \qquad
\frac{P_3}{P_1} = \left(\frac{T_3}{T_1}\right)^{\frac{\gamma}{\gamma-1}} = \left(\frac{1{,}914.7}{2{,}160}\right)^{4.03} = 0.615
$$

**Why this route is worth knowing in addition to the direct method above**: $\phi$ and $\psi$ are
exactly the non-dimensional groups that populate a **Smith chart** — the standard industry map of
turbine stage efficiency vs. $(\phi,\psi)$. Solving a triangle problem in these coordinates, rather
than raw velocities, is what lets you immediately look up whether a design point sits in a
high-efficiency region.

**How many turbine stages does the engine need?** The exact turbine-side counterpart of
[L14](L14-compressors-1.md)'s "why 10 compressor stages" calculation, and just as commonly asked:

$$
n_{\text{stages}} = \frac{\Delta T_{0,\text{total}}}{\Delta T_{0,\text{per stage}}}
$$

where $\Delta T_{0,\text{total}} = T_{04}-T_{05}$ comes from the cycle work balance
([L06](L06-thermodynamics-of-jet-engines.md) §7) and $\Delta T_{0,\text{per stage}}=U^2\psi/c_p$ comes
from this page's velocity-triangle work. **Round up** — a fractional answer (e.g. 2.22) means 3 real
stages, each doing slightly less work than the per-stage design point, not "2.22 stages." This is the
quantitative version of the qualitative claim in [L26](L26-course-takeaways.md) that a turbine extracts
the compressor's work in 1–2 stages against the compressor's 10+ — the turbine's much larger $\psi$
(favorable pressure gradient allows far more turning and work per stage,
[L14 §1](L14-compressors-1.md)) is *why* the ratio comes out that lopsided, not an assumption.

---

## Common pitfalls

- **Using the compressor stage order.** Turbine is **stator (NGV) first**, then rotor.
- **Sign errors in $\Delta C_w$.** Compressor: $C_{w2}-C_{w1}$. Turbine: $C_{w1}-C_{w2}$.
- **Applying the de Haller limit to a turbine rotor.** Irrelevant — the relative flow *accelerates*.
- **Using cold $c_p$ and $\gamma$.** Turbine gas is at 1,400–1,700 K: $c_p \approx 1150$,
  $\gamma \approx 1.33$.
- **Assuming $R = 0.5$ is always best for turbines.** HP stages commonly run 0.2–0.4.
- **Forgetting the NGV does no work.** $T_0$ constant across it.
- **Thinking turbines need fewer stages "because the gas is hot."** It's the pressure gradient.
- **Neglecting to check NGV Mach number.** It's usually choked, which matters for matching.
- **Forgetting $R$ varies with radius.**

---

## Exam checklist

- [ ] Draw a turbine stage with NGV and rotor in the correct order; label the triangles
- [ ] Write Euler's equation with the correct turbine sign convention
- [ ] **Explain why turbines need far fewer stages than compressors** (favorable gradient / boundary layer)
- [ ] Define turbine degree of reaction and write the working form
- [ ] **Compare impulse ($R=0$) and 50% reaction on work, losses, and tip leakage**
- [ ] State the optimum blade speed ratio for an impulse stage
- [ ] Define $\psi$ and $\phi$ for a turbine, give typical values, and contrast with compressors
- [ ] **Describe the Smith chart and the efficiency/weight trade it encodes**
- [ ] Compute a full turbine stage: triangles, work, $\Delta T_0$, $\psi$, $R$, $\pi_t$
- [ ] Check NGV exit Mach number and explain why choking matters

---

## Links

- Previous: [L18 — Transonic Fan Stage](L18-transonic-fan-stage.md)
- Next: [L20 — Turbines 2](L20-turbines-2.md) — efficiency, losses, cooling
- Compressor counterpart: [L14 — Compressors 1](L14-compressors-1.md)
- Where TIT comes from: [L04 — Combustion Thermodynamics 2](L04-combustion-thermodynamics-2.md)
- Concept: [velocity-triangles](../../concepts/velocity-triangles.md)
- Course hub: [EAS4300](../EAS4300.md)
