# L08a — Turbojets

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 8 (part 1 of 2)
**Dates:** Wed 16 Sep, Fri 18 Sep 2026
**Book §:** 5.4 *Turbojet Engines* (p. 164) — ✅ verified
**Tags:** #turbojet #cycle-analysis #brayton #gas-generator #work-balance #optimum-pressure-ratio #spool

---

## Why this lecture matters

The turbojet solves the ramjet's fatal flaw — **zero static thrust** — by adding a compressor to supply
pressure ratio that flight speed can't. The price is a turbine to drive it. This lecture is the **full
cycle analysis** template: once you can march station-by-station through a turbojet, the turbofan
([L08b](L08b-turbofans.md)) is the same march with a second stream.

---

## Core concepts

### 1. Architecture and stations

```
0 → [Inlet] → 2 → [Compressor] → 3 → [Burner] → 4 → [Turbine] → 5 → [Nozzle] → 9
```

The **gas generator** (core) is stations **2→5**: compressor, burner, turbine. Everything else — nozzle,
fan, afterburner — bolts onto that core. This modularity is real: manufacturers reuse a core across
turbojet, turbofan, and turboshaft product lines.

**The defining constraint** (restated from [L06](L06-thermodynamics-of-jet-engines.md)):
**the turbine exists only to drive the compressor.** Whatever pressure is left at station 5 goes to the
nozzle to make thrust.

### 2. The cycle parameters

Standard notation used throughout the rest of the course:

$$
\tau_r = \frac{T_{02}}{T_0} = 1 + \frac{\gamma-1}{2}M_0^2
\qquad\text{(ram temperature ratio)}
$$

$$
\pi_r = \frac{p_{02}}{p_0} = \left(1+\frac{\gamma-1}{2}M_0^2\right)^{\frac{\gamma}{\gamma-1}}
\qquad\text{(ram pressure ratio)}
$$

$$
\pi_c = \frac{p_{03}}{p_{02}}, \qquad
\tau_c = \frac{T_{03}}{T_{02}} = \pi_c^{\frac{\gamma-1}{\gamma}}\ \text{(ideal)}
$$

$$
\pi_t = \frac{p_{05}}{p_{04}}, \qquad
\tau_t = \frac{T_{05}}{T_{04}}
$$

$$
\tau_\lambda = \frac{T_{04}}{T_0}
\qquad\text{(cycle temperature ratio — the TIT parameter)}
$$

$\tau_\lambda$ and $\pi_c$ are **the two design knobs**. Nearly every turbojet result is a statement
about how performance varies with those two.

### 3. Ideal turbojet cycle — station by station

**Assumptions:** isentropic inlet/compressor/turbine/nozzle, constant-pressure burner, $f \ll 1$,
perfectly expanded nozzle ($p_9 = p_0$), single $\gamma$ and $c_p$.

**Inlet (0→2):**

$$
T_{02} = T_0 \tau_r, \qquad p_{02} = p_0 \pi_r
$$

**Compressor (2→3):**

$$
T_{03} = T_{02}\tau_c = T_0 \tau_r \tau_c, \qquad p_{03} = p_{02}\pi_c
$$

**Burner (3→4):**

$$
T_{04} = T_0 \tau_\lambda, \qquad p_{04} = p_{03}
$$

**Turbine (4→5) — from the work balance.** Turbine work = compressor work:

$$
c_p\left(T_{04}-T_{05}\right) = c_p\left(T_{03}-T_{02}\right)
$$

$$
T_{05} = T_{04} - T_{02}\left(\tau_c - 1\right)
$$

In ratio form — **this is the key relation**:

$$
\tau_t = 1 - \frac{\tau_r}{\tau_\lambda}\left(\tau_c - 1\right)
$$

$$
\pi_t = \tau_t^{\frac{\gamma}{\gamma-1}}
$$

**Nozzle (5→9), perfectly expanded:**

$$
\frac{p_{05}}{p_0} = \pi_r \pi_c \pi_t
$$

$$
M_9^2 = \frac{2}{\gamma-1}\left[\left(\frac{p_{05}}{p_0}\right)^{\frac{\gamma-1}{\gamma}} - 1\right]
$$

$$
T_9 = \frac{T_{05}}{1+\frac{\gamma-1}{2}M_9^2}, \qquad
u_9 = M_9\sqrt{\gamma R T_9}
$$

**Specific thrust:**

$$
\frac{F}{\dot{m}_a} = u_9 - u_0 = a_0\left(M_9\sqrt{\frac{T_9}{T_0}} - M_0\right)
$$

**Fuel-air ratio:**

$$
f = \frac{c_p T_0\left(\tau_\lambda - \tau_r \tau_c\right)}{\eta_b Q_R - c_p T_0 \tau_\lambda}
$$

**TSFC:**

$$
\mathrm{TSFC} = \frac{f}{F/\dot{m}_a}
$$

**The march is always the same:** ram → compress → burn → extract turbine work equal to compressor
work → expand what's left. Memorize the *sequence*, not the individual formulas.

### 4. The optimum compressor pressure ratio

