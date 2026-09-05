# L11 — Combustors

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 11 · **Date:** Wed 30 Sep 2026
**Book §:** 6.4 *Gas Turbine Combustors* (p. 242) — ✅ verified
**Tags:** #combustor #primary-zone #dilution #flame-stabilization #swirler #pattern-factor #flame-speed #NOx #relight #residence-time

---

## Why this lecture matters

[L03](L03-combustion-thermodynamics-1.md) and [L04](L04-combustion-thermodynamics-2.md) established
the fundamental tension: **the combustor must run overall lean ($\phi \approx 0.25$) to protect the
turbine, but a $\phi = 0.25$ mixture won't sustain a flame.** This lecture is how hardware resolves
that. It's also where the abstract "$\pi_b = 0.95$" of cycle analysis gets its physical origin.

---

## Core concepts

### 1. The competing requirements

A combustor must simultaneously deliver:

| Requirement | Typical target |
|---|---|
| High combustion efficiency | $\eta_b > 0.99$ at design |
| Low stagnation pressure loss | $\pi_b = 0.94$–0.98 |
| Uniform exit temperature | Low pattern factor |
| Wide stability limits | Idle to full power, all altitudes |
| Reliable altitude relight | Up to ~30,000 ft |
| Low emissions | NOₓ, CO, UHC, smoke |
| Short length, low weight | Every cm of shaft length costs weight |
| Long life | Liner durability at 2,000 K |

**Several of these directly conflict.** Low NOₓ wants low flame temperature and lean burning; stability
and efficiency want near-stoichiometric burning. Short length wants fast mixing; low pressure loss
wants gentle flow. Combustor design is an exercise in managed compromise.

### 2. The zone architecture — how the lean/flammable conflict is resolved

The answer is **staging**: don't burn lean everywhere; burn near-stoichiometric in a small region and
dilute afterwards.

```
Diffuser → [ Primary zone ] → [ Intermediate zone ] → [ Dilution zone ] → Turbine
  M↓        φ ≈ 0.8–1.2          φ ≈ 0.6–0.8            φ ≈ 0.25–0.3
            ~2200 K              burnout                ~1600–1900 K
            ~20% of air          ~20% of air            ~40% of air
                                                        (+ ~20% liner cooling)
```

**Pre-diffuser.** Compressor exit air arrives at $M \approx 0.3$–0.4. That is far too fast — Rayleigh
$p_0$ loss scales roughly with $M^2$ ([L05](L05-gas-dynamics.md) §10), and flame speeds are only a few
m/s. The pre-diffuser slows it to **$M \approx 0.05$–0.1**. This is why combustors are the fattest part
of the engine's flow path.

**Primary zone.** Roughly 20% of the air, mixed with **all** the fuel, giving local $\phi \approx 1$.
Burns at ~2,200 K. This is where flame stabilization happens.

**Intermediate zone.** Additional air completes burnout of CO and unburned hydrocarbons, and lets
dissociated species recombine (recovering some of the energy lost per
[L04](L04-combustion-thermodynamics-2.md) §3).

**Dilution zone.** The remaining air is jetted in through discrete holes to drop the temperature to
what the turbine tolerates and to *tailor the radial profile*.

**Liner cooling.** 20–30% of the air never participates in combustion — it's used as film cooling along
the liner walls, which see 2,000 K gas but are made of alloys good to ~1,150 K.

### 3. Flame stabilization — how you hold a flame in a 50 m/s wind

**The core problem:** laminar flame speed of kerosene-air is roughly **0.4 m/s**; turbulent flame speed
maybe 5–20 m/s. Bulk flow through the combustor is 20–50 m/s. **The flame would simply blow downstream
and out.** Something must anchor it.

**Mechanism: create a recirculation zone** — a region of reversed flow that continuously carries hot
products back upstream to ignite incoming reactants. This is a continuous self-ignition loop, not a
propagating flame front.

