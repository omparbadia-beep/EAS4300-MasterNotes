# L23 — Rocket Engines 1: Thrust, Specific Impulse, and the Rocket Equation

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 23 · **Date:** Fri 13 Nov 2026
**Book §:** Ch. 10 *Performance of Rocket Vehicles* (p. 469) — ✅ verified
*(10.1 Intro · 10.2 Static Performance · 10.3 Vehicle Acceleration · 10.4 Chemical Rockets · 10.5 Electrical Rocket Vehicles · 10.6 Space Missions)*
**Tags:** #rocket #specific-impulse #characteristic-velocity #thrust-coefficient #tsiolkovsky #rocket-equation #staging #delta-v #chamber #sounding-rocket #structural-efficiency

*(Wed 11 Nov — Veterans Day holiday, no class. First lecture after Midterm 2.)*

---

## Why this lecture matters

The course's catalog description promises "air-breathing **and rocket** engines." Everything from
[L06](L06-thermodynamics-of-jet-engines.md) onward assumed an atmosphere to breathe. Rockets discard
that assumption, and the consequences — no ram drag, no altitude lapse, and a brutal exponential
penalty on mass — reshape the whole analysis.

---

## Core concepts

### 1. The rocket thrust equation

From [L01](L01-introduction.md), with **no incoming momentum** because the propellant starts at rest
relative to the vehicle:

$$
F = \dot m_p u_e + \left(p_e - p_a\right)A_e
$$

**Effective exhaust velocity** bundles the pressure term into an equivalent velocity — the quantity you
actually use:

$$
c = u_e + \frac{(p_e-p_a)A_e}{\dot m_p}
\qquad\Longrightarrow\qquad
F = \dot m_p\, c
$$

**Consequences that distinguish rockets from air-breathers:**

- **Thrust is independent of flight velocity.** No ram drag term. A rocket at Mach 20 produces the same
  thrust as at Mach 0.
- **Thrust *increases* with altitude.** As $p_a \to 0$, the pressure term grows. Typically 10–30% more
  thrust in vacuum than at sea level.
- **Propulsive efficiency** ([L06](L06-thermodynamics-of-jet-engines.md)) is terrible at low speed and
  actually **peaks at $u_a = u_e$** — a rocket becomes propulsively efficient only once it's flying as
  fast as its own exhaust.

### 2. Specific impulse

$$
I_{sp}=\frac{F}{\dot m_p\, g_0}=\frac{c}{g_0} \qquad [\mathrm{s}]
$$

**Why seconds?** The units are a historical artifact of dividing by weight flow rather than mass flow —
it makes $I_{sp}$ numerically identical in SI and imperial units, which is why it survived. The
physically meaningful quantity is $c$ (m/s).

**Benchmarks:**

| System | $I_{sp}$ (vac) | $c$ (m/s) |
|---|---|---|
| Solid propellant | 250–280 | 2,450–2,750 |
| Kerosene/LOX (RP-1) | 330–360 | 3,240–3,530 |
| Hydrazine monoprop | 220–230 | 2,160–2,260 |
| **LH₂/LOX** | **440–465** | **4,320–4,560** |
| Nuclear thermal | 800–900 | 7,850–8,830 |
| Hall thruster | 1,500–3,000 | 14,700–29,400 |
| Ion thruster | 3,000–10,000 | 29,400–98,100 |

**Why LH₂/LOX wins among chemicals** — the key physical insight:

$$
c \propto \sqrt{\frac{T_c}{\mathcal{M}}}
$$

Exhaust velocity depends on **chamber temperature over molecular mass**. LH₂/LOX doesn't burn
especially hot (~3,300 K, cooler than kerosene/LOX at the same mixture ratio), but its exhaust is mostly
**H₂O and excess H₂** with very low $\mathcal M$. **Low molecular mass beats high temperature.**

