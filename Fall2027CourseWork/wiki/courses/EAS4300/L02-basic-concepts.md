# L02 — Basic Concepts

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 2 · **Dates:** Mon 24 Aug, Wed 26 Aug 2026
**Book §:** 2.1 *Introduction* · 2.2 *Fundamental Equations* (24 Aug) · 2.3 *Thermodynamics of Gases* (26 Aug) — ✅ verified
**Tags:** #control-volume #conservation-laws #continuity #momentum #energy #entropy #perfect-gas #reynolds-transport

---

## Why this lecture matters

This is the **toolbox lecture**. Every component analysis in the rest of the course — inlet,
combustor, compressor, turbine, nozzle — is the same four equations applied between two stations with
different things assumed negligible. If the control-volume method is solid here, the remaining 24
lectures are bookkeeping. If it isn't, everything after Lecture 6 will feel like memorization.

---

## Core concepts

### 1. The control volume is the whole method

You almost never track a fluid particle in propulsion. You draw a box (the **control volume**, CV),
label where flow crosses the boundary (**stations**), and write balances of mass, momentum, energy,
and entropy across it.

**Reynolds transport theorem** is the formal bridge from "system" (fixed mass) to "control volume"
(fixed region):

$$
\frac{dB_{\text{sys}}}{dt}
= \frac{\partial}{\partial t}\int_{CV} \beta \rho \, d\mathcal{V}
+ \int_{CS} \beta \rho\,(\mathbf{V}\cdot \mathbf{n})\, dA
$$

where $B$ is any extensive property and $\beta = B/m$ its intensive counterpart. Read it as:
*rate of change for the fluid = rate of change stored inside the box + net rate carried out through
the walls.*

**Steady flow kills the first term.** Almost everything in this course is steady, one-dimensional, and
has a finite number of discrete inlets/outlets, which collapses the surface integral into a sum. That
reduction is what makes the equations below tractable.

### 2. The four conservation statements

Assume **steady**, **one-dimensional** flow with uniform properties at each port.

**Mass (continuity).** What goes in comes out.

**Momentum.** The net force on the CV equals the net momentum flux out. This is a *vector* equation —
the one place in the course where sign convention causes the most grief. Forces include pressure
acting on every part of the CV surface plus any reaction force from solid structure.

**Energy (Steady Flow Energy Equation, SFEE).** Heat added plus shaft work in equals the change in
total enthalpy of the stream. **Total (stagnation) enthalpy is the natural variable** because it
already bundles internal energy, flow work, and kinetic energy.

**Entropy (2nd law).** Sets the *direction* and quantifies irreversibility. It's what turns "ideal
cycle" into "real cycle" via component efficiencies.

### 3. Stagnation (total) properties — the key simplification

Define the **stagnation state** as the state a flow would reach if brought to rest **adiabatically**
(and, for stagnation *pressure*, **isentropically**).

Why this matters so much: in an adiabatic duct with no shaft work, **stagnation enthalpy is
constant** even if velocity, static pressure, and static temperature all change wildly. So the messy
kinetic-energy bookkeeping becomes a single conserved quantity.

The crisp mental model:
- **Stagnation temperature $T_0$ tracks energy.** It changes only with heat addition or shaft work.
- **Stagnation pressure $p_0$ tracks quality/losses.** It changes with those *and* drops with any
  irreversibility — friction, shocks, mixing, combustion pressure loss.

So across an ideal, adiabatic, work-free component: $T_0$ constant, $p_0$ constant.
Across a *real* one: $T_0$ constant, $p_0$ **drops**. That single sentence is how you'll characterize
inlets, combustors, and nozzles for the rest of the semester. Full treatment:
[stagnation-properties](../../concepts/stagnation-properties.md).

### 4. Perfect and calorically perfect gases (§2.3)

Two distinct idealizations that get conflated:

- **Thermally perfect (ideal) gas:** $p = \rho R T$. Internal energy and enthalpy are functions of
  temperature alone: $u=u(T)$, $h=h(T)$.
- **Calorically perfect gas:** additionally, $c_p$ and $c_v$ are **constants**, so $h = c_p T$ and
  $u = c_v T$.

Nearly all closed-form results in this course assume **calorically perfect**. That's a decent
assumption for air at inlet/compressor temperatures and a **poor** one across a combustor, where $T$
may triple and $c_p$ rises appreciably. The standard engineering dodge — used in this course and in
industry — is to use **two different constant values**: "cold" properties upstream of the burner and
"hot" properties downstream.

