# Propulsion Efficiencies

**Type:** cross-cutting concept
**Used in:** [EAS4300](../courses/EAS4300.md) — L01, L06–L09, and every cycle analysis
**Tags:** #efficiency #propulsive #thermal #overall #froude #tsfc #isp

---

## The three efficiencies, and the question each answers

| Efficiency | Question it answers | Improved by |
|---|---|---|
| **Thermal $\eta_{th}$** | How well does fuel energy become flow kinetic energy? | Pressure ratio, component efficiency |
| **Propulsive $\eta_p$** | How well does that KE become useful thrust power? | **Lower exhaust velocity** (higher bypass) |
| **Overall $\eta_o$** | Fuel energy → propulsive power, end to end | Both |

$$
\eta_{th}=\frac{\tfrac12\dot m_a\left[(1+f)u_e^2-u_a^2\right]}{\dot m_f Q_R}
$$

$$
\eta_p = \frac{F u_a}{\tfrac12\dot m_a\left[(1+f)u_e^2-u_a^2\right]}
$$

$$
\eta_o = \eta_{th}\,\eta_p = \frac{F u_a}{\dot m_f Q_R}
$$

---

## Froude propulsive efficiency — the central result

Neglecting $f$ and pressure thrust:

$$
\boxed{\ \eta_p = \frac{2u_a}{u_e+u_a}=\frac{2}{1+u_e/u_a}\ }
$$

**Read both limits:**
- $u_e \to u_a$: $\eta_p \to 1$, but thrust $F = \dot m(u_e-u_a) \to 0$. **You cannot have both.**
- $u_a = 0$: $\eta_p = 0$. A static engine delivers **zero** propulsive power regardless of thrust.

**The waste is literal:** the exhaust leaves with residual KE $\tfrac12\dot m(u_e-u_a)^2$ relative to
the ground, dumped into the atmosphere as turbulence.

### The design consequence

For fixed added energy:

$$
\frac{F}{\dot E}=\frac{2}{u_e+u_a}
$$

**Thrust per unit energy is maximized by minimizing $u_e$** — but small increments need large $\dot m$
to keep thrust up. Hence: **move a lot of air slowly, not a little air quickly.**

That single sentence is the argument for the turbofan, for high bypass ratio, and (in the limit) for
the propeller. It's also why rockets — which cannot ingest mass — are stuck with high $u_e$.

**Typical values at cruise:**

| Engine | $\eta_p$ |
|---|---|
| Turbojet at M 0.85 | ~0.36 |
| Low-bypass turbofan | ~0.6 |
| High-bypass turbofan ($\alpha$=8–10) | **0.75–0.85** |
| Turboprop | 0.85–0.9 |
| Rocket at low speed | very low |

---

## Component isentropic efficiencies — note the inversion

$$
\eta_c = \frac{T_{03s}-T_{02}}{T_{03}-T_{02}} \qquad \text{ideal work / actual work}
$$

$$
\eta_t = \frac{T_{04}-T_{05}}{T_{04}-T_{05s}} \qquad \text{actual work / ideal work}
$$

**Both ≤ 1, but the ratio is inverted** — the compressor *consumes* work (you want to consume little)
while the turbine *produces* it (you want to produce a lot). **Getting this backwards is one of the
most common errors in the course.** Write out "ideal over actual" explicitly every time.

Working forms:

$$
T_{03}=T_{02}\left[1+\frac{1}{\eta_c}\left(\pi_c^{\frac{\gamma-1}{\gamma}}-1\right)\right]
$$

$$
T_{05}=T_{04}\left[1-\eta_t\left(1-\pi_t^{\frac{\gamma-1}{\gamma}}\right)\right]
$$

---

## Polytropic efficiency and the preheat/reheat asymmetry

Isentropic efficiency depends on pressure ratio even for machines of identical aerodynamic quality.
**Polytropic (small-stage) efficiency** removes that dependence:

$$
\tau_c = \pi_c^{\frac{\gamma-1}{\gamma\eta_{p,c}}} \qquad\text{(compressor)}
$$

$$
\tau_t = \pi_t^{\frac{(\gamma-1)\eta_{p,t}}{\gamma}} \qquad\text{(turbine)}
$$

**The sign flips between the two — know this cold:**

| | Effect of upstream losses | Relationship |
|---|---|---|
| **Compressor** | **Preheat** — hotter inlet means the next stage needs *more* work | $\eta_c < \eta_p$ |
| **Turbine** | **Reheat** — hotter inlet means the next stage can extract *more* work | $\eta_t > \eta_p$ |

Both gaps **widen with pressure ratio**. Constant-pressure lines diverging on a $T$-$s$ diagram is the
underlying reason for both.

---

## TSFC and specific impulse

$$
\mathrm{TSFC}=\frac{\dot m_f}{F}=\frac{u_a}{\eta_o Q_R}
$$

$$
I_{sp}=\frac{F}{\dot m_p g_0}, \qquad \mathrm{TSFC}=\frac{1}{I_{sp}g_0}
$$

**Note $u_a$ in the TSFC numerator** — faster flight is thirstier per unit thrust. But in the Breguet
range equation the group $u/\mathrm{TSFC} = \eta_o Q_R$, so **speed cancels** and range depends on
$\eta_o$, not speed per se ([L09](../courses/EAS4300/L09-engine-aircraft-performance.md)).

**Air-breathing vs. rocket $I_{sp}$ are not comparable as efficiencies** — air-breathers count only
fuel in the denominator, rockets count all propellant. A 3,000 s turbofan is not "10× better" than a
400 s rocket in any thermodynamic sense.

---

## Common errors

- **Inverting $\eta_c$ and $\eta_t$**
- **Using $\eta_{th}$ when the question wants $\eta_o$**
- **Forgetting $\eta_p = 0$ statically**
- **Assuming higher $u_e$ is better** — it raises specific thrust but wrecks $\eta_p$
- **Getting the polytropic inequality direction backwards**
- **Comparing $I_{sp}$ across engine families as an efficiency**
- **Believing ideal $\eta_{th}$ depends on TIT** — it depends on pressure ratio; TIT drives *specific work*

---

## Links

- [L01 — Introduction](../courses/EAS4300/L01-introduction.md)
- [L06 — Thermodynamics of Jet Engines](../courses/EAS4300/L06-thermodynamics-of-jet-engines.md) — main treatment
- [L08b — Turbofans](../courses/EAS4300/L08b-turbofans.md) — the design payoff
- [L09 — Engine/Aircraft Performance](../courses/EAS4300/L09-engine-aircraft-performance.md) — Breguet
- [L15 — Compressors 2](../courses/EAS4300/L15-compressors-2.md) — polytropic/preheat
- [L20 — Turbines 2](../courses/EAS4300/L20-turbines-2.md) — polytropic/reheat
- [EAS4300 course hub](../courses/EAS4300.md)