Unlike the ideal Brayton result (efficiency rises monotonically with $r_p$), **specific thrust has a
genuine maximum in $\pi_c$**, even for an ideal cycle. The reason is a direct competition:

- **Raising $\pi_c$** raises cycle efficiency and $T_{03}$
- **But** higher $T_{03}$ means less temperature rise available in the burner (with $T_{04}$ fixed by
  materials), and more turbine work is consumed driving the bigger compressor
- **Result:** less pressure and energy left over for the nozzle

Maximizing $F/\dot m_a$ with respect to $\tau_c$ gives the classical result:

$$
\tau_{c,\text{opt}} = \frac{\sqrt{\tau_\lambda}}{\tau_r}
$$

$$
\pi_{c,\text{opt}} = \left(\frac{\sqrt{\tau_\lambda}}{\tau_r}\right)^{\frac{\gamma}{\gamma-1}}
$$

**Interpretation — three things to say about this in an exam:**

1. **The optimum rises with $\tau_\lambda$ (TIT).** Hotter turbines justify bigger compressors. This is
   the historical driver: as blade materials and cooling improved, OPR climbed alongside.
2. **The optimum falls with $\tau_r$ (flight Mach).** At high speed, ram compression already does the
   job, so the compressor should be smaller. Taken to the limit, $\tau_c \to 1$ — **the engine becomes
   a ramjet.** The turbojet and ramjet are endpoints of one continuum.
3. It's the optimum for **specific thrust**, not for **TSFC**. Minimum TSFC occurs at a *higher* $\pi_c$.
   Fighters size near max specific thrust (small engine); transports near min TSFC (cheap fuel).

### 5. Real turbojet — component losses

Replace the ideal steps with efficiency-corrected ones ([L06](L06-thermodynamics-of-jet-engines.md)):

**Inlet:** $\pi_d < 1$. Military standard for supersonic recovery:

$$
\pi_{d} = \pi_{d,\max}\left[1 - 0.075\left(M_0-1\right)^{1.35}\right] \quad (M_0 > 1)
$$

**Compressor:**

$$
\tau_c = 1 + \frac{1}{\eta_c}\left(\pi_c^{\frac{\gamma_c-1}{\gamma_c}}-1\right)
$$

**Burner:** $\pi_b \approx 0.94$–$0.98$, $\eta_b \approx 0.99$.

**Turbine** — the work balance now carries $\eta_m$, $(1+f)$, and hot-section $c_p$:

$$
T_{05} = T_{04} - \frac{c_{p,c}\,T_{02}\left(\tau_c-1\right)}{\eta_m\,(1+f)\,c_{p,h}}
$$

$$
\pi_t = \left[1 - \frac{1}{\eta_t}\left(1-\tau_t\right)\right]^{\frac{\gamma_h}{\gamma_h-1}}
$$

**Nozzle:** $\eta_n \approx 0.98$, and the nozzle may not be perfectly expanded — retain the pressure
thrust term.

**Where the losses actually bite:** at high flight Mach the *inlet* dominates (shock losses,
[L10](L10-inlets.md)). At low speed, compressor and turbine efficiencies dominate. The burner and
nozzle are comparatively small contributors at design point.

### 6. Spools

A **spool** is one compressor + one turbine on a common shaft, free to run at its own speed.

- **Single-spool:** simple, but every stage is locked to one rotational speed. Off-design behavior is
  poor because front and rear stages want very different speeds (see
  [L17](L17-compressors-4.md) on stage matching).
- **Two-spool:** LP compressor + LP turbine on the inner shaft; HP compressor + HP turbine on the
  concentric outer shaft. The HP spool runs faster. This dramatically improves off-design matching and
  is standard practice.
- **Three-spool:** Rolls-Royce architecture (fan / IP / HP), better matching still, more mechanical
  complexity.

**Why more spools help:** the front stages see high-density-variation flow and need lower speed;
the rear stages need higher speed. Decoupling them lets each run near its own optimum across the
throttle range. This is the practical fix for the compressor-matching problem in
[L16](L16-compressors-3.md).

### 7. Where turbojets win and lose

**Wins:** high specific thrust (small frontal area, light for a given thrust), good performance at
high supersonic Mach, mechanically simple relative to a turbofan.

**Loses:** poor propulsive efficiency at subsonic speed (high $u_e$, Froude efficiency from
[L06](L06-thermodynamics-of-jet-engines.md)), very noisy (jet noise scales roughly as $u_e^8$).

**Consequence:** pure turbojets have essentially vanished from civil aviation, replaced entirely by
turbofans. They survive in high-Mach military and missile applications where specific thrust and
frontal area dominate the trade.

---

## Worked logic — ideal turbojet at cruise

**Given:** $M_0 = 0.85$, $T_0 = 220$ K, $\gamma=1.4$, $c_p = 1005$ J/(kg·K), $\pi_c = 20$,
$T_{04} = 1600$ K, $Q_R = 43$ MJ/kg, ideal components.

**Step 1 — ram:**

$$
\tau_r = 1 + 0.2(0.85)^2 = 1.1445
\quad\Longrightarrow\quad T_{02} = 251.8\ \mathrm{K}
$$