**Devices:**
- **Swirler** — the primary method in gas turbines. Vanes impart strong tangential velocity; if the
  swirl number is high enough (S ≳ 0.6) the resulting adverse axial pressure gradient produces
  **vortex breakdown** and a central toroidal recirculation zone. Robust and compact.
- **Bluff body / V-gutter** — a physical obstruction with a wake recirculation. Standard in
  **afterburners** ([L12](L12-afterburners-ramjet-combustors.md)) where a swirler is impractical.
- **Primary jets** — dilution/primary air jets penetrating from the liner also drive recirculation.
- **Step / sudden expansion** — a dump combustor's rearward-facing step, common in ramjets.

### 4. Residence time — the sizing criterion

The flow must stay in the combustor long enough for chemistry to complete:

$$
\tau_{\text{res}} = \frac{V_{\text{comb}}}{\dot{V}} = \frac{\rho V_{\text{comb}}}{\dot{m}}
$$

**Requirement:**

$$
\tau_{\text{res}} > \tau_{\text{chem}} \quad (\text{typically } \tau_{\text{res}} \approx 2\text{–}10\ \mathrm{ms})
$$

**Chemical time scales strongly with pressure and temperature:**

$$
\tau_{\text{chem}} \propto \frac{1}{p^{n}}\exp\left(\frac{E_a}{R_u T}\right), \qquad n \approx 1\text{–}2
$$

**This is why altitude relight is hard.** At 10 km, $p$ and $T$ are low, so $\tau_{chem}$ balloons while
$\tau_{res}$ is unchanged. The combustor can blow out and refuse to relight. **Relight envelopes** are
a certification requirement, and combustors are sized for the worst case (high altitude, windmilling
start) rather than the design point.

**Loading parameter** — the classical correlation grouping these effects:

$$
\Omega = \frac{\dot{m}}{p^{1.8}\,V\,e^{T/300}}
$$

Blowout occurs above a critical $\Omega$. Low $p$ (altitude) and high $\dot m$ push you toward it.

### 5. Stagnation pressure loss — where $\pi_b$ comes from

Two distinct contributions, and you should be able to separate them:

**(a) Cold loss (friction, diffusion, mixing, jet penetration).** Roughly:

$$
\frac{\Delta p_0}{p_0}\bigg|_{\text{cold}} \approx K\, \frac{\tfrac{1}{2}\rho V_{\text{ref}}^2}{p_0}
$$

Dominated by the pressure drop across the liner holes, which is *deliberately* kept at 3–6% of $p_0$ —
that $\Delta p$ is what drives the dilution jets in with enough momentum to penetrate and mix. **It's a
design feature, not purely a loss.**

**(b) Fundamental (Rayleigh) loss from heat addition.** From [L05](L05-gas-dynamics.md) §10, heating a
compressible flow reduces $p_0$ even with zero friction:

$$
\frac{p_{04}}{p_{03}}\bigg|_{\text{Rayleigh}} \approx 1 - \gamma M_3^2\left(\frac{T_{04}}{T_{03}}-1\right)\ \ \text{(small-}M\text{ approximation)}
$$

**Read the $M_3^2$ factor** — it is precisely why the pre-diffuser exists. At $M_3 = 0.05$ this term is
negligible; at $M_3 = 0.3$ it would be crippling.

**Total:**

$$
\pi_b = \frac{p_{04}}{p_{03}} \approx 0.94\text{–}0.98
$$

**Every 1% of $p_0$ lost in the combustor costs roughly 1% of engine thrust.** Combustor pressure loss
is a first-order cycle penalty, not a rounding error.

### 6. Exit temperature distribution

The turbine cares intensely about *how* the temperature is distributed, not just its mean.

**Pattern factor (overall temperature distribution factor)** — for the nozzle guide vanes, which see
the worst local spot:

$$
\mathrm{PF} = \frac{T_{04,\max} - T_{04,\text{avg}}}{T_{04,\text{avg}} - T_{03}}
$$

Target: **PF < 0.25**.

**Profile factor (radial)** — for the rotor blades, which spin and therefore average circumferentially
but not radially:

$$
\mathrm{Profile} = \frac{T_{04,\text{avg-circ},\max} - T_{04,\text{avg}}}{T_{04,\text{avg}} - T_{03}}
$$

**Design intent:** the profile is deliberately shaped **hot in the middle, cool at hub and tip** —
because the blade *root* carries the centrifugal stress and the *tip* runs against the casing with
tight clearance. Both need to be cooler than the midspan. A flat profile would actually be worse than
a shaped one.

### 7. Combustor geometries

| Type | Description | Pros | Cons |
|---|---|---|---|
| **Can** | Multiple separate cylindrical cans, each with its own liner | Easy to test/replace one can | Heavy, poor circumferential uniformity |
| **Annular** | One continuous annulus | Light, short, uniform exit, best $\Delta p$ | Hard to develop; must test the whole thing |
| **Can-annular (cannular)** | Discrete liners inside a common annular casing | Compromise; development ease | Heavier than annular |

**Modern aero engines are essentially all annular** — the weight and length savings dominate. Industrial
gas turbines still use cans because maintainability matters more than weight.

### 8. Emissions — the modern design driver

| Pollutant | Formed when | Reduced by |
|---|---|---|
| **NOₓ** | High flame temperature, long residence (thermal/Zeldovich) | Lower peak $T$, lean burning, shorter residence |
| **CO** | Incomplete oxidation, low $T$, short residence | Higher $T$, longer residence |
| **UHC** | Poor atomization, quenching at walls | Better fuel prep, avoid wall quench |
| **Smoke/soot** | Locally rich zones | Better mixing, leaner primary |

**The central conflict:** NOₓ wants *cooler and shorter*, CO/UHC want *hotter and longer*. There's a
narrow temperature window (~1,700–1,900 K) where both are acceptable, and the design must sit in it
across the whole power range — which is the hard part, since idle and takeoff are radically different.

**Thermal NOₓ (Zeldovich)** has an extreme temperature sensitivity:

$$
\text{NO}_x \propto \exp\left(-\frac{E_a}{R_u T_{\text{flame}}}\right)
$$

Roughly, NOₓ **doubles for every ~40–50 K** of flame temperature rise near 2,000 K. That exponential is
why lean-burn strategies dominate:

- **RQL (Rich-Quench-Lean)** — burn rich (low $T$, low NOₓ, but soot), quench rapidly through
  stoichiometric, then burn lean. The rapid quench is what avoids dwelling at peak-NOₓ temperature.
- **LPP (Lean Premixed Prevaporized)** — premix thoroughly and burn very lean. Excellent NOₓ, but
  vulnerable to **flashback** and **combustion instability**.
- **Staged combustion (TAPS, DAC)** — separate pilot and main burners, so the pilot handles stability
  at idle while the mains run lean at power.

**Combustion instability ("rumble," "screech")** — a thermoacoustic feedback loop where heat release
fluctuation couples to an acoustic mode. **Rayleigh's criterion:** the instability grows if heat release
is in phase with pressure oscillation. Lean-premixed combustors are particularly susceptible because
the flame sits close to the lean blowout limit and responds strongly to equivalence-ratio
perturbations. It can destroy hardware in seconds.

---

## Worked logic — air split and exit temperature

**Given:** $\dot m_a = 50$ kg/s at station 3, $T_{03}=700$ K, $p_{03}=2.0$ MPa,
$f_{\text{overall}}=0.02$, $Q_R=43$ MJ/kg, $\eta_b=0.99$, $c_{p,h}=1150$ J/(kg·K).

**Step 1 — overall exit temperature:**

$$
\dot{m}_f = 0.02 \times 50 = 1.0\ \mathrm{kg/s}
$$

$$
T_{04} = T_{03} + \frac{\dot m_f \eta_b Q_R}{(\dot m_a + \dot m_f)c_{p,h}}
= 700 + \frac{1.0 \times 0.99\times43\times10^6}{51 \times 1150}
$$