This is also why hydrogen-rich mixture ratios are used deliberately: running LH₂/LOX at an O/F of ~6
rather than the stoichiometric ~8 *lowers* the temperature but *lowers $\mathcal M$ more*, netting
higher $I_{sp}$. **Optimum mixture ratio is fuel-rich, not stoichiometric** — a favorite exam point,
and a different reason from the "slightly rich peak flame temperature" of
[L03](L03-combustion-thermodynamics-1.md).

### 3. Characteristic velocity $c^*$ and thrust coefficient $C_F$

**The most useful decomposition in rocketry:** separate the *combustion chamber's* performance from the
*nozzle's*.

**Characteristic velocity — measures the chamber (propellant + combustion quality):**

$$
c^* = \frac{p_c A_t}{\dot m_p}
$$

From the choked mass flow relation ([L05](L05-gas-dynamics.md) §4):

$$
c^* = \frac{\sqrt{\gamma R T_c}}{\gamma\sqrt{\left(\frac{2}{\gamma+1}\right)^{\frac{\gamma+1}{\gamma-1}}}}
= \frac{1}{\Gamma}\sqrt{\frac{R_u T_c}{\mathcal M}}
$$

$$
\Gamma = \sqrt{\gamma}\left(\frac{2}{\gamma+1}\right)^{\frac{\gamma+1}{2(\gamma-1)}}
$$

**$c^*$ depends only on $T_c$, $\mathcal M$, $\gamma$** — i.e. on the propellant and how well it burns.
**It is independent of nozzle geometry.** Measured $c^*$ divided by theoretical $c^*$ is the
**$c^*$ efficiency**, the standard metric for injector and chamber quality (typically 0.95–0.99).

**Thrust coefficient — measures the nozzle:**

$$
C_F = \frac{F}{p_c A_t}
$$

$$
C_F = \Gamma\sqrt{\frac{2\gamma}{\gamma-1}\left[1-\left(\frac{p_e}{p_c}\right)^{\frac{\gamma-1}{\gamma}}\right]}
+ \frac{(p_e-p_a)A_e}{p_c A_t}
$$

**The clean decomposition:**

$$
\boxed{\ F = \dot m_p c = c^*\, C_F\, \dot m_p \cdot \frac{1}{c^*}\cdot\ldots \quad\text{i.e.}\quad c = c^*\,C_F\ }
$$

$$
I_{sp}=\frac{c^*\,C_F}{g_0}
$$

**Why this matters:** in a test campaign, you can diagnose whether a shortfall is a **chamber** problem
(low $c^*$ ⇒ poor mixing, incomplete combustion, injector issue) or a **nozzle** problem (low $C_F$ ⇒
separation, erosion, wrong expansion ratio). Two independent measurements from one test. This is
standard practice and a very likely exam concept.

Typical $C_F$: 1.3–1.6 at sea level, up to 1.9–2.0 for high-expansion vacuum nozzles.

### 4. The Tsiolkovsky rocket equation

**The most important equation in astronautics.** Start with Newton's second law for a vehicle in
field-free space:

$$
m\frac{du}{dt}=F = -c\frac{dm}{dt}
$$

(the mass decreases, hence the sign). Separate:

$$
du = -c\frac{dm}{m}
$$

Integrate from initial mass $m_0$ to final mass $m_f$ with constant $c$:

$$
\boxed{\ \Delta V = c\,\ln\frac{m_0}{m_f} = I_{sp}\,g_0 \ln\frac{m_0}{m_f}\ }
$$

**Rearranged for the mass ratio required** — the form that hurts:

$$
\frac{m_0}{m_f}=\exp\left(\frac{\Delta V}{c}\right)
$$

**Propellant mass fraction:**

$$
\zeta = \frac{m_p}{m_0}=1-e^{-\Delta V/c}
$$

**The exponential is the tyranny.** Note the contrast with the Breguet range equation
([L09](L09-engine-aircraft-performance.md)), where the mass ratio also appears logarithmically — but
there it *multiplies* an $L/D$ of 18. A rocket has no $L/D$ to leverage; the mass ratio is
everything.

**Typical $\Delta V$ budgets:**

