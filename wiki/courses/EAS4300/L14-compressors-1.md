# L14 — Axial Compressors 1: Velocity Triangles and Euler Work

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 14 · **Date:** Wed 14 Oct 2026
**Book §:** 7.1 *Introduction* (p. 275) · 7.2 *Angular Momentum* (p. 277) · 7.3 *Work and Compression* (p. 282) — ✅ verified
**Tags:** #compressor #axial #velocity-triangles #euler-equation #rothalpy #stage #rotor #stator #work-input #flow-coefficient #blade-speed

---

## Why this lecture matters

This is the **most important single lecture in the turbomachinery half of the course**. Velocity
triangles and Euler's equation are the language of compressors ([L14](L14-compressors-1.md)–[L18](L18-transonic-fan-stage.md)),
turbines ([L19](L19-turbines-1.md)–[L21](L21-turbines-3.md)), and centrifugal machines
([L22](L22-centrifugal-compressors.md)) alike. Learn it once, cleanly, and eight lectures become one
idea applied repeatedly.

---

## Core concepts

### 1. What a compressor stage is

```
[ Rotor ] → [ Stator ]
   ↑            ↑
adds energy   converts
(work in)    KE → pressure
```

**Rotor.** Moving blades. **The only place work enters the flow.** It raises both total pressure and
total temperature, and adds swirl (tangential velocity).

**Stator.** Stationary blades. **Adds no work** — $T_0$ is constant across it. It diffuses the flow
(converting kinetic energy to static pressure) and removes the swirl the rotor added, setting the flow
up for the next rotor.

**A "stage" = one rotor + one stator.** Both are diffusing passages (adverse pressure gradient), which
is why compressors are fundamentally harder than turbines — see §7.

**IGV (Inlet Guide Vanes)** may precede the first rotor to pre-swirl the flow.
**OGV (Outlet Guide Vanes)** at the exit remove residual swirl before the combustor.

### 2. The two frames of reference — the heart of the method

Turbomachinery is confusing until you internalize that there are **two observers**:

- **Absolute frame** (stationary, lab/casing frame): velocity $\mathbf{C}$ (some texts use $\mathbf V$)
- **Relative frame** (rotating with the rotor): velocity $\mathbf{W}$

They differ by the **blade speed** $\mathbf{U}$:

$$
\mathbf{C} = \mathbf{W} + \mathbf{U}
$$

$$
U = \omega r = \frac{2\pi N r}{60} \quad (N \text{ in rpm})
$$

**Rules that follow, and that you must apply automatically:**
- **Stators** are stationary ⇒ analyze in the **absolute** frame
- **Rotors** move ⇒ analyze in the **relative** frame
- $U$ is purely **tangential**
- The **axial** component is the same in both frames: $C_a = W_a$

**The single most common error in this entire course** is applying a relation in the wrong frame. Draw
the triangle, label $C$, $W$, $U$ explicitly, and note which frame each equation belongs to.

### 3. Velocity triangle notation

Standard axial-compressor convention (fixed here and used throughout the wiki):

| Symbol | Meaning |
|---|---|
| $C$ | Absolute velocity |
| $W$ | Relative velocity |
| $U$ | Blade speed, $\omega r$ |
| $C_a$ | Axial component ($=W_a$) |
| $C_w$ or $C_\theta$ | Absolute tangential (whirl/swirl) component |
| $W_w$ or $W_\theta$ | Relative tangential component |
| $\alpha$ | Absolute flow angle, from axial |
| $\beta$ | Relative flow angle, from axial |
| Subscript 1 | Rotor inlet |
| Subscript 2 | Rotor exit = stator inlet |
| Subscript 3 | Stator exit |

Geometric relations:

$$
C_w = C_a\tan\alpha, \qquad W_w = C_a\tan\beta
$$

$$
U = C_w + W_w = C_a\left(\tan\alpha + \tan\beta\right)
$$

$$
C^2 = C_a^2 + C_w^2, \qquad W^2 = C_a^2 + W_w^2
$$

**What happens across a compressor stage:**
- **Rotor (1→2):** in the relative frame the flow **diffuses** ($W_2 < W_1$), turning toward axial.
  In the absolute frame it **accelerates** and gains swirl ($C_2 > C_1$, $C_{w2} > C_{w1}$).
- **Stator (2→3):** in the absolute frame the flow **diffuses** ($C_3 < C_2$), removing swirl,
  typically returning to $C_3 \approx C_1$ so stages can be repeated.

