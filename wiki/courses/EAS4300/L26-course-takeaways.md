# L26 — Course Takeaways

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 26 · **Date:** Fri 20 Nov 2026
**Book §:** 9.1 *Introduction* · 9.2 *Centrifugal Compressor Stage Dynamics* (pp. 425, 427)

> 📖 **Reconciled 2026-08-25.** The syllabus cites §9.1–9.2, which are the **opening sections of
> Chapter 9, *The Centrifugal Compressor*** — not a synthesis chapter. Together with L22 (also Ch. 9)
> and L25 (§9.5), the last block of the course appears to be **centrifugal compressor material**.
>
> So this "Course Takeaways" page may be the instructor's own synthesis rather than a reading, with
> §9.1–9.2 as leftover centrifugal coverage. **The synthesis below is still the right way to revise
> for a cumulative final** — but if the final leans on Chapter 9, pair it with
> [L22](L22-centrifugal-compressors.md) and [L25 §0](L25-testing-performance-characteristics.md).
> See [textbook-section-map](textbook-section-map.md).
**Tags:** #synthesis #review #big-picture #final-exam-prep #design-trades #course-summary

*(23–27 Nov — Thanksgiving holiday. Final review 30 Nov and 2 Dec. **Final exam Mon 7 Dec, 10 AM–12 PM.**)*

---

## Why this lecture matters

This is the synthesis lecture — and functionally, the start of final exam preparation. The value here
isn't new material; it's seeing that **26 lectures were really about six ideas applied repeatedly.**
If you can reconstruct the course from the six ideas below, you can derive most of what you'd otherwise
memorize.

---

## The six ideas the whole course runs on

### 1. Thrust is a momentum balance on a control volume

Everything from [L01](L01-introduction.md) to [L24](L24-rocket-engines-2.md) is this equation with
different terms retained:

$$
F = \dot m_e u_e - \dot m_a u_a + (p_e-p_a)A_e
$$

- **Air-breathing:** all three terms
- **Rocket:** drop the ram drag term ⇒ thrust independent of flight speed
- **Perfectly expanded:** drop the pressure term
- Ram drag is why air-breathing thrust decays with speed; its absence is why rocket thrust doesn't

### 2. Stagnation properties carry the energy bookkeeping

From [L02](L02-basic-concepts.md), and used in every component analysis since:

| Component | $T_0$ | $p_0$ |
|---|---|---|
| Inlet, nozzle, stator, duct | **constant** | falls (loss) |
| Compressor, fan | rises | rises |
| Combustor, afterburner | rises | falls |
| Turbine | falls | falls |

**Ideal + adiabatic + work-free ⇒ both constant. Real ⇒ $T_0$ constant, $p_0$ falls.**
Loss = stagnation pressure loss. That one sentence characterizes inlets, combustors, and nozzles.

### 3. Compressible flow reverses your intuition

From [L05](L05-gas-dynamics.md):

$$
\frac{dA}{A}=(M^2-1)\frac{dV}{V}
$$

- Converging accelerates subsonic, decelerates supersonic
- $M=1$ only at a throat (or by friction/heat in constant area)
- Choking fixes mass flow independent of back pressure — the basis of corrected parameters *and* of
  component matching
- Supersonic flow can't be warned about what's ahead ⇒ shocks, unique incidence, unstart

### 4. Euler's turbomachinery equation is exact and universal

From [L14](L14-compressors-1.md):

$$
w = U\,\Delta C_w = c_p\,\Delta T_0
$$

Same equation for compressors ([L14](L14-compressors-1.md)–[L18](L18-transonic-fan-stage.md)),
turbines ([L19](L19-turbines-1.md)–[L21](L21-turbines-3.md)), and centrifugal machines
([L22](L22-centrifugal-compressors.md)). Only the **sign** and which term of the three-term form
dominates changes.

**It holds for real machines** — losses affect how much *pressure* you get from the work, not the work
itself.

### 5. The pressure gradient decides what's achievable

**The single most explanatory fact in the course:**