| Mission | $\Delta V$ (m/s) |
|---|---|
| LEO (incl. gravity + drag losses) | 9,300–10,000 |
| LEO → GTO | 2,500 |
| GTO → GEO | 1,500 |
| LEO → trans-lunar injection | 3,150 |
| Mars transfer | 3,600 |
| Lunar landing (from orbit) | 1,700 |

**The consequence, made concrete.** For LEO at $\Delta V = 9{,}400$ m/s:

- With kerosene/LOX ($c = 3{,}300$ m/s): $m_0/m_f = e^{2.85} = 17.3$ ⇒ **94.2% propellant**
- With LH₂/LOX ($c = 4{,}400$ m/s): $m_0/m_f = e^{2.14} = 8.5$ ⇒ **88.2% propellant**

Only 5.8% of the vehicle can be structure *and* payload in the first case. Since structure alone is
typically 6–10% of stage mass, **a single-stage-to-orbit chemical rocket is barely — if at all —
possible.** That's not an engineering shortfall; it's what the exponential says.

### 5. Staging

**The fix for the exponential:** throw away empty tanks so you stop accelerating dead mass.

For $n$ stages, $\Delta V$ adds:

$$
\Delta V_{\text{total}}=\sum_{i=1}^{n} c_i \ln\left(\frac{m_{0,i}}{m_{f,i}}\right)
$$

**Why it works:** each stage's mass ratio is computed against a smaller vehicle. The upper stages never
have to carry the first stage's empty tanks.

**Optimal staging** (equal $I_{sp}$, similar structural fractions) gives roughly **equal $\Delta V$ per
stage**. In practice the split is skewed because:
- Lower stages fight gravity and drag, favoring **high thrust** (dense propellants like RP-1)
- Upper stages operate in vacuum, favoring **high $I_{sp}$** (LH₂, huge nozzle expansion ratios)

**Diminishing returns:** going from 1 to 2 stages is transformative; 2 to 3 is worthwhile; beyond 3 the
added interstage structure, separation events, and failure modes usually outweigh the gain. Most
launchers are 2–3 stages.

**Losses that inflate the required $\Delta V$:**

$$
\Delta V_{\text{required}} = \Delta V_{\text{orbital}} + \Delta V_{\text{gravity}} + \Delta V_{\text{drag}} + \Delta V_{\text{steering}}
$$

- **Gravity loss** (1,200–1,500 m/s to LEO) — the component of thrust spent holding the vehicle up
  rather than accelerating it. Minimized by high initial thrust-to-weight and a prompt gravity turn.
- **Drag loss** (100–500 m/s) — modest, and reduced by not going too fast too low (hence max-Q
  throttling).
- **Steering loss** — thrust not aligned with velocity.

### 6. Thrust-to-weight and the launch constraint

$$
\frac{T}{W}=\frac{F}{m_0 g_0}
$$

**Must exceed 1 to lift off**, and in practice 1.2–1.5 at liftoff. Too low and gravity losses dominate;
too high and you incur excessive drag and structural loads.

**Note the tension:** high $I_{sp}$ engines (LH₂, and especially electric) tend to have **low thrust
density**. Electric propulsion has $I_{sp}$ 10× chemical but $T/W \ll 1$ — it can never launch, only
maneuver in space over months. **$I_{sp}$ and thrust are largely a trade**, and which one matters
depends entirely on whether you're fighting gravity.

### 7. Propellant classes

| Type | Examples | Character |
|---|---|---|
| **Liquid bipropellant** | LH₂/LOX, RP-1/LOX, CH₄/LOX, MMH/NTO | Throttleable, restartable, highest $I_{sp}$. Complex — needs turbopumps, valves, cooling. |
| **Solid** | APCP (AP + Al + HTPB binder) | Simple, storable, very high thrust density. **Cannot be throttled or shut down.** |
| **Hybrid** | Solid fuel + liquid oxidizer | Throttleable and safer than solid; poor combustion efficiency, low regression rate. |
| **Monopropellant** | Hydrazine over a catalyst bed | Very simple, reliable, low $I_{sp}$. Attitude control. |
| **Cold gas** | N₂, He | Trivially simple, tiny $I_{sp}$. Fine ACS, CubeSats. |

