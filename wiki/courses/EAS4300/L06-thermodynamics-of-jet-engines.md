# L06 — Thermodynamics of Jet Engines

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 6 · **Date:** Fri 11 Sep 2026
**Book §:** 5.1 *Introduction* (p. 141) · 5.2 *Thrust and Efficiency* (p. 146) — ✅ verified
**Tags:** #thrust-equation #propulsive-efficiency #thermal-efficiency #overall-efficiency #TSFC #brayton #station-numbering #specific-thrust

---

## Why this lecture matters

This lecture is the **hinge of the course**. Lectures 1–5 built tools; Lectures 7–9 apply them to
specific engines. Here you assemble the tools into the general framework: station numbering, the
thrust equation, and the three efficiencies. Every cycle analysis for the rest of the semester is a
specialization of what's on this page.

---

## Core concepts

### 1. Station numbering — learn this cold

The standard aircraft-engine station convention (SAE ARP755). Every equation you write for the rest
of the course will carry these subscripts, and mixing them up makes an otherwise-correct solution
unmarkable.

| Station | Location |
|---|---|
| **0** or **a** | Free stream (ambient, far upstream) |
| **1** | Inlet / diffuser entry (highlight) |
| **2** | Compressor (or fan) face — inlet exit |
| **13** | Fan exit / bypass duct (turbofans) |
| **3** | Compressor exit / combustor entry |
| **4** | Combustor exit / **turbine inlet** (this is where TIT lives) |
| **4.5** | Between HP and LP turbine (two-spool engines) |
| **5** | Turbine exit |
| **6** | Afterburner entry / mixer exit |
| **7** | Nozzle entry (afterburner exit) |
| **8** | Nozzle **throat** |
| **9** or **e** | Nozzle **exit** plane |

**Component mapping:**
- Inlet/diffuser: **0 → 2**
- Fan: **2 → 13** (bypass) and **2 → 2.5** (core)
- Compressor: **2 → 3**
- Combustor: **3 → 4**
- Turbine: **4 → 5**
- Afterburner: **6 → 7**
- Nozzle: **7 → 9**

Full detail: [station-numbering](../../concepts/station-numbering.md).

### 2. The thrust equation, properly

Derived in [L02](L02-basic-concepts.md); restated here as the working form:

$$
F = \dot{m}_a\left[(1+f)u_e - u_a\right] + (p_e - p_a)A_e
$$

with $f = \dot m_f/\dot m_a$ from [L03](L03-combustion-thermodynamics-1.md).

**Three terms, three physical stories:**
- $\dot m_a (1+f) u_e$ — **gross thrust**: momentum thrown out the back
- $-\dot m_a u_a$ — **ram drag**: momentum you had to pick up. Grows with flight speed.
- $(p_e - p_a)A_e$ — **pressure thrust**: nonzero only if the nozzle isn't perfectly expanded

**Specific thrust** — thrust per unit air mass flow, the parameter that sets **engine size**:

$$
\frac{F}{\dot{m}_a} = (1+f)u_e - u_a + \frac{(p_e-p_a)A_e}{\dot{m}_a}
$$

High specific thrust ⇒ a small, light engine for a given thrust ⇒ good for fighters.
Low specific thrust with high mass flow ⇒ big fan, better fuel burn ⇒ good for airliners.
**Specific thrust and fuel efficiency pull in opposite directions.** That tension is the central design
trade of the whole subject and reappears in [L08b](L08b-turbofans.md) and [L09](L09-engine-aircraft-performance.md).

### 3. The three efficiencies

This is the most examinable content in the lecture. Each answers a different question.

#### Thermal efficiency — *how well does the engine convert fuel energy into kinetic energy?*

$$
\eta_{th} = \frac{\text{rate of KE added to the flow}}{\text{rate of fuel energy in}}
= \frac{\tfrac{1}{2}\dot{m}_a\left[(1+f)u_e^2 - u_a^2\right]}{\dot{m}_f\, Q_R}
$$

This is the **cycle** question — a Brayton cycle efficiency. It improves with **pressure ratio** and
**turbine inlet temperature**.

#### Propulsive efficiency — *how well does that kinetic energy become useful thrust power?*

$$
\eta_p = \frac{\text{thrust power delivered to vehicle}}{\text{rate of KE added to flow}}
= \frac{F u_a}{\tfrac{1}{2}\dot{m}_a\left[(1+f)u_e^2-u_a^2\right]}
$$

Neglecting $f$ and pressure thrust, this collapses to the **Froude efficiency** — the single most
important formula in the lecture:

$$
\eta_p = \frac{2u_a}{u_e + u_a} = \frac{2}{1 + u_e/u_a}
$$

**Read it carefully:**
- $\eta_p \to 1$ as $u_e \to u_a$ — but then thrust $\to 0$. **You cannot have both.**
- $\eta_p = 0$ at $u_a = 0$. A static engine delivers no propulsive power, period.
- Lower $u_e/u_a$ ⇒ better $\eta_p$ ⇒ **the argument for high bypass ratio**, exactly as previewed in
  [L01](L01-introduction.md).