| | Adverse gradient (diffusing) | Favorable gradient (accelerating) |
|---|---|---|
| Components | Inlets, compressors, diffusers | Nozzles, turbines |
| Boundary layer | Wants to separate | Stays attached |
| Turning/diffusion per row | Limited (de Haller ≥ 0.72) | Nearly unlimited (100°+) |
| Stages needed | Many (10–15) | Few (1–2) |
| Efficiency | 88–92% | 90–93% |
| Failure mode | Stall, surge, separation | Thermal, creep |

**This explains:** why compressors have 15 stages and turbines have 2; why nozzles are 98% efficient
and diffusers struggle; why compressors surge and turbines can't; why supersonic inlets are hard and
supersonic nozzles are easy.

### 6. Everything is a trade, and components can't be designed alone

**The recurring conflicts:**

| Want more of... | Costs you... | Seen in |
|---|---|---|
| Specific thrust | Fuel efficiency | [L06](L06-thermodynamics-of-jet-engines.md), [L08b](L08b-turbofans.md) |
| Propulsive efficiency | Engine size and weight | [L08b](L08b-turbofans.md) |
| Turbine inlet temperature | Cooling bleed | [L20](L20-turbines-2.md) |
| Compressor pressure ratio | Weight, stall margin, rear-stage losses | [L08a](L08a-turbojets.md), [L17](L17-compressors-4.md) |
| Inlet pressure recovery | Weight, complexity, unstart risk | [L10](L10-inlets.md) |
| Combustor stability | NOₓ emissions | [L11](L11-combustors.md) |
| Nozzle expansion at altitude | Separation at sea level | [L13](L13-nozzles.md), [L24](L24-rocket-engines-2.md) |
| Rocket $I_{sp}$ | Thrust-to-weight | [L23](L23-rocket-engines-1.md) |

**Coupling examples worth citing in an exam:**
- Lighting the afterburner requires opening $A_8$, or the compressor surges
  ([L12](L12-afterburners-ramjet-combustors.md) ↔ [L16](L16-compressors-3.md))
- Inlet distortion eats compressor surge margin ([L10](L10-inlets.md) ↔ [L16](L16-compressors-3.md))
- The choked turbine NGV sets the compressor operating line
  ([L21](L21-turbines-3.md) ↔ [L16](L16-compressors-3.md))
- Combustor exit profile is shaped for turbine blade stress
  ([L11](L11-combustors.md) ↔ [L20](L20-turbines-2.md))
- Ramjet heat addition can unstart the inlet ([L07](L07-ramjets.md) ↔ [L10](L10-inlets.md))

---

## The engine family tree, revisited

The course's organizing continuum, ordered by design flight Mach number:

```
Turboprop → High-bypass turbofan → Low-bypass turbofan → Turbojet → Ramjet → Scramjet
   M<0.6         M 0.7-0.9              M 1-2            M 2-3      M 3-5     M>5
   
   ←──────── more turbomachinery          less turbomachinery ────────→
   ←──────── higher propulsive efficiency   higher specific thrust ────→
```

**The unifying principle:** as flight Mach rises, ram compression does more of the work, so you need
less machinery. At $M\approx 3$–4 the compressor's optimum pressure ratio approaches 1 and the turbojet
*becomes* a ramjet ([L08a](L08a-turbojets.md) §4). At $M \approx 6$ ram temperature reaches the material
limit and the ramjet must become a scramjet ([L07](L07-ramjets.md) §3).

**Rockets sit outside the tree** because they carry their oxidizer — which is why they work in vacuum,
have no ram drag, and have $I_{sp}$ an order of magnitude lower.

---

## Master equation sheet

### Thrust and performance

$$
F = \dot m_a\left[(1+f)u_e - u_a\right]+(p_e-p_a)A_e
$$

$$
\eta_p = \frac{2}{1+u_e/u_a}, \qquad \eta_{th}=\frac{\tfrac12\dot m_a[(1+f)u_e^2-u_a^2]}{\dot m_f Q_R},
\qquad \eta_o = \eta_{th}\eta_p
$$

$$
\mathrm{TSFC}=\frac{\dot m_f}{F}=\frac{u_a}{\eta_o Q_R}, \qquad I_{sp}=\frac{F}{\dot m_p g_0}
$$

$$
R = \frac{u}{g_0\mathrm{TSFC}}\left(\frac{L}{D}\right)\ln\frac{W_i}{W_f} \qquad \text{(Breguet)}
$$