$$
T_{04} = 700 + \frac{4.257\times10^7}{58{,}650} = 700 + 726 = 1{,}426\ \mathrm{K}
$$

**Step 2 — overall equivalence ratio.** With $f_{\text{stoich}} \approx 0.068$:

$$
\phi_{\text{overall}} = \frac{0.02}{0.068} = 0.29
$$

**Far below the lean flammability limit** (~$\phi = 0.5$ for kerosene). Confirms §2: a uniformly-mixed
combustor at this $\phi$ would not burn at all.

**Step 3 — primary zone.** Put 20% of the air with all the fuel:

$$
\dot m_{a,\text{prim}} = 0.20\times 50 = 10\ \mathrm{kg/s}
$$

$$
f_{\text{prim}} = \frac{1.0}{10}=0.10
\quad\Longrightarrow\quad
\phi_{\text{prim}} = \frac{0.10}{0.068}=1.47
$$

That's **too rich** — soot and incomplete combustion. Iterate to 30% of the air:

$$
f_{\text{prim}} = \frac{1.0}{15}=0.0667
\quad\Longrightarrow\quad
\phi_{\text{prim}} = 0.98 \quad \checkmark
$$

**Near stoichiometric — flame will anchor and burn stably.** Local flame temperature ~2,300 K.

**Step 4 — the design story.** 30% of the air burns at $\phi \approx 1$ and ~2,300 K; the remaining
70% is split between liner cooling and dilution, bringing the mixed exit to 1,426 K.

**This is the whole lecture in one calculation:** the combustor is a mixing device that *creates* a
locally flammable region inside a globally non-flammable flow, then dilutes the result down to what the
turbine survives.

---

## Common pitfalls

- **Assuming uniform $\phi$ throughout.** The overall value never occurs anywhere physically.
- **Forgetting liner cooling air** in the air-split budget. 20–30% never sees the flame.
- **Ignoring the Rayleigh contribution to $\pi_b$.** It's fundamental, not a friction artifact.
- **Thinking liner pressure drop is purely wasteful.** It drives the dilution jets; without it they
  wouldn't penetrate.
- **Assuming $T_{04}$ is the flame temperature.** $T_{04}$ is the *mixed* value; local primary-zone
  temperature is far higher.
- **Wanting a flat exit profile.** You want it shaped — cool at hub and tip.
- **Missing the NOₓ/CO conflict.** Reducing one usually increases the other.
- **Assuming design-point performance sizes the combustor.** Altitude relight and blowout do.
- **Confusing flame speed with flow speed.** Flames don't propagate upstream against 50 m/s flow —
  recirculation anchors them.

---

## Exam checklist

- [ ] List the (conflicting) combustor requirements and typical values
- [ ] Draw the zone architecture with air splits and equivalence ratios
- [ ] **Explain why the primary zone must be near-stoichiometric while the overall is lean**
- [ ] Explain flame stabilization by recirculation; name three stabilizer devices
- [ ] Define residence time; explain why altitude relight is the hard case
- [ ] Separate the cold and Rayleigh contributions to $\pi_b$; explain the $M_3^2$ dependence
- [ ] Define pattern factor and profile factor; explain the desired radial shape and why
- [ ] Compare can, annular, and can-annular geometries
- [ ] Explain the NOₓ vs. CO trade and describe RQL and LPP
- [ ] State Rayleigh's criterion for combustion instability
- [ ] **Compute an air split to achieve a target primary-zone $\phi$** (worked example above)

---

## Links

- Previous: [L10 — Inlets](L10-inlets.md)
- Next: [L12 — Afterburners & Ramjet Combustors](L12-afterburners-ramjet-combustors.md)
- Theory: [L03](L03-combustion-thermodynamics-1.md), [L04](L04-combustion-thermodynamics-2.md)
- Rayleigh flow: [L05 — Gas Dynamics](L05-gas-dynamics.md)
- What the turbine does with the exit profile: [L20 — Turbines 2](L20-turbines-2.md)
- Course hub: [EAS4300](../EAS4300.md)