**Hypergolic** propellants (MMH/NTO, UDMH/N₂O₄) ignite on contact — no ignition system needed, and
restartable indefinitely. Standard for spacecraft and upper stages where reliability of restart is
paramount. The cost is extreme toxicity.

**Methane/LOX** is the modern favorite for reusable vehicles: better $I_{sp}$ than kerosene, far denser
than hydrogen, doesn't coke the cooling channels the way RP-1 does, and can be produced on Mars from
CO₂ and water (the Sabatier reaction).

**Why real vehicles mix propellants by stage** (e.g. Saturn V — kerosene first stage, hydrogen upper
stages): the choice is **density, not just $I_{sp}$**. Hydrogen's low density means huge tanks — more
structural mass, more drag, more surface area to insulate cryogenically — a bad trade at liftoff, when
thrust and thrust-to-weight dominate (§6) and the vehicle is fighting through the thickest atmosphere.
Kerosene's high density gives compact tanks and massive thrust for the first stage's brief, violent job.
Once above the atmosphere, drag and structural mass matter less, so upper stages spend their entire
flight in a regime where trading tank mass for higher $I_{sp}$ (hydrogen) pays off — exactly the same
logic that gives high-bypass turbofans their efficiency edge at cruise but not at takeoff
([propulsion-efficiencies](../../concepts/propulsion-efficiencies.md)).

---

## Worked logic — single-stage sounding rocket (burn + coast altitude)

*Cross-referenced from a parallel offering's in-class problem — a good warm-up before the two-stage
launcher below, since it introduces the **structural efficiency** and **payload coefficient**
bookkeeping used throughout staging analysis.*

**Definitions used across all staging problems:**

$$
\epsilon = \frac{m_{\text{struct}}}{m_{\text{struct}}+m_{\text{propellant}}}
\qquad(\text{structural efficiency})
$$

$$
\lambda = \frac{m_{\text{payload}}}{m_{\text{struct}}+m_{\text{propellant}}}
\qquad(\text{payload coefficient})
$$

**Given:** 350 kg payload, 1,000 kg propellant, $\epsilon=0.1$, $I_{sp}=250$ s, max acceleration
5$g$ (occurs at burnout, when the vehicle is lightest), $g=g_e=9.8\ \mathrm{m/s^2}$, negligible drag.
Find the burn time and peak altitude.

**Step 1 — masses.** From $\epsilon$: $m_{\text{struct}} = \epsilon\, m_p/(1-\epsilon) = 111.1$ kg.
So $m_0 = 350+111.1+1000 = 1{,}461.1$ kg, $m_f = 350+111.1 = 461.1$ kg (payload + structure only, fuel
spent).

**Step 2 — thrust from the burnout acceleration constraint.** Max $a$ occurs at burnout
(lightest mass), from the force balance $T-m_fg = m_f a_{\max}$:

$$
T = m_f\left(a_{\max}+g\right) = 461.1(5\times 9.8 + 9.8) \approx 27{,}132\ \mathrm N
$$

**Step 3 — propellant flow and burn time**, from $T = \dot m\, I_{sp}\, g$:

$$
\dot m = \frac{T}{I_{sp}\,g} = 11.1\ \mathrm{kg/s}
\;\Rightarrow\;
t_b = \frac{m_p}{\dot m} = 90.4\ \mathrm s
$$

**Step 4 — burnout velocity**, Tsiolkovsky with a gravity-loss term (constant $g$, vertical flight):

$$
u_e = I_{sp}\,g = 2{,}451.7\ \mathrm{m/s}, \qquad
V_{b} = u_e\ln\frac{m_0}{m_f} - g\,t_b = 1{,}941.4\ \mathrm{m/s}
$$

**Step 5 — split the trajectory into burn + coast**, since thrust stops at burnout but the rocket
keeps rising:

$$
h_{\text{burn}} \approx u_e t_b\left(1-\frac{m_f}{m_0}\right) - \tfrac12 g t_b^2 \approx 63{,}685\ \mathrm m
$$