### Cycle parameters

$$
\tau_r = 1+\frac{\gamma-1}{2}M_0^2, \qquad \pi_r = \tau_r^{\frac{\gamma}{\gamma-1}}, \qquad
\tau_\lambda = \frac{T_{04}}{T_0}
$$

$$
\tau_t = 1 - \frac{\tau_r}{\tau_\lambda}\left[(\tau_c-1)+\alpha(\tau_f-1)\right]
$$

$$
\tau_{c,\text{opt}}=\frac{\sqrt{\tau_\lambda}}{\tau_r}, \qquad
\eta_{th,\text{ideal}}=1-\frac{1}{r_p^{(\gamma-1)/\gamma}}
$$

$$
f = \frac{c_{p,h}T_{04}-c_{p,c}T_{03}}{\eta_b Q_R - c_{p,h}T_{04}}
$$

### Gas dynamics

$$
\frac{T_0}{T}=1+\frac{\gamma-1}{2}M^2, \qquad
\frac{p_0}{p}=\left(1+\frac{\gamma-1}{2}M^2\right)^{\frac{\gamma}{\gamma-1}}
$$

$$
\frac{dA}{A}=(M^2-1)\frac{dV}{V}, \qquad
\frac{A}{A^*}=\frac{1}{M}\left[\frac{2}{\gamma+1}\left(1+\frac{\gamma-1}{2}M^2\right)\right]^{\frac{\gamma+1}{2(\gamma-1)}}
$$

$$
\dot m = \frac{p_0 A^*}{\sqrt{T_0}}\sqrt{\frac{\gamma}{R}}\left(\frac{2}{\gamma+1}\right)^{\frac{\gamma+1}{2(\gamma-1)}}
$$

$$
M_2^2 = \frac{1+\frac{\gamma-1}{2}M_1^2}{\gamma M_1^2-\frac{\gamma-1}{2}}, \qquad
M_{n1}=M_1\sin\beta
$$

### Turbomachinery

$$
w = U\Delta C_w = c_p\Delta T_0, \qquad
w = \frac{C_2^2-C_1^2}{2}+\frac{U_2^2-U_1^2}{2}+\frac{W_1^2-W_2^2}{2}
$$

$$
R_{\text{comp}}=1-\frac{C_{w1}+C_{w2}}{2U}, \qquad
R_{\text{turb}}=\frac{C_a}{2U}\left(\tan\beta_2-\tan\beta_1\right)
$$

$$
\phi = \frac{C_a}{U}, \qquad \psi = \frac{\Delta C_w}{U}, \qquad \mathrm{DH}=\frac{W_2}{W_1}\ge0.72
$$

$$
\tau_c = \pi_c^{\frac{\gamma-1}{\gamma\eta_{p,c}}}, \qquad
\Delta T_0 = \frac{\lambda U\Delta C_w}{c_p} \ \text{(work-done factor)}
$$

$$
\dot m_{\text{corr}}=\frac{\dot m\sqrt\theta}{\delta}, \qquad N_{\text{corr}}=\frac{N}{\sqrt\theta}
$$

### Rockets

$$
F = \dot m_p c, \qquad c = c^*C_F, \qquad I_{sp}=\frac{c}{g_0}, \qquad c\propto\sqrt{\frac{T_c}{\mathcal M}}
$$

$$
c^*=\frac{p_c A_t}{\dot m_p}, \qquad C_F = \frac{F}{p_c A_t}
$$

$$
\Delta V = c\ln\frac{m_0}{m_f} \qquad \text{(Tsiolkovsky)}
$$

$$
r = a\,p_c^{\,n}, \qquad n<1 \ \text{for stability}
$$

---

## Numbers worth carrying into the exam