$$
\text{Cold section: } \gamma \approx 1.4,\ c_p \approx 1005\ \mathrm{J/(kg\cdot K)}
$$

$$
\text{Hot section: } \gamma \approx 1.33,\ c_p \approx 1150\ \mathrm{J/(kg\cdot K)}
$$

Using $\gamma = 1.4$ through the turbine is a classic and expensive exam mistake.

### 5. Reversibility, irreversibility, and where losses live

Real losses in a gas turbine come from a short list:
**viscous friction** in boundary layers · **shock waves** · **mixing** of streams at different
velocities/temperatures · **heat transfer across finite temperature differences** ·
**combustion** itself (chemical irreversibility) · **leakage** past tip clearances.

Each shows up in the analysis as a **stagnation pressure loss** or as a **component efficiency < 1**.
Recognizing which mechanism dominates in which component is a recurring exam question:
inlets → friction and shocks; combustors → mixing, friction, and heat release at finite $\Delta T$;
turbomachinery → friction, tip leakage, and shocks in transonic stages.

---

## Key equations

### Continuity

$$
\dot{m} = \rho A V = \text{constant along a stream tube}
$$

Multi-port steady form:

$$
\sum_{\text{in}} \dot{m}_i = \sum_{\text{out}} \dot{m}_e
$$

Differential (logarithmic) form — extremely useful in [L05](L05-gas-dynamics.md):

$$
\frac{d\rho}{\rho} + \frac{dA}{A} + \frac{dV}{V} = 0
$$

### Momentum (steady, 1-D, x-direction)

$$
\sum F_x = \sum_{\text{out}} \dot{m}_e u_e - \sum_{\text{in}} \dot{m}_i u_i
$$

Expanded with pressure forces on the control surface:

$$
\sum F_{x,\text{surface}} + \sum_{\text{in}} (p_i A_i) - \sum_{\text{out}} (p_e A_e)
= \sum_{\text{out}} \dot{m}_e u_e - \sum_{\text{in}} \dot{m}_i u_i
$$

**Impulse function** — the combination that appears constantly, because it bundles pressure force and
momentum flux into one quantity:

$$
\mathcal{I} = pA + \dot{m}u = pA\left(1 + \gamma M^2\right)
$$

Thrust problems become "compute $\mathcal I$ at each station and difference them."

### Energy — Steady Flow Energy Equation

$$
\dot{Q} - \dot{W}_s = \sum_{\text{out}} \dot{m}\left(h + \tfrac{V^2}{2} + gz\right)
- \sum_{\text{in}} \dot{m}\left(h + \tfrac{V^2}{2} + gz\right)
$$

Drop $gz$ (always negligible for gases here) and write in stagnation enthalpy:

$$
h_0 \equiv h + \frac{V^2}{2}
$$

$$
\dot{Q} - \dot{W}_s = \dot{m}\,(h_{0,e} - h_{0,i})
$$

Calorically perfect gas, single stream:

$$
\dot{Q} - \dot{W}_s = \dot{m}\,c_p\,(T_{0,e} - T_{0,i})
$$

**Adiabatic, no shaft work ⇒ $T_{0}$ = constant.** Nozzles, inlets, and diffusers all live here.

### Stagnation relations (calorically perfect gas)

$$
T_0 = T\left(1 + \frac{\gamma-1}{2}M^2\right)
$$

$$
\frac{p_0}{p} = \left(1 + \frac{\gamma-1}{2}M^2\right)^{\frac{\gamma}{\gamma-1}}
$$

$$
\frac{\rho_0}{\rho} = \left(1 + \frac{\gamma-1}{2}M^2\right)^{\frac{1}{\gamma-1}}
$$

Speed of sound and Mach number:

$$
a = \sqrt{\gamma R T}, \qquad M = \frac{V}{a}
$$

### Entropy

$$
\dot{S}_{gen} = \sum_{\text{out}} \dot{m}s - \sum_{\text{in}} \dot{m}s - \int \frac{\delta \dot{Q}}{T} \;\ge\; 0
$$

Change between two states, calorically perfect gas:

$$
s_2 - s_1 = c_p \ln\frac{T_2}{T_1} - R \ln\frac{p_2}{p_1}
$$

The same relation **in stagnation variables** (this is the workhorse):

$$
s_2 - s_1 = c_p \ln\frac{T_{02}}{T_{01}} - R \ln\frac{p_{02}}{p_{01}}
$$

**Adiabatic and work-free ⇒ $T_{02}=T_{01}$ ⇒**