$$
h_{\text{coast}} = \frac{V_b^2}{2g} \approx 192{,}166\ \mathrm m
\;\Rightarrow\;
h_{\text{total}} \approx 255{,}851\ \mathrm m \approx 256\ \mathrm{km}
$$

**The pattern worth keeping**: burnout velocity comes from Tsiolkovsky; total altitude comes from
**Tsiolkovsky plus a separate ballistic coast phase** — a rocket performance problem is rarely just
"plug into the rocket equation," it's the rocket equation feeding a second, more familiar
kinematics problem.

⚠️ **Notation watch:** the two-stage example below defines $\epsilon$ as structure-over-*stage-mass*
(structure/(structure+propellant+payload)), while this example used structure-over-(structure+
propellant) only. Both conventions appear in the wild — **always re-derive $\epsilon$ from whatever
masses a problem actually gives you**, rather than assuming a fixed formula.

---

## Worked logic — a two-stage launcher

**Given:** target $\Delta V = 9{,}400$ m/s.
**Stage 1:** RP-1/LOX, $I_{sp}=310$ s (sea level average), structural fraction $\epsilon_1 = 0.08$.
**Stage 2:** LH₂/LOX, $I_{sp}=450$ s, $\epsilon_2 = 0.12$.
Split the $\Delta V$ evenly: 4,700 m/s each.

**Step 1 — effective exhaust velocities:**

$$
c_1 = 310\times9.81=3{,}041\ \mathrm{m/s}, \qquad c_2 = 450\times9.81=4{,}415\ \mathrm{m/s}
$$

**Step 2 — required mass ratios:**

$$
\frac{m_{0,1}}{m_{f,1}}=e^{4700/3041}=e^{1.5455}=4.691
$$

$$
\frac{m_{0,2}}{m_{f,2}}=e^{4700/4415}=e^{1.0646}=2.900
$$

**Step 3 — stage 2 payload fraction.** With structural fraction $\epsilon$ (structure / stage mass),
the payload fraction of a stage is:

$$
\lambda = \frac{\frac{1}{R}-\epsilon}{1-\epsilon}, \qquad R = \frac{m_0}{m_f}
$$

$$
\lambda_2 = \frac{\frac{1}{2.900}-0.12}{1-0.12}=\frac{0.3448-0.12}{0.88}=\frac{0.2248}{0.88}=0.2555
$$

$$
\lambda_1 = \frac{\frac{1}{4.691}-0.08}{1-0.08}=\frac{0.2132-0.08}{0.92}=\frac{0.1332}{0.92}=0.1448
$$

**Step 4 — overall payload fraction:**

$$
\lambda_{\text{total}} = \lambda_1 \times \lambda_2 = 0.1448\times0.2555=0.0370
$$

**3.7% of liftoff mass reaches orbit as payload.** For a 500-tonne launcher, that's **18.5 tonnes** —
which is a realistic figure for a medium-lift vehicle.

**Step 5 — compare single stage.** Using the better engine ($c=4{,}415$) for the whole ascent:

$$
R = e^{9400/4415}=e^{2.129}=8.41
$$

$$
\lambda = \frac{\frac{1}{8.41}-0.12}{1-0.12}=\frac{0.1189-0.12}{0.88}= \frac{-0.0011}{0.88} < 0
$$

**Negative — physically impossible.** The structure alone exceeds the entire non-propellant budget.
**SSTO with these numbers cannot work**, whereas two stages deliver 3.7%.

**This calculation is the entire justification for staging** and is a very likely exam problem. Note how
sharply the answer flips — the exponential is unforgiving right at the margin.

**Step 6 — sanity check the split.** Try 5,200 m/s on stage 1 and 4,200 on stage 2:

$$
R_1 = e^{5200/3041}=5.55, \qquad \lambda_1 = \frac{0.1802-0.08}{0.92}=0.1089
$$

$$
R_2 = e^{4200/4415}=2.59, \qquad \lambda_2 = \frac{0.3861-0.12}{0.88}=0.3024
$$