| Quantity | Value |
|---|---|
| $R_{\text{air}}$ | 287 J/(kg·K) |
| $c_p$ cold / hot | 1005 / ~1150 J/(kg·K) |
| $\gamma$ cold / hot | 1.4 / ~1.33 |
| $g_0$ | 9.80665 m/s² |
| Jet-A LHV $Q_R$ | ~43 MJ/kg |
| $f_{\text{stoich}}$ (kerosene) | ~0.068, $(A/F)\approx14.7$ |
| Typical cruise $f$ | 0.02–0.025 ⇒ $\phi\approx0.3$ |
| $p^*/p_0$ at $M=1$ ($\gamma=1.4$) | **0.528** |
| $T^*/T_0$ at $M=1$ | 0.833 |
| Choking pressure ratio | 1.89 ($\gamma$=1.4), 1.85 ($\gamma$=1.33) |
| Normal shock $p_{02}/p_{01}$ at $M=2$ / $M=3$ | 0.72 / 0.33 |
| Compressor stage $\Delta T_0$ / $\pi$ | 25–35 K / 1.3–1.4 |
| Turbine stage $\Delta T_0$ | 150–300 K |
| Centrifugal stage $\pi$ | 3–8 |
| Modern TIT | 1,700–2,000 K |
| Cooling bleed | 15–25% |
| Combustor $\pi_b$ / $\eta_b$ | 0.94–0.98 / ~0.99 |
| Nozzle $\eta_n$ | 0.97–0.99 |
| Surge margin requirement | 15–25% |
| de Haller limit | $W_2/W_1 \ge 0.72$ |
| Blade life rule | +15 K ⇒ half life |
| LEO $\Delta V$ | ~9,400 m/s |

---

## Suggested final-exam study sequence

The final is **cumulative** (30% of the grade, 2 hours — twice the length of a midterm, so expect
longer multi-part problems). Suggested order:

1. **[L06](L06-thermodynamics-of-jet-engines.md) first.** Station numbering and the three efficiencies
   are the connective tissue; everything else hangs off them.
2. **[L05](L05-gas-dynamics.md)** — the most-reused toolkit. Redo the summary table from memory.
3. **Cycle march: [L07](L07-ramjets.md) → [L08a](L08a-turbojets.md) → [L08b](L08b-turbofans.md).**
   Practice the station-by-station march until it's automatic.
4. **[L14](L14-compressors-1.md) → [L19](L19-turbines-1.md).** Velocity triangles both ways. Draw them;
   don't just read them.
5. **Matching: [L16](L16-compressors-3.md) + [L21](L21-turbines-3.md).** These two are one topic.
6. **Rockets: [L23](L23-rocket-engines-1.md) + [L24](L24-rocket-engines-2.md).** Self-contained, high
   yield, likely underprepared by most of the class since it comes after Midterm 2.
7. **Components ([L10](L10-inlets.md)–[L13](L13-nozzles.md)) and cooling
   ([L20](L20-turbines-2.md))** — mostly conceptual; good for short-answer marks.
8. **[L25](L25-testing-performance-characteristics.md)** — small but distinctive; easy marks if the
   others skip it.

**Highest-value derivations to have at your fingertips:**
- Thrust equation from a CV momentum balance ([L02](L02-basic-concepts.md))
- Froude propulsive efficiency ([L06](L06-thermodynamics-of-jet-engines.md))
- $dA/A = (M^2-1)dV/V$ ([L05](L05-gas-dynamics.md))
- Euler's turbomachinery equation ([L14](L14-compressors-1.md))
- Degree of reaction ([L15](L15-compressors-2.md))
- Breguet range equation ([L09](L09-engine-aircraft-performance.md))
- Tsiolkovsky rocket equation ([L23](L23-rocket-engines-1.md))
- $p_{02}\le p_{01}$ for adiabatic work-free flow ([L02](L02-basic-concepts.md))

---

## Links

- Previous: [L25 — Testing and Performance Characteristics](L25-testing-performance-characteristics.md)
- **Final exam prep** → [exam-final](exam-final.md)
- Midterm scope pages: [exam-midterm-1](exam-midterm-1.md), [exam-midterm-2](exam-midterm-2.md)
- Concept pages: [station-numbering](../../concepts/station-numbering.md) ·
  [stagnation-properties](../../concepts/stagnation-properties.md) ·
  [propulsion-efficiencies](../../concepts/propulsion-efficiencies.md) ·
  [velocity-triangles](../../concepts/velocity-triangles.md) ·
  [corrected-parameters](../../concepts/corrected-parameters.md)
- Course hub: [EAS4300](../EAS4300.md)