$$
s_2 - s_1 = -R \ln\frac{p_{02}}{p_{01}} \;\ge\; 0
\quad\Longrightarrow\quad
p_{02} \le p_{01}
$$

That is the formal proof of the claim in §3: **stagnation pressure can only fall** across an adiabatic,
work-free component. Loss = $p_0$ loss. Memorize this derivation; it's a favorite short-answer item.

### Gas property relations

$$
c_p - c_v = R, \qquad \gamma = \frac{c_p}{c_v}
$$

$$
c_p = \frac{\gamma R}{\gamma - 1}, \qquad c_v = \frac{R}{\gamma-1}
$$

$$
R_{\text{air}} = 287\ \mathrm{J/(kg\cdot K)}
$$

Isentropic relations for a calorically perfect gas:

$$
\frac{p_2}{p_1} = \left(\frac{T_2}{T_1}\right)^{\frac{\gamma}{\gamma-1}}
= \left(\frac{\rho_2}{\rho_1}\right)^{\gamma}
$$

---

## Worked logic — deriving the thrust equation from the momentum balance

This derivation appears on exams and is the payoff of the lecture.

Draw a CV enclosing the engine, with the upstream face far ahead in undisturbed air at $p_a$, the
downstream face at the nozzle exit plane, and the side faces far enough out that the flow there is at
ambient pressure $p_a$.

Momentum balance in the flight direction, with $F$ the reaction force from the strut holding the
engine:

$$
F + p_a A_{\text{in}} - p_e A_e - p_a\left(A_{\text{in}} - A_e\right)
= \dot{m}_e u_e - \dot{m}_a u_a
$$

The ambient-pressure terms on the side and inlet faces collapse:

$$
F - (p_e - p_a)A_e = \dot{m}_e u_e - \dot{m}_a u_a
$$

$$
\boxed{\,F = \dot{m}_e u_e - \dot{m}_a u_a + (p_e - p_a)A_e\,}
$$

Two things to notice:
1. **$p_a$ cancels everywhere except at the exit plane.** The pressure-thrust term exists purely
   because the nozzle exit may not be at ambient pressure.
2. **$\dot m_a u_a$ is "ram drag."** It is not a loss mechanism — it's the momentum you had to pick up
   and re-throw. It is why thrust falls as flight speed rises.

---

## Common pitfalls

- **Sign errors in the momentum equation.** Fix a positive direction *once*, on the sketch, before
  writing anything. Outflow momentum is positive, inflow negative, forces follow the sketch.
- **Using static properties where stagnation belongs.** In any duct with velocity, $T \ne T_0$. Both
  appear in the same problem; label them.
- **Assuming $p_0$ is constant because the flow is adiabatic.** Adiabatic gives you *$T_0$* constant.
  $p_0$ is constant only if it's *also* reversible (isentropic).
- **Using $\gamma = 1.4$ downstream of the combustor.** Use hot-section properties.
- **Forgetting $\dot m_f$ in the exhaust flow** when the problem gives a fuel-air ratio and expects
  $\dot m_e = \dot m_a(1+f)$.
- **Treating the CV boundary as if pressure only acts at inlet and exit.** It acts everywhere; the
  standard choice of far-field boundaries is precisely what makes the other contributions cancel.

---

## Exam checklist

- [ ] Write continuity, momentum, energy, and entropy for a steady 1-D CV from memory
- [ ] Define stagnation enthalpy, temperature, and pressure, including the *isentropic* qualifier on $p_0$
- [ ] State what conserves $T_0$ and what conserves $p_0$, and give a physical example of each
- [ ] Prove $p_{02} \le p_{01}$ for an adiabatic, work-free process
- [ ] Distinguish thermally perfect from calorically perfect; know cold vs. hot $\gamma$, $c_p$
- [ ] Derive the thrust equation from a control-volume momentum balance
- [ ] Write the impulse function and use it for a thrust or force-on-duct problem
- [ ] Convert between static and stagnation states given $M$

---

## Links

- Previous: [L01 — Introduction](L01-introduction.md)
- Next: [L03 — Combustion Thermodynamics 1](L03-combustion-thermodynamics-1.md)
- Applied to compressible flow: [L05 — Gas Dynamics](L05-gas-dynamics.md)
- Concept: [stagnation-properties](../../concepts/stagnation-properties.md)
- Concept: [station-numbering](../../concepts/station-numbering.md)
- Course hub: [EAS4300](../EAS4300.md)
