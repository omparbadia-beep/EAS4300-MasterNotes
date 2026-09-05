# Midterm 1 — Scope and Prep

**Course:** EAS 4300 Aerospace Propulsion
**Date:** **Wed 7 Oct 2026**, in class, 3:00–3:50 PM, Matherly 0018
**Weight:** 25% of final grade · 100 points
**Review session:** Mon 5 Oct (in class)
**Tags:** #exam #midterm-1 #review

⏱️ **50 minutes.** That is a hard pacing constraint — roughly 12 minutes per question on a 4-question
exam. You will not have time to re-derive things from scratch. Know the standard results cold.

---

## Scope

Everything from **L01 through L12** (last new material 2 Oct).

| # | Lecture | Book § | Weight guess |
|---|---|---|---|
| 1 | [Introduction](L01-introduction.md) | 1.1–1.2, 1.4 | Low — conceptual |
| 2 | [Basic Concepts](L02-basic-concepts.md) | 2.1–2.3 | **High** — foundational |
| 3 | [Combustion Thermo 1](L03-combustion-thermodynamics-1.md) | 2.4 | Medium |
| 4 | [Combustion Thermo 2](L04-combustion-thermodynamics-2.md) | 2.4 | Medium |
| 5 | [Gas Dynamics](L05-gas-dynamics.md) | 3.1–3.6 | **Highest** — 3 lectures |
| 6 | [Jet Engine Thermo](L06-thermodynamics-of-jet-engines.md) | 5.1–5.2 | **High** — the hinge |
| 7 | [Ramjets](L07-ramjets.md) | 5.3 | Medium |
| 8a | [Turbojets](L08a-turbojets.md) | 5.4 | **High** — 2 lectures |
| 8b | [Turbofans](L08b-turbofans.md) | **5.5** ⚠️ | **High** — 2 lectures |
| 9 | [Engine/Aircraft Performance](L09-engine-aircraft-performance.md) | 5.7–**5.8** ⚠️ | Medium |
| 10 | [Inlets](L10-inlets.md) | 6.1–6.3 | Medium |
| 11 | [Combustors](L11-combustors.md) | 6.4 | Medium |
| 12 | [Afterburners](L12-afterburners-ramjet-combustors.md) | 6.5 | Low–Medium |

**Not on this exam:** nozzles (L13), all turbomachinery (L14–L22), rockets (L23–L24), testing (L25).

**Homework covered:** HW1 (out 31 Aug), HW2 (14 Sep), HW3 (21 Sep), HW4 (28 Sep).
**Rework these — midterm problems are usually close relatives of homework problems.**

---

## The five things most likely to appear

Ranked by (lecture time × examinability):

### 1. A full cycle analysis march (turbojet or turbofan)
The single highest-probability problem type. Given flight condition, $\pi_c$, $T_{04}$, component
efficiencies — march stations 0→9 and produce specific thrust and TSFC.