**The waste is literal:** the exhaust leaves with residual kinetic energy relative to the ground, of
magnitude $\tfrac12 \dot m (u_e - u_a)^2$. That energy is dumped into the atmosphere as swirl and
turbulence and does nothing for you.

#### Overall efficiency

$$
\eta_o = \eta_{th}\,\eta_p = \frac{F u_a}{\dot{m}_f\, Q_R}
$$

The bottom line: **useful propulsive power out per unit fuel energy in.** Modern high-bypass turbofans
reach $\eta_o \approx 0.35$–$0.40$ at cruise — genuinely comparable to a good stationary power plant,
which is remarkable given the weight constraints.

### 4. Relation to TSFC

$$
\mathrm{TSFC} = \frac{\dot{m}_f}{F} = \frac{u_a}{\eta_o\, Q_R}
$$

**Note $u_a$ in the numerator.** At fixed $\eta_o$, TSFC *increases* with flight speed. Faster flight is
inherently thirstier per unit thrust — but you also need thrust for less time, which is why the range
equation ([L09](L09-engine-aircraft-performance.md)) contains $u_a/\mathrm{TSFC}$ and speed partly
cancels out.

### 5. The Brayton cycle behind it all

An air-breathing engine is an **open Brayton cycle**:

1. **0 → 3**: compression (ram + compressor), ideally isentropic
2. **3 → 4**: heat addition at constant pressure (combustor)
3. **4 → 9**: expansion (turbine + nozzle), ideally isentropic
4. **9 → 0**: heat rejection to atmosphere at constant pressure (the "cycle closes" through the sky)

**Ideal Brayton thermal efficiency:**

$$
\eta_{th,\text{ideal}} = 1 - \frac{1}{r_p^{\frac{\gamma-1}{\gamma}}}
= 1 - \frac{T_2}{T_3}
$$

with $r_p = p_{03}/p_{02}$ the overall pressure ratio.

**Two conclusions, both important:**
- **Thermal efficiency depends only on pressure ratio** (for the ideal cycle) — not on TIT. This is why
  overall pressure ratios have climbed from ~5 in early jets to **40–60** in modern turbofans.
- **But specific work — thrust per unit airflow — depends strongly on TIT.** Raising $T_{04}$ doesn't
  improve ideal $\eta_{th}$, but it lets a smaller engine make the same thrust.

For **real** cycles with component losses, an optimum pressure ratio appears: past a point, extra
compressor stages cost more in losses and weight than they return. The optimum $r_p$ rises with TIT,
which is why high-TIT and high-OPR engines evolved together.

### 6. Ideal vs. real component behavior

The bridge from ideal to real, using [L02](L02-basic-concepts.md)'s $p_0$ logic:

| Component | Ideal | Real |
|---|---|---|
| Inlet (0→2) | $p_{02}=p_{00}$, $T_{02}=T_{00}$ | $\pi_d = p_{02}/p_{00} < 1$; $T_0$ still constant |
| Compressor (2→3) | isentropic | $\eta_c < 1$ ⇒ more work for same $p$ rise |
| Combustor (3→4) | $p_{04}=p_{03}$ | $\pi_b \approx 0.94$–$0.98$; $\eta_b \approx 0.99$ |
| Turbine (4→5) | isentropic | $\eta_t < 1$ ⇒ less work for same $p$ drop |
| Nozzle (7→9) | isentropic | $\eta_n \approx 0.97$–$0.99$ |

**Isentropic efficiency definitions** — note the flip between compressor and turbine:

$$
\eta_c = \frac{h_{03s}-h_{02}}{h_{03}-h_{02}} = \frac{T_{03s}-T_{02}}{T_{03}-T_{02}}
\qquad(\text{ideal work} / \text{actual work})
$$

$$
\eta_t = \frac{h_{04}-h_{05}}{h_{04}-h_{05s}} = \frac{T_{04}-T_{05}}{T_{04}-T_{05s}}
\qquad(\text{actual work} / \text{ideal work})
$$

**Both are ≤ 1**, but the ratio is inverted because the compressor *consumes* work (you want to
consume little) while the turbine *produces* it (you want to produce a lot). Getting this backwards is
extremely common — write out which one is "ideal over actual" every time.

Useful working forms:

$$
T_{03} = T_{02}\left[1 + \frac{1}{\eta_c}\left(\pi_c^{\frac{\gamma-1}{\gamma}} - 1\right)\right]
$$

$$
T_{05} = T_{04}\left[1 - \eta_t\left(1 - \pi_t^{\frac{\gamma-1}{\gamma}}\right)\right]
$$

### 7. The work balance — how a gas generator holds together

The turbine drives the compressor. Nothing else. That single constraint closes the cycle:

$$
\dot{m}_a\, c_{p,c}\left(T_{03}-T_{02}\right)
= \eta_m\, \dot{m}_a (1+f)\, c_{p,h}\left(T_{04}-T_{05}\right)
$$

with $\eta_m \approx 0.99$ the mechanical (bearing/windage) efficiency. Solving for turbine exit
temperature:

$$
T_{05} = T_{04} - \frac{c_{p,c}\left(T_{03}-T_{02}\right)}{\eta_m (1+f)\, c_{p,h}}
$$

**Whatever pressure remains after station 5 is what the nozzle gets to make thrust with.** That single
sentence explains the turbojet, and it explains why a turbofan diverts more turbine work: the fan is
just another load on the same shaft.

---

## Worked logic — the efficiency chain, end to end

Follow the energy from tank to vehicle.

**1. Fuel chemical power in:**

$$
\dot{E}_{\text{fuel}} = \dot{m}_f\, Q_R
$$

**2. Converted to flow kinetic energy** (thermal efficiency):

$$
\dot{E}_{KE} = \eta_{th}\, \dot{m}_f Q_R = \tfrac{1}{2}\dot{m}_a\left[(1+f)u_e^2 - u_a^2\right]
$$

**3. Converted to thrust power** (propulsive efficiency):

$$
P = \eta_p \dot{E}_{KE} = F u_a
$$

**4. Overall:**

$$
\eta_o = \frac{Fu_a}{\dot{m}_f Q_R} = \eta_{th}\eta_p
$$

### Numerical illustration — why the turbofan won

Two engines, same flight speed $u_a = 250$ m/s, same thrust $F = 50$ kN, same $\eta_{th} = 0.45$.

**Turbojet:** $u_e = 600$ m/s.

$$
\dot{m}_a = \frac{F}{u_e-u_a} = \frac{50{,}000}{350} = 143\ \mathrm{kg/s}
$$

$$
\eta_p = \frac{2(250)}{600+250} = 0.588
\quad\Longrightarrow\quad \eta_o = 0.45 \times 0.588 = 0.265
$$

**Turbofan:** $u_e = 350$ m/s.

$$
\dot{m}_a = \frac{50{,}000}{100} = 500\ \mathrm{kg/s}
$$

$$
\eta_p = \frac{2(250)}{350+250} = 0.833
\quad\Longrightarrow\quad \eta_o = 0.45 \times 0.833 = 0.375
$$

**Result: 42% better overall efficiency, at the cost of 3.5× the mass flow** — meaning a much larger,
heavier fan and nacelle, with more drag. That trade is the entire history of commercial engine
development since the 1960s: bypass ratios climbed from 1 to 12+ as materials and nacelle design let
designers afford the size.

---

## Common pitfalls

- **Inverting $\eta_c$ and $\eta_t$.** Compressor: ideal/actual. Turbine: actual/ideal.
- **Using $\eta_{th}$ when the question wants $\eta_o$.** Thermal efficiency ignores whether the KE
  actually propelled anything.
- **Forgetting $\eta_p = 0$ at static conditions.** A test-stand engine has *undefined or zero*
  propulsive efficiency, no matter its thrust.
- **Using one $c_p$ across the burner.** Cold section 1005, hot section ~1150 J/(kg·K).
- **Ignoring $(1+f)$ in the turbine and nozzle mass flows.**
- **Assuming higher $u_e$ is better.** It raises specific thrust but wrecks $\eta_p$.
- **Believing ideal $\eta_{th}$ depends on TIT.** It doesn't — only on pressure ratio. TIT drives
  *specific work*.
- **Mislabeling stations.** Station 3 is compressor *exit*; station 4 is turbine *inlet*.

---

## Exam checklist

- [ ] Reproduce the station numbering table and map each component to its stations
- [ ] Write the full thrust equation and identify gross thrust, ram drag, pressure thrust
- [ ] Define $\eta_{th}$, $\eta_p$, $\eta_o$ and state what question each answers
- [ ] Derive the Froude efficiency $\eta_p = 2/(1+u_e/u_a)$ and interpret both limits
- [ ] Explain the specific-thrust vs. fuel-efficiency trade
- [ ] State ideal Brayton $\eta_{th}$ and explain why it depends on $r_p$ but not TIT
- [ ] Write $\eta_c$ and $\eta_t$ correctly and derive $T_{03}$, $T_{05}$
- [ ] Write the compressor-turbine work balance and solve for $T_{05}$
- [ ] Relate TSFC to $\eta_o$ and explain the $u_a$ dependence

---

## Links

- Previous: [L05 — Gas Dynamics](L05-gas-dynamics.md)
- Next: [L07 — Ramjets](L07-ramjets.md) — simplest application of this framework
- Then: [L08a — Turbojets](L08a-turbojets.md), [L08b — Turbofans](L08b-turbofans.md)
- Concept: [propulsion-efficiencies](../../concepts/propulsion-efficiencies.md)
- Concept: [station-numbering](../../concepts/station-numbering.md)
- Course hub: [EAS4300](../EAS4300.md)