**A repeating stage** has $C_3 = C_1$ and $\alpha_3 = \alpha_1$ — a common and convenient design
assumption that makes multistage analysis tractable.

### 4. Euler's turbomachinery equation

**The central result of turbomachinery.** Apply angular momentum conservation to a control volume around
the rotor. Torque equals rate of change of angular momentum:

$$
\tau = \dot m \left(r_2 C_{w2} - r_1 C_{w1}\right)
$$

Power = torque × angular velocity:

$$
\dot W = \tau\omega = \dot m\left(\omega r_2 C_{w2} - \omega r_1 C_{w1}\right)
$$

$$
\boxed{\ w = \frac{\dot W}{\dot m} = U_2 C_{w2} - U_1 C_{w1}\ }
$$

For an **axial** machine with constant mean radius, $U_1=U_2=U$:

$$
w = U\left(C_{w2}-C_{w1}\right) = U\,\Delta C_w
$$

Combined with the SFEE ([L02](L02-basic-concepts.md)):

$$
w = c_p\left(T_{02}-T_{01}\right) = c_p\,\Delta T_0
$$

$$
\boxed{\ \Delta T_0 = \frac{U \Delta C_w}{c_p}\ }
$$

**This is the equation to know cold.** Three observations:

1. **Work depends only on the change in swirl.** Not on pressure, not on losses, not on efficiency.
   Euler's equation is **exact** for the work input — it holds for real and ideal machines alike.
   Losses determine how much *pressure rise* you get from that work, not the work itself.
2. **Work scales with $U$** — so blade speed is the dominant design lever. Doubling $U$ doubles work at
   the same $\Delta C_w$. This is why compressor design is a fight against mechanical and aerodynamic
   limits on tip speed.
3. **In a compressor $\Delta C_w > 0$** (work in). In a turbine $\Delta C_w < 0$ (work out) — same
   equation, sign flipped ([L19](L19-turbines-1.md)).

**Alternative form** (from the triangle geometry, useful for interpreting the physics):

$$
w = \frac{C_2^2-C_1^2}{2} + \frac{U_2^2-U_1^2}{2} + \frac{W_1^2-W_2^2}{2}
$$

Three terms: absolute KE change + centrifugal (radial) effect + relative diffusion. For an axial machine
the middle term vanishes; for a **centrifugal** compressor it's the dominant one, which is exactly why
centrifugal machines achieve much higher pressure ratio per stage
([L22](L22-centrifugal-compressors.md)).

### 5. Rothalpy — the rotating-frame conserved quantity

In the rotating frame, $h_0$ is *not* conserved (the blade does work). The quantity that is conserved
across a rotor is **rothalpy**:

$$
I = h + \frac{W^2}{2} - \frac{U^2}{2} = h_{0,\text{rel}} - \frac{U^2}{2}
$$

$$
I_1 = I_2 \qquad \text{(adiabatic rotor)}
$$

For an **axial** rotor ($U_1=U_2$) this simplifies to: **relative stagnation enthalpy is conserved.**

$$
h_{01,\text{rel}} = h_{02,\text{rel}} \quad\Longrightarrow\quad T_{01,\text{rel}}=T_{02,\text{rel}}
$$

**Why it matters:** rothalpy is to the rotating frame what $h_0$ is to the stationary frame. It's the
tool that lets you do energy accounting inside a rotor, and it's what makes relative-frame Mach numbers
and pressure ratios computable ([L18](L18-transonic-fan-stage.md)).

### 6. The dimensionless stage parameters

Three numbers characterize any stage design and appear on every design chart:

**Flow coefficient** — how axial the flow is:

$$
\phi = \frac{C_a}{U}
$$

Typical 0.4–0.7. Low $\phi$ ⇒ more turning, more work, but higher stall risk.

**Stage loading (work) coefficient:**

$$
\psi = \frac{c_p\Delta T_0}{U^2}=\frac{\Delta C_w}{U}
$$