$$
\lambda_{\text{total}}=0.1089\times0.3024=0.0329
$$

**Worse (3.29% vs. 3.70%)** — confirming the even split was closer to optimal here.

**Further practice — a 3-stage version** (cross-referenced from a parallel offering's homework):
same escape-mission setup, but 3 stages with $\epsilon_1=0.05$, $\epsilon_2=0.07$, $\epsilon_3=0.06$,
$I_{sp,1}=450$ s, $I_{sp,2}=350$ s, $I_{sp,3}=400$ s, and payload coefficients constrained by
$\lambda_2=0.9\lambda_1$, $\lambda_3=1.1\lambda_1$ rather than assumed equal. The method is identical
to the two-stage case above — write $\Delta V = \sum c_i \ln(m_{0,i}/m_{f,i})$, express each mass
ratio in terms of $\lambda_i$ and $\epsilon_i$, and solve the resulting system for $\lambda_1$ — but
the unequal $\lambda_i$ constraint is a good check that you understand the *structure* of the
staging equations rather than having memorized a two-stage-only formula. A companion problem also
asks for **velocity ratio between two competing vehicle designs** (one liquid-, one solid-propellant)
carrying the same payload — a reminder that $I_{sp}$, $\epsilon$, and Tsiolkovsky combine to make
*mission-level* trade studies, not just single-vehicle sizing.

---

## Common pitfalls

- **Including a ram drag term.** Rockets have none.
- **Assuming rocket thrust falls with altitude.** It **rises**.
- **Using sea-level $I_{sp}$ for a vacuum stage** or vice versa. Always state which.
- **Thinking maximum $I_{sp}$ is at stoichiometric mixture ratio.** It's **fuel-rich**, because
  $c\propto\sqrt{T_c/\mathcal M}$ and lowering $\mathcal M$ wins.
- **Confusing $c^*$ with $c$.** $c^*$ is the chamber metric; $c = c^* C_F$ is the effective exhaust
  velocity.
- **Forgetting gravity and drag losses** in a $\Delta V$ budget. LEO needs ~9,400, not the orbital
  7,800.
- **Applying the rocket equation across a staging event.** Apply per stage and sum.
- **Assuming high $I_{sp}$ is always better.** Electric propulsion cannot launch anything.
- **Using $g_0$ as local gravity.** It's a defined constant (9.80665), not the local value.

---

## Exam checklist

- [ ] Write the rocket thrust equation and explain the absence of ram drag
- [ ] Explain why rocket thrust increases with altitude
- [ ] Define $I_{sp}$ and $c$; convert between them; explain why the units are seconds
- [ ] **Explain $c\propto\sqrt{T_c/\mathcal M}$ and why LH₂/LOX and fuel-rich operation win**
- [ ] **Define $c^*$ and $C_F$; state what each diagnoses and show $c = c^* C_F$**
- [ ] **Derive the Tsiolkovsky rocket equation from $m\,du/dt = -c\,dm/dt$**
- [ ] Compute mass ratio and propellant fraction for a given $\Delta V$
- [ ] **Explain why staging is necessary; compute a two-stage payload fraction**
- [ ] List the $\Delta V$ loss terms and typical magnitudes
- [ ] Explain the $I_{sp}$ vs. thrust trade and why electric propulsion can't launch
- [ ] Compare propellant classes and explain hypergolic and methalox advantages

---

## Links

- Previous: [L22 — Centrifugal Compressors](L22-centrifugal-compressors.md)
- Next: [L24 — Rocket Engines 2](L24-rocket-engines-2.md) — chambers, nozzles, turbopumps
- Basic thrust concepts: [L01 — Introduction](L01-introduction.md)
- Choked flow: [L05 — Gas Dynamics](L05-gas-dynamics.md)
- Nozzle regimes: [L13 — Nozzles](L13-nozzles.md)
- Combustion: [L03](L03-combustion-thermodynamics-1.md), [L04](L04-combustion-thermodynamics-2.md)
- Course hub: [EAS4300](../EAS4300.md)