$$
\pi_r = (1.1445)^{3.5} = 1.604
$$

**Step 2 — compressor:**

$$
\tau_c = 20^{0.2857} = 2.354
\quad\Longrightarrow\quad T_{03} = 251.8 \times 2.354 = 592.7\ \mathrm{K}
$$

**Step 3 — burner:**

$$
\tau_\lambda = \frac{1600}{220} = 7.273
$$

$$
f = \frac{1005 \times 220\,(7.273 - 1.1445\times2.354)}{0.98\times43\times10^6 - 1005\times220\times7.273}
= \frac{1005\times220\,(4.579)}{4.214\times10^7 - 1.608\times10^6} \approx 0.0249
$$

**Step 4 — turbine (work balance):**

$$
\tau_t = 1 - \frac{1.1445}{7.273}(2.354-1) = 1 - 0.2131 = 0.7869
$$

$$
T_{05} = 1600 \times 0.7869 = 1259\ \mathrm{K}
$$

$$
\pi_t = (0.7869)^{3.5} = 0.4318
$$

**Step 5 — nozzle:**

$$
\frac{p_{05}}{p_0} = 1.604 \times 20 \times 0.4318 = 13.85
$$

$$
M_9^2 = 5\left[(13.85)^{0.2857}-1\right] = 5(2.076-1) = 5.38
\quad\Longrightarrow\quad M_9 = 2.32
$$

$$
T_9 = \frac{1259}{1+0.2(5.38)} = \frac{1259}{2.076} = 606\ \mathrm{K}
$$

$$
u_9 = 2.32\sqrt{1.4\times287\times606} = 2.32 \times 493.5 = 1145\ \mathrm{m/s}
$$

**Step 6 — performance:**

$$
a_0 = \sqrt{1.4\times287\times220}=297\ \mathrm{m/s}, \qquad u_0 = 0.85\times297 = 252\ \mathrm{m/s}
$$

$$
\frac{F}{\dot m_a} = 1145 - 252 = 893\ \mathrm{N\cdot s/kg}
$$

$$
\mathrm{TSFC} = \frac{0.0249}{893} = 2.79\times10^{-5}\ \mathrm{kg/(N\cdot s)}
\approx 0.098\ \mathrm{kg/(N\cdot hr)}
$$

$$
\eta_p = \frac{2(252)}{1145+252} = 0.361
$$

**The punchline:** specific thrust is excellent (893 vs. ~250 for a high-bypass turbofan), but
**propulsive efficiency is only 36%** at M 0.85. Nearly two-thirds of the kinetic energy imparted to
the air is thrown away as residual jet velocity. That single number is why the next lecture exists.

---

## Common pitfalls

- **Forgetting the work balance sets $T_{05}$.** The turbine is *not* free to expand to ambient; it
  extracts exactly the compressor's work and no more.
- **Assuming the turbine expands to $p_0$.** It expands only as far as the work balance requires.
- **Using cold $c_p$, $\gamma$ in the turbine and nozzle.**
- **Dropping $(1+f)$ in the turbine work balance** when precision is wanted.
- **Assuming higher $\pi_c$ always helps.** Specific thrust peaks at $\tau_{c,opt} = \sqrt{\tau_\lambda}/\tau_r$.
- **Confusing optimum-for-thrust with optimum-for-TSFC.** Different, and the TSFC optimum is higher.
- **Assuming the nozzle is perfectly expanded** when the problem specifies a fixed geometry.
- **Forgetting that a choked nozzle has $p_9 > p_0$** and therefore a pressure-thrust term.

---

## Exam checklist

- [ ] Draw the turbojet with all stations and name each component's station pair
- [ ] Define $\tau_r$, $\pi_r$, $\tau_c$, $\pi_c$, $\tau_t$, $\pi_t$, $\tau_\lambda$
- [ ] March the ideal cycle from station 0 to 9 and get specific thrust and TSFC
- [ ] Derive $\tau_t = 1 - (\tau_r/\tau_\lambda)(\tau_c-1)$ from the work balance
- [ ] State $\tau_{c,opt} = \sqrt{\tau_\lambda}/\tau_r$ and interpret both trends
- [ ] Explain why $\pi_{c,opt} \to 1$ at high $M_0$ and what engine that becomes
- [ ] Write real-component corrections for compressor, turbine, inlet, burner
- [ ] Explain what a spool is and why multi-spool improves off-design behavior
- [ ] Explain why turbojets lost civil aviation to turbofans

---

## Links

- Previous: [L07 — Ramjets](L07-ramjets.md)
- Next: [L08b — Turbofans](L08b-turbofans.md) — fixing the propulsive efficiency problem
- Then: [L09 — Engine/Aircraft Performance](L09-engine-aircraft-performance.md)
- Components: [L10](L10-inlets.md), [L11](L11-combustors.md), [L13](L13-nozzles.md), [L14](L14-compressors-1.md), [L19](L19-turbines-1.md)
- Concept: [propulsion-efficiencies](../../concepts/propulsion-efficiencies.md)
- Course hub: [EAS4300](../EAS4300.md)
