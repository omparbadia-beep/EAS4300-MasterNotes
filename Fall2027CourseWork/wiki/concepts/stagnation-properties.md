# Stagnation (Total) Properties

**Type:** cross-cutting concept
**Used in:** [EAS4300](../courses/EAS4300.md) — L02 onward, essentially every lecture
**Tags:** #stagnation #total-properties #compressible-flow #energy-bookkeeping #entropy

---

## Definition

The **stagnation state** is the state a flowing fluid would reach if brought to rest:
- **adiabatically** (for stagnation temperature/enthalpy)
- **adiabatically and reversibly** (for stagnation pressure)

$$
h_0 \equiv h + \frac{V^2}{2}
$$

For a calorically perfect gas:

$$
T_0 = T + \frac{V^2}{2c_p} = T\left(1+\frac{\gamma-1}{2}M^2\right)
$$

$$
\frac{p_0}{p}=\left(1+\frac{\gamma-1}{2}M^2\right)^{\frac{\gamma}{\gamma-1}}
$$

$$
\frac{\rho_0}{\rho}=\left(1+\frac{\gamma-1}{2}M^2\right)^{\frac{1}{\gamma-1}}
$$

---

## Why the concept exists

**It collapses kinetic-energy bookkeeping into a single variable.**

In an adiabatic duct with no shaft work, velocity, static pressure, and static temperature can all
change wildly — but $h_0$ (and therefore $T_0$) is **constant**. So instead of tracking three
interdependent quantities, you track one.

## The two-line summary that does most of the work

> **$T_0$ tracks energy. $p_0$ tracks quality.**
>
> $T_0$ changes only with heat addition or shaft work.
> $p_0$ changes with those **and falls with any irreversibility.**

| Process | $T_0$ | $p_0$ |
|---|---|---|
| Ideal adiabatic, no work (inlet, nozzle, stator, duct) | constant | constant |
| **Real** adiabatic, no work | **constant** | **falls** |
| Heat addition (combustor) | rises | falls |
| Work in (compressor, fan) | rises | rises |
| Work out (turbine) | falls | falls |
| Normal shock | **constant** | falls sharply |
| Expansion fan | constant | constant |
| Friction (Fanno) | constant | falls |

---

## The key proof: $p_0$ can only fall

For any adiabatic, work-free process, entropy change in stagnation variables:

$$
s_2 - s_1 = c_p\ln\frac{T_{02}}{T_{01}} - R\ln\frac{p_{02}}{p_{01}}
$$

Adiabatic and work-free ⇒ $T_{02}=T_{01}$ ⇒ first term vanishes:

$$
s_2 - s_1 = -R\ln\frac{p_{02}}{p_{01}}
$$

Second law: $s_2 - s_1 \ge 0$, therefore:

$$
\boxed{\ \frac{p_{02}}{p_{01}} \le 1\ }
$$

**Loss = stagnation pressure loss.** This is why every component's real-world performance is quoted as a
$p_0$ ratio ($\pi_d$, $\pi_b$, $\pi_n$), and it's a very common short-answer exam item.

---

## Critical (sonic) values

The reference state used throughout gas dynamics, at $M=1$:

$$
\frac{T^*}{T_0}=\frac{2}{\gamma+1}, \qquad
\frac{p^*}{p_0}=\left(\frac{2}{\gamma+1}\right)^{\frac{\gamma}{\gamma-1}}
$$

| $\gamma$ | $T^*/T_0$ | $p^*/p_0$ | Choking $p_0/p_a$ |
|---|---|---|---|
| **1.4** (cold air) | 0.8333 | **0.5283** | 1.893 |
| **1.33** (hot gas) | 0.8584 | 0.5397 | 1.853 |
| 1.20 (rocket) | 0.9091 | 0.5644 | 1.772 |

**$p^*/p_0 = 0.528$ is the single most useful number in the course.** If the pressure ratio across a
converging nozzle exceeds ~1.89, it's choked.

---

## Relative stagnation properties (rotating frames)

In a rotor, the blade does work, so $h_0$ is not conserved. The relative-frame equivalents:

$$
h_{0,\text{rel}} = h + \frac{W^2}{2}, \qquad
T_{0,\text{rel}} = T\left(1+\frac{\gamma-1}{2}M_{\text{rel}}^2\right)
$$

**Rothalpy** is the quantity actually conserved across a rotor:

$$
I = h + \frac{W^2}{2}-\frac{U^2}{2} = \text{constant}
$$

For an **axial** rotor ($U_1 = U_2$), this reduces to $T_{0,\text{rel}}$ = constant.
For a **centrifugal** machine, the $U^2/2$ term is exactly what produces the large pressure rise
([L22](../courses/EAS4300/L22-centrifugal-compressors.md)).

---

## Common errors

- **Assuming $p_0$ is constant because the flow is adiabatic.** Adiabatic gives $T_0$ = constant.
  $p_0$ is constant only if it's *also* reversible.
- **Using static where stagnation belongs.** In any duct with velocity, $T \ne T_0$.
- **Applying isentropic relations across a shock.** $T_0$ carries; $p_0$ does not.
- **"Losing energy" in a shock.** Energy is conserved ($T_0$ constant); *availability* is lost.
- **Using $\gamma = 1.4$ in the hot section.** Use ~1.33.
- **Averaging Mach numbers.** $M$ isn't additive.

---

## Links

- [L02 — Basic Concepts](../courses/EAS4300/L02-basic-concepts.md) — introduced here
- [L05 — Gas Dynamics](../courses/EAS4300/L05-gas-dynamics.md) — applied to compressible flow
- [station-numbering](station-numbering.md)
- [corrected-parameters](corrected-parameters.md)
- [EAS4300 course hub](../courses/EAS4300.md)