*(Some texts define $\psi = \Delta h_0/(\tfrac12 U^2)$, giving values twice these — check your
instructor's convention.)* Typical 0.3–0.5 for axial compressors. Higher loading means fewer stages but
more diffusion per stage and less stall margin.

**Degree of reaction** — how the static pressure rise is split between rotor and stator:

$$
R = \frac{\text{static enthalpy rise in rotor}}{\text{static enthalpy rise in stage}}
= \frac{h_2-h_1}{h_3-h_1}
$$

Covered fully in [L15](L15-compressors-2.md). For 50% reaction:

$$
R = 1 - \frac{C_{w1}+C_{w2}}{2U}
$$

### 7. Why compressors are harder than turbines

**The single most important qualitative fact about compressors**, and a recurring exam question.

| | **Compressor** | **Turbine** |
|---|---|---|
| Pressure gradient | **Adverse** (rising $p$) | **Favorable** (falling $p$) |
| Boundary layer | Wants to separate | Stays attached |
| Turning per blade row | Limited (~20–45°) | Large (~70–120°) |
| Stages for a given ratio | **Many** (10–15) | **Few** (1–2) |
| Failure mode | **Stall / surge** | Thermal/creep |

**A modern engine might have 15 compressor stages driven by 2 turbine stages** — the turbine extracts in
two rows what the compressor needed fifteen rows to put in. That asymmetry is entirely due to the
pressure gradient.

**De Haller number** — the classical diffusion limit:

$$
\mathrm{DH} = \frac{W_2}{W_1} \ge 0.72
$$

Diffusing the relative velocity by more than ~28% in one row separates the boundary layer. **This is the
hard constraint that caps work per stage** and forces multistage designs.

**Diffusion factor** (a more refined criterion accounting for blade loading):

$$
D = 1 - \frac{W_2}{W_1} + \frac{\Delta W_w}{2\sigma W_1} \le 0.6
$$

where $\sigma = c/s$ is **solidity** (chord/spacing). Higher solidity spreads the loading over more
blade surface, permitting more turning — which is why heavily-loaded stages have more, closer blades.

---

## Worked logic — designing one compressor stage

**Given:** $U = 300$ m/s (mean radius), $C_a = 150$ m/s (constant through the stage), axial inlet
($\alpha_1 = 0$, so $C_{w1}=0$), rotor exit relative angle $\beta_2 = 30°$,
$c_p = 1005$ J/(kg·K), $T_{01}=288$ K, $p_{01}=101.3$ kPa, $\eta_{\text{stage}}=0.88$, $\gamma=1.4$.

**Step 1 — inlet triangle.** Axial inlet:

$$
C_1 = C_a = 150\ \mathrm{m/s}, \qquad C_{w1}=0
$$

$$
W_{w1} = U - C_{w1} = 300\ \mathrm{m/s}
$$

$$
\tan\beta_1 = \frac{W_{w1}}{C_a}=\frac{300}{150}=2.0 \quad\Longrightarrow\quad \beta_1 = 63.4°
$$

$$
W_1 = \sqrt{150^2+300^2}=335.4\ \mathrm{m/s}
$$

**Step 2 — exit triangle:**

$$
W_{w2}=C_a\tan\beta_2 = 150\tan(30°)=86.6\ \mathrm{m/s}
$$

$$
C_{w2}=U - W_{w2}=300-86.6=213.4\ \mathrm{m/s}
$$

$$
W_2 = \sqrt{150^2+86.6^2}=173.2\ \mathrm{m/s}
$$

$$
C_2 = \sqrt{150^2+213.4^2}=260.8\ \mathrm{m/s}, \qquad \alpha_2 = \arctan\frac{213.4}{150}=54.9°
$$

**Step 3 — check the de Haller limit** (do this *before* trusting the design):

$$
\mathrm{DH}=\frac{W_2}{W_1}=\frac{173.2}{335.4}=0.516 \quad \color{red}{< 0.72\ \text{✗}}
$$

**This stage is far too aggressive** — the rotor boundary layer would separate. The design must be
relaxed: either reduce the turning (increase $\beta_2$), raise $C_a$, or reduce $U$.

**Redesign with $\beta_2 = 45°$:**

$$
W_{w2}=150\tan(45°)=150\ \mathrm{m/s}, \qquad C_{w2}=300-150=150\ \mathrm{m/s}
$$

$$
W_2 = \sqrt{150^2+150^2}=212.1\ \mathrm{m/s}
\quad\Longrightarrow\quad
\mathrm{DH}=\frac{212.1}{335.4}=0.632
$$

Still below 0.72. Try $\beta_2 = 52°$:

$$
W_{w2}=150\tan(52°)=192.0, \quad W_2=\sqrt{150^2+192^2}=243.6
\quad\Longrightarrow\quad \mathrm{DH}=0.726\ \checkmark
$$

**Step 4 — work and temperature rise** with the acceptable design ($C_{w2}=300-192=108$ m/s):

$$
\Delta T_0 = \frac{U\Delta C_w}{c_p}=\frac{300(108-0)}{1005}=32.2\ \mathrm{K}
$$

**Step 5 — pressure ratio:**

$$
\pi_{\text{stage}}=\left[1+\frac{\eta_{\text{stage}}\Delta T_0}{T_{01}}\right]^{\frac{\gamma}{\gamma-1}}
=\left[1+\frac{0.88\times32.2}{288}\right]^{3.5}
$$

$$
=\left(1.0984\right)^{3.5}=1.379
$$

**Step 6 — the design lesson.** One realistic stage gives $\pi \approx 1.38$. To reach an overall
$\pi_c = 20$:

$$
n = \frac{\ln 20}{\ln 1.379} = \frac{2.996}{0.3213}\approx 9.3 \quad\Longrightarrow\quad \textbf{10 stages}
$$

**That's the answer to "why do compressors have so many stages?"** — the de Haller limit caps each
stage at ~1.3–1.4 pressure ratio, and you need 10+ to reach modern OPR. Compare a turbine, which
extracts all that work in 2 stages.

**Further practice — the reverse direction** (cross-referenced from a parallel offering): given
$W_1=240$ m/s, $C_1=140$ m/s, $\beta_2=30°$, $W_2=140$ m/s, $T_1=300$ K, $\eta_{\text{stage}}=0.85$,
find the stage pressure ratio. This problem hands you the **relative** velocities and asks you to
back out $U$ and $C_{w2}$ — the reverse of the given-$U$-and-$C_a$ approach above. Method: get
$C_a = W_2\sin\beta_2$ from the exit triangle, then $U-C_{w2}=C_a/\tan\beta_2$, then use
$C_{w2}=\sqrt{C_2^2-C_a^2}$ (from the known $C_2$) to solve the two equations for $U$ and $C_{w2}$
simultaneously, then proceed exactly as in Step 4 above ($\Delta T_0 = U\Delta C_w/c_p$, then stage
efficiency, then $\pi_{\text{stage}}$). **The lesson**: velocity-triangle problems come in "solve
forward from $U,C_a$" and "solve backward from measured/relative velocities" flavors — recognize
which one you're given before picking a solution path.

---

## Common pitfalls

- **Mixing absolute and relative frames.** Draw and label the triangle first, every time.
- **Sign errors in $\Delta C_w$.** Compressor: positive (work in). Turbine: negative.
- **Thinking Euler's equation requires isentropic flow.** It does **not** — it's exact for work input.
  Efficiency affects the *pressure* you get, not the work.
- **Forgetting $C_a$ is common to both frames.**
- **Skipping the de Haller check.** A triangle can be geometrically fine and aerodynamically impossible.
- **Assuming $U$ is the same at hub and tip.** $U = \omega r$ varies strongly with radius —
  see [L17](L17-compressors-4.md).
- **Using $\psi$ conventions inconsistently.** Factor-of-2 differences between textbooks.
- **Forgetting the stator adds no work.** $T_0$ is constant across a stator; only $p_0$ drops (loss).

---

## Exam checklist

- [ ] Draw a compressor stage velocity triangle with $C$, $W$, $U$, $\alpha$, $\beta$ correctly labeled
- [ ] State which frame applies to rotor and to stator
- [ ] **Derive Euler's equation from angular momentum conservation**
- [ ] Write $\Delta T_0 = U\Delta C_w/c_p$ and explain why it's independent of efficiency
- [ ] Write the alternative three-term form and identify the centrifugal term
- [ ] Define rothalpy and state what it conserves across a rotor
- [ ] Define $\phi$, $\psi$, $R$ and give typical values
- [ ] **Explain why compressors need many more stages than turbines** (pressure gradient argument)
- [ ] State the de Haller criterion and use it to check a design
- [ ] Compute stage $\Delta T_0$, $\pi_{stage}$, and the number of stages for a target $\pi_c$

---

## Links

- Previous: [L13 — Nozzles](L13-nozzles.md)
- Next: [L15 — Compressors 2](L15-compressors-2.md) — reaction, efficiency, losses
- Same math, turbines: [L19 — Turbines 1](L19-turbines-1.md)
- Concept: [velocity-triangles](../../concepts/velocity-triangles.md)
- Course hub: [EAS4300](../EAS4300.md)