**Practice until automatic:** [L08a worked example](L08a-turbojets.md#worked-logic--ideal-turbojet-at-cruise),
[L08b worked example](L08b-turbofans.md#worked-logic--turbofan-vs-turbojet-matched-conditions).

**Do not forget:** the turbine work balance sets $T_{05}$ — the turbine does *not* expand to ambient.
For a turbofan, include the $\alpha(\tau_f-1)$ term.

### 2. Gas dynamics: nozzle regime, shock, or choking
Given a geometry and pressure ratio: is it choked? Which $A/A^*$ root? Where's the shock? What's
$p_{02}/p_{01}$?

**Know cold:** $p^*/p_0 = 0.528$, the choking condition, the seven C-D nozzle regimes, and the normal
shock table trend ($p_{02}/p_{01} = 0.72$ at $M$=2, $0.33$ at $M$=3).

### 3. Derivations
Short, standard, and high-yield:
- **Thrust equation from a CV momentum balance** ([L02](L02-basic-concepts.md))
- **Froude efficiency** $\eta_p = 2/(1+u_e/u_a)$ ([L06](L06-thermodynamics-of-jet-engines.md))
- **$dA/A = (M^2-1)dV/V$** ([L05](L05-gas-dynamics.md))
- **$p_{02}\le p_{01}$** for adiabatic work-free flow ([L02](L02-basic-concepts.md))
- **Breguet range equation** ([L09](L09-engine-aircraft-performance.md))

### 4. Combustion: fuel-air ratio or air split
Compute $f$ from the burner energy balance; compute $\phi$; do a combustor air split to hit a target
primary-zone $\phi$ ([L11 worked example](L11-combustors.md#worked-logic--air-split-and-exit-temperature)).

**Do not forget the $-c_p T_{04}$ term** in the $f$ denominator.

### 5. Conceptual short-answer
- Why do turbofans beat turbojets subsonically?
- Why can't a ramjet produce static thrust? Why does it die at high Mach?
- Why is a single normal shock unacceptable above M 1.6?
- Why is a combustor overall lean but locally stoichiometric?
- Why must $A_8$ open when the afterburner lights?

---

## Formula sheet (assemble your own version of this)

### Thrust and efficiency
$$
F = \dot m_a\left[(1+f)u_e-u_a\right]+(p_e-p_a)A_e
$$
$$
\eta_p = \frac{2}{1+u_e/u_a}, \qquad \eta_o = \eta_{th}\eta_p = \frac{Fu_a}{\dot m_f Q_R},
\qquad \mathrm{TSFC}=\frac{\dot m_f}{F}
$$

### Cycle
$$
\tau_r = 1+\frac{\gamma-1}{2}M_0^2, \qquad \pi_r = \tau_r^{\frac{\gamma}{\gamma-1}},
\qquad \tau_\lambda = \frac{T_{04}}{T_0}
$$
$$
\tau_t = 1-\frac{\tau_r}{\tau_\lambda}\left[(\tau_c-1)+\alpha(\tau_f-1)\right]
$$
$$
\tau_{c,\text{opt}}=\frac{\sqrt{\tau_\lambda}}{\tau_r}, \qquad
f = \frac{c_{p,h}T_{04}-c_{p,c}T_{03}}{\eta_b Q_R - c_{p,h}T_{04}}
$$
$$
\eta_c = \frac{T_{03s}-T_{02}}{T_{03}-T_{02}}, \qquad \eta_t = \frac{T_{04}-T_{05}}{T_{04}-T_{05s}}
$$

### Gas dynamics
$$
\frac{T_0}{T}=1+\frac{\gamma-1}{2}M^2, \qquad \frac{p_0}{p}=\left(\frac{T_0}{T}\right)^{\frac{\gamma}{\gamma-1}}
$$
$$
\frac{A}{A^*}=\frac{1}{M}\left[\frac{2}{\gamma+1}\left(1+\frac{\gamma-1}{2}M^2\right)\right]^{\frac{\gamma+1}{2(\gamma-1)}}
$$
$$
\dot m = \frac{p_0A^*}{\sqrt{T_0}}\sqrt{\frac{\gamma}{R}}\left(\frac{2}{\gamma+1}\right)^{\frac{\gamma+1}{2(\gamma-1)}}
$$
$$
M_2^2 = \frac{1+\frac{\gamma-1}{2}M_1^2}{\gamma M_1^2-\frac{\gamma-1}{2}}, \qquad M_{n1}=M_1\sin\beta
$$

### Aircraft performance
$$
R = \frac{u}{g_0\mathrm{TSFC}}\left(\frac{L}{D}\right)\ln\frac{W_i}{W_f}
$$

---

## Numbers to memorize

| | |
|---|---|
| $R_{\text{air}}$ = 287 J/(kg·K) | $g_0$ = 9.80665 m/s² |
| $c_p$ cold = 1005, hot ≈ 1150 J/(kg·K) | $\gamma$ cold = 1.4, hot ≈ 1.33 |
| $p^*/p_0$ = **0.528** ($\gamma$=1.4) | $T^*/T_0$ = 0.833 |
| Choking $p_0/p_a$ = 1.89 | $Q_R$ (Jet-A) ≈ 43 MJ/kg |
| $f_{\text{stoich}}$ ≈ 0.068 | Typical cruise $f$ ≈ 0.02–0.025 |
| Normal shock $p_{02}/p_{01}$: M2 → 0.72, M3 → 0.33 | $\pi_b$ ≈ 0.95, $\eta_b$ ≈ 0.99 |

---

## Top 10 pitfalls to check on every answer

1. **Cold vs. hot $c_p$ and $\gamma$** — did you switch at station 4?
2. **$\eta_c$ vs. $\eta_t$ inversion** — compressor: ideal/actual. Turbine: actual/ideal.
3. **Forgetting the turbine work balance** sets $T_{05}$
4. **Forgetting $\alpha(\tau_f-1)$** in a turbofan
5. **Dropping the pressure thrust term** when $p_e \ne p_a$
6. **Wrong $A/A^*$ root** — subsonic vs. supersonic
7. **Using $M_1$ not $M_{n1}=M_1\sin\beta$** for oblique shocks
8. **Applying isentropic relations across a shock**
9. **Dropping $-c_pT_{04}$** from the $f$ denominator
10. **Units** — especially TSFC, and $\dot m$ vs. $\dot m_{\text{core}}$ vs. $\dot m_{\text{total}}$

---

## Suggested 5-day plan

| Day | Focus |
|---|---|
| **5 days out** | Re-read [L06](L06-thermodynamics-of-jet-engines.md) and [L02](L02-basic-concepts.md). Station numbering and the four conservation laws from memory. |
| **4 days out** | [L05](L05-gas-dynamics.md) — reproduce the §11 summary table blind. Work shock and nozzle problems. |
| **3 days out** | Rework HW1–HW4 **without looking at your solutions**. |
| **2 days out** | Cycle marches: do the [L08a](L08a-turbojets.md) and [L08b](L08b-turbofans.md) worked examples from a blank page. |
| **1 day out** | Components ([L10](L10-inlets.md)–[L12](L12-afterburners-ramjet-combustors.md)) — conceptual. Write your formula sheet. Attend the 5 Oct review. |

---

## Links

- Course hub: [EAS4300](../EAS4300.md)
- Next exam: [exam-midterm-2](exam-midterm-2.md)
- [exam-final](exam-final.md)
- Concepts: [station-numbering](../../concepts/station-numbering.md) ·
  [stagnation-properties](../../concepts/stagnation-properties.md) ·
  [propulsion-efficiencies](../../concepts/propulsion-efficiencies.md)
