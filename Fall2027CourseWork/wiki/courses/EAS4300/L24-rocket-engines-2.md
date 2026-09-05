# L24 — Rocket Engines 2: Chambers, Nozzles, and Feed Systems

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 24 · **Date:** Mon 16 Nov 2026
**Book §:** Ch. 10 *Performance of Rocket Vehicles* — ✅ verified · **HW9 assigned**

> 📖 **Reconciled 2026-08-25.** ⚠️ Much of this page (thrust chambers, injectors, cooling, power cycles, solid motors) is **Chapters 11–13, which the course does not assign.** Rocket coverage is **Chapter 10 only** — vehicle-level performance. Treat this page as useful background, and prioritize [L23](L23-rocket-engines-1.md) for the final. See [textbook-section-map](textbook-section-map.md).
**Tags:** #thrust-chamber #injector #regenerative-cooling #expansion-ratio #turbopump #staged-combustion #combustion-instability #solid-motor #area-ratio

---

## Why this lecture matters

[L23](L23-rocket-engines-1.md) established *what* performance a rocket needs. This lecture is *how the
hardware delivers it* — and it's where the nozzle theory of [L13](L13-nozzles.md), the combustion
physics of [L11](L11-combustors.md), and the turbomachinery of
[L22](L22-centrifugal-compressors.md) all reappear under far more extreme conditions.

---

## Core concepts

### 1. The thrust chamber

```
Injector → [ Combustion Chamber ] → [ Throat ] → [ Nozzle ] → Exhaust
             p_c, T_c                  A_t          A_e
```

**Design conditions that make this hard:**
- Chamber pressure **5–30 MPa** (50–300 atm)
- Chamber temperature **3,000–3,600 K** — hotter than any turbine
- Heat flux at the throat **up to 160 MW/m²** — among the highest sustained fluxes in engineering
- Residence time **~1–3 ms**

**Characteristic length** — the classical sizing parameter:

$$
L^* = \frac{V_c}{A_t}
$$

$L^*$ sets residence time for a given contraction ratio. Typical values: 0.8–1.5 m for LOX/RP-1,
0.6–1.0 m for LOX/LH₂ (hydrogen burns faster). Too short and combustion is incomplete (low $c^*$); too
long and you add mass and heat load for nothing.

**Contraction ratio** $A_c/A_t \approx 2$–5. Large enough that chamber velocity is low (minimizing
Rayleigh $p_0$ loss per [L05](L05-gas-dynamics.md) §10 — the same argument as the combustor
pre-diffuser in [L11](L11-combustors.md)).

### 2. Injectors

The injector's job is to atomize, mix, and distribute propellants in **milliseconds** — and it largely
determines both $c^*$ efficiency and whether the engine survives.

| Type | Description | Used on |
|---|---|---|
| **Impinging jet** (like-on-like, unlike) | Streams collide, atomizing on impact | F-1, many RP-1 engines |
| **Coaxial shear** | Central LOX post surrounded by annular fuel gas | LH₂ engines (RS-25, RL10) |
| **Coaxial swirl** | Swirled LOX for better atomization | Russian engines (RD-170 family) |
| **Pintle** | A single central movable element | Merlin, Apollo LM descent engine |

**The pintle injector deserves note:** it's inherently **throttleable** (moving the pintle changes the
annular gap) and is remarkably **stability-resistant** — a single injection element can't support the
transverse acoustic coupling that plagues multi-element faceplates. That's why it was chosen for the
lunar module descent engine, where deep throttling and absolute reliability were both required.

**Face cooling.** A fraction of fuel is injected along the chamber wall (**film cooling**) to protect
both the injector face and the chamber wall. It costs $I_{sp}$ (that propellant burns at a locally
fuel-rich, cooler condition) but is often unavoidable.

### 3. Combustion instability — the classic rocket failure mode

Far more violent than the gas turbine version ([L11](L11-combustors.md) §8) because the energy density
is orders of magnitude higher.

| Mode | Frequency | Mechanism |
|---|---|---|
| **Chugging** | 10–400 Hz | Feed-system coupling — chamber pressure oscillation feeds back through the propellant lines |
| **Buzzing** | 400–1,000 Hz | Intermediate; combustion/feed coupling |
| **Screaming/screeching** | 1,000–20,000 Hz | **Transverse acoustic modes** of the chamber. Can destroy an engine in **tens of milliseconds.** |

**Rayleigh's criterion** applies as always: instability grows when heat release is in phase with the
pressure oscillation.

**Fixes:**
- **Acoustic cavities** in the injector face periphery — quarter-wave or Helmholtz resonators tuned to
  the dangerous modes
- **Baffles** — radial and circumferential walls projecting from the injector face, which break up
  transverse modes by physically preventing the acoustic wave from traversing the chamber
- **Injector redesign** — changing element spacing, pattern, or type

**The F-1 engine's development is the canonical case:** roughly **2,000 full-scale tests** and years of
work went into curing its combustion instability, eventually solved with a baffled injector arrived at
largely empirically. Instability remains only partly predictable; it is still the risk that dominates
new engine development schedules.

### 4. Cooling the chamber

At 160 MW/m² at the throat, no material survives passively.

**Regenerative cooling** — the standard for large liquid engines. Fuel (usually) flows through channels
milled into the chamber wall or formed by brazed tubes *before* being injected.

**Two benefits at once:**
1. The wall is cooled
2. The heat is **not lost** — it's carried back into the chamber with the fuel, so it returns to the
   cycle. Thermodynamically nearly free.

Milled-channel copper-alloy liners with electroformed nickel closeouts are typical for high-flux
engines (RS-25); brazed tube-wall construction was used on the F-1 and RL10.

**Other methods:**

| Method | Description | Where used |
|---|---|---|
| **Film cooling** | Fuel injected along the wall | Supplements regen, esp. near the throat |
| **Ablative** | Silica-phenolic liner chars and erodes, carrying heat away | Upper stages, short-duration, low cost |
| **Radiative** | Refractory nozzle extension (niobium, C/C) glows and radiates | Vacuum nozzle extensions only — needs low pressure |
| **Transpiration** | Porous wall | Rare; used on some injector faces |
| **Dump cooling** | Coolant expelled overboard | Rare, wasteful |

**RP-1 coking problem.** Kerosene decomposes and deposits carbon in hot cooling channels, progressively
blocking them. This limits reusability and is a major reason **methane** is preferred for reusable
engines ([L23](L23-rocket-engines-1.md) §7) — it doesn't coke.

### 5. Nozzle design for rockets

Everything from [L13](L13-nozzles.md) applies, but the pressure ratios are extreme (100–1,000+) so the
expansion ratios are enormous.

$$
\epsilon = \frac{A_e}{A_t}
$$

| Application | $\epsilon$ |
|---|---|
| Sea-level first stage | 10–25 |
| Sea-level, high-$p_c$ (RS-25 at liftoff) | ~69 |
| Vacuum upper stage | 80–200 |
| Deep-space, high-$I_{sp}$ (RL10B-2) | ~285 |

**The sea-level constraint is separation**, not optimization. From [L13](L13-nozzles.md) §4, the
Summerfield criterion ($p_e \gtrsim 0.4\,p_a$) caps $\epsilon$ at liftoff. Exceeding it causes
asymmetric separation and destructive side loads.

**Bell (contoured) nozzles.** A conical nozzle wastes thrust to divergence
($\lambda = (1+\cos\alpha)/2$, [L13](L13-nozzles.md) §5). A **Rao thrust-optimized parabolic** contour
turns the flow back toward axial, recovering most of that loss in **60–80% of the length** of an
equivalent 15° cone. Essentially all modern rocket nozzles are bell contours.

**Extendible nozzles.** A deployable extension increases $\epsilon$ after stage separation, giving upper
stages a huge vacuum expansion ratio while fitting in the interstage. The RL10B-2's carbon-carbon
extension deploys to $\epsilon = 285$ — the highest of any flight engine.

**Altitude compensation** (recapping [L13](L13-nozzles.md) §8): the **aerospike** and **dual-bell**
concepts adapt $\epsilon$ to ambient pressure passively. Both are attractive in theory; neither has
flown operationally, largely because staging already solves the problem cheaply.

### 6. Feed systems

Getting propellant into a 20 MPa chamber is itself a major engineering problem.

**Pressure-fed.** Tanks pressurized above chamber pressure by stored gas (helium).
*Pro:* simple, very reliable, no turbomachinery.
*Con:* tanks must withstand full chamber pressure ⇒ **heavy**. Limits $p_c$ to ~2–3 MPa.
*Used on:* spacecraft propulsion, small upper stages, the Apollo service module.

**Pump-fed.** A turbopump raises propellant pressure; the turbine is driven by hot gas.
*Pro:* tanks stay at low pressure (light), $p_c$ can be very high.
*Con:* the turbopump is the most highly-stressed rotating machine ever built.

**Turbopump scale, to appreciate the problem:** the RS-25 (Space Shuttle Main Engine) high-pressure fuel
turbopump produces roughly **51 MW** — comparable to a small power station — from a package about the
size of a car engine, spinning at ~35,000 rpm. It uses **centrifugal pump stages and radial/axial
turbines** exactly as described in [L22](L22-centrifugal-compressors.md), for exactly the reasons given
there: maximum head rise in minimum length and mass.

**Cavitation** is the pump's characteristic failure mode. If local static pressure falls below the
propellant's vapor pressure at the inducer, vapor bubbles form and collapse violently, eroding the
blades and destroying head rise. Prevented by:
- An **inducer** (a low-head axial stage ahead of the main impeller) that raises pressure enough for the
  impeller to work
- Adequate **NPSH** (net positive suction head), maintained by modest tank pressurization

### 7. Power cycles

**How the turbine drive gas is produced** — the defining architectural choice of a liquid engine.

| Cycle | Description | Trade | Examples |
|---|---|---|---|
| **Gas generator (open)** | A small preburner drives the turbine; its exhaust is **dumped overboard** | Simple; **1–3% $I_{sp}$ loss** from dumped propellant | F-1, Merlin, RS-68 |
| **Staged combustion (closed)** | A preburner drives the turbine; **all** its exhaust goes into the main chamber | Highest $I_{sp}$, high $p_c$; extreme turbine inlet pressure and complexity | RS-25, RD-180, Raptor |
| **Expander** | Fuel heated by **regenerative cooling** drives the turbine, then burns | Very clean, reliable, no preburner; **thrust-limited** by available heat | RL10 |
| **Electric pump** | Battery-driven electric motors run the pumps | Simple, no turbine; battery mass grows with burn time | Rutherford (Electron) |

**The expander cycle's limit is elegant and worth understanding:** heat pickup scales with chamber
*surface area* ($\propto r^2$) while thrust scales with throat *area* — but as engines grow, the
surface-to-throat-area ratio falls. So there's a maximum thrust an expander cycle can support (roughly
300–400 kN). It's a genuine scaling law, not an engineering limitation.

**Full-flow staged combustion** (both an oxidizer-rich and a fuel-rich preburner, so *all* propellant
passes through a turbine) is the most efficient and most difficult architecture. SpaceX's **Raptor** is
the first to fly operationally.

### 8. Solid rocket motors

Fundamentally different — no feed system, no injector, no cooling. The propellant grain *is* the
combustion chamber lining.

**Burn rate law (Saint-Robert / Vieille):**

$$
r = a\, p_c^{\,n}
$$

with $n$ the **pressure exponent**, typically 0.2–0.5.

**The stability requirement — a very examinable result.** Combining the burn rate with mass
conservation in the chamber:

$$
p_c \propto \left(\frac{A_b}{A_t}\right)^{\frac{1}{1-n}}
$$

with $A_b$ the burning surface area. **Stability requires $n < 1$:**
- If $n < 1$, a pressure rise increases mass generation less than it increases mass outflow ⇒
  self-correcting
- If $n \ge 1$, a small pressure rise runs away ⇒ **explosion**

**Grain geometry controls the thrust-time curve** through $A_b(t)$:

| Geometry | $A_b$ trend | Thrust |
|---|---|---|
| **End burner** | Constant | Neutral, long, low thrust |
| **Star / internal burning** | Roughly constant (tailored) | Neutral |
| **Circular perforation** | Increases | **Progressive** |
| **Rod and tube / slotted** | Decreases | **Regressive** |

Shuttle SRBs used a tapered 11-point star at the forward end specifically to produce a **thrust dip
through max-Q** — a good example of grain design solving a vehicle-level structural problem.

**The fundamental limitation:** once lit, a solid motor cannot be throttled or shut down (thrust
termination ports can blow the top off, but that's destruction, not control). This is why solids are
used for boosters and missiles but not for anything requiring precision.

---

## Worked logic — sizing a thrust chamber

**Given:** $F = 800$ kN (vacuum), $p_c = 10$ MPa, LOX/RP-1, $T_c = 3{,}600$ K,
$\mathcal M = 23$ kg/kmol, $\gamma = 1.20$, target vacuum $\epsilon = 40$.

**Step 1 — gas constant and $\Gamma$:**

$$
R = \frac{8314}{23}=361.5\ \mathrm{J/(kg\cdot K)}
$$

$$
\Gamma = \sqrt{1.20}\left(\frac{2}{2.20}\right)^{\frac{2.20}{2(0.20)}}=1.0954\,(0.9091)^{5.5}
$$

$$
(0.9091)^{5.5}=e^{5.5\ln 0.9091}=e^{5.5(-0.09531)}=e^{-0.5242}=0.5921
$$

$$
\Gamma = 1.0954\times0.5921=0.6486
$$

**Step 2 — characteristic velocity:**

$$
c^* = \frac{1}{\Gamma}\sqrt{R T_c}=\frac{1}{0.6486}\sqrt{361.5\times3600}=\frac{1}{0.6486}\sqrt{1{,}301{,}400}
$$

$$
c^* = \frac{1140.8}{0.6486}=1{,}759\ \mathrm{m/s}
$$

**Step 3 — exit pressure at $\epsilon = 40$.** Solving the area-ratio relation for $\gamma = 1.20$,
$\epsilon = 40$ gives $M_e \approx 4.0$ and:

$$
\frac{p_c}{p_e}=\left(1+\frac{0.20}{2}(4.0)^2\right)^{\frac{1.20}{0.20}}=(2.6)^{6}=308.9
$$

$$
p_e = \frac{10\times10^6}{308.9}=32{,}374\ \mathrm{Pa} = 32.4\ \mathrm{kPa}
$$

**Step 4 — vacuum thrust coefficient ($p_a = 0$):**

$$
C_{F,\text{ideal}}=\Gamma\sqrt{\frac{2\gamma}{\gamma-1}\left[1-\left(\frac{p_e}{p_c}\right)^{\frac{\gamma-1}{\gamma}}\right]}
$$

$$
\left(\frac{1}{308.9}\right)^{\frac{0.2}{1.2}}=\left(0.003237\right)^{0.1667}=e^{0.1667\ln(0.003237)}=e^{0.1667(-5.732)}=e^{-0.9554}=0.3847
$$

$$
C_{F,\text{ideal}}=0.6486\sqrt{\frac{2.4}{0.2}(1-0.3847)}=0.6486\sqrt{12\times0.6153}=0.6486\sqrt{7.384}
$$

$$
C_{F,\text{ideal}}=0.6486\times2.7174=1.7625
$$

Plus the vacuum pressure term:

$$
\frac{p_e A_e}{p_c A_t}=\frac{32{,}374\times40}{10\times10^6}=0.1295
$$

$$
C_{F,\text{vac}}=1.7625+0.1295=1.892
$$

**Step 5 — throat area and mass flow:**

$$
A_t = \frac{F}{p_c\,C_F}=\frac{800{,}000}{10\times10^6\times1.892}=0.04228\ \mathrm{m^2}
$$

$$
D_t = \sqrt{\frac{4(0.04228)}{\pi}}=0.232\ \mathrm{m}
$$

$$
\dot m_p = \frac{p_c A_t}{c^*}=\frac{10\times10^6\times0.04228}{1759}=240.4\ \mathrm{kg/s}
$$

**Step 6 — specific impulse:**

$$
c = c^*\,C_F = 1759\times1.892=3{,}328\ \mathrm{m/s}
$$

$$
I_{sp}=\frac{3328}{9.81}=339\ \mathrm{s}
$$

**Sanity check:** 339 s vacuum for LOX/RP-1 is exactly right (the Merlin 1D vacuum is ~348 s, the F-1
was ~304 s). ✓

**Step 7 — exit diameter and the sea-level check:**

$$
A_e = 40\times0.04228=1.691\ \mathrm{m^2} \quad\Longrightarrow\quad D_e = 1.468\ \mathrm{m}
$$

At sea level, $p_e = 32.4$ kPa vs. $p_a = 101.3$ kPa:

$$
\frac{p_e}{p_a}=0.32 \quad < 0.4 \ \text{(Summerfield)}
$$

**This nozzle would separate at sea level.** It is a **vacuum-only** design — correct for an upper stage,
unusable on a first stage. A sea-level version would need $\epsilon \approx 15$–20.

**This is the design decision of [L13](L13-nozzles.md) §4 and [L23](L23-rocket-engines-1.md) §5 made
concrete**, and it's why launch vehicles use different nozzles on different stages.

---

## Common pitfalls

- **Forgetting the Summerfield separation limit** when choosing sea-level $\epsilon$.
- **Using the same nozzle for sea level and vacuum.** Different $\epsilon$ required.
- **Confusing $c^*$ (chamber) with $C_F$ (nozzle) with $c$ (product).**
- **Using $\gamma = 1.4$.** Rocket exhaust is 1.15–1.25.
- **Treating regenerative cooling as a loss.** The heat returns to the cycle.
- **Assuming staged combustion is always better.** It's heavier, far more complex, and higher-risk.
- **Forgetting the expander cycle's thrust limit** and its surface-area origin.
- **Getting the solid motor stability condition wrong.** $n < 1$ is stable.
- **Assuming solid motors can be throttled.** They cannot.
- **Neglecting cavitation** when discussing turbopumps.

---

## Exam checklist

- [ ] Sketch a thrust chamber; define $L^*$ and contraction ratio and say what each controls
- [ ] Compare injector types; explain why pintle injectors throttle and resist instability
- [ ] **Name the three instability regimes and their frequencies; describe baffles and acoustic cavities**
- [ ] **Explain regenerative cooling and why the heat is not lost**
- [ ] Compare cooling methods and state where each is used
- [ ] Explain the RP-1 coking problem and the methane advantage
- [ ] **Select $\epsilon$ for sea level vs. vacuum using the Summerfield criterion**
- [ ] Explain bell contours and extendible nozzles
- [ ] Compare pressure-fed and pump-fed; explain the tank-mass argument
- [ ] **Compare gas generator, staged combustion, expander, and electric pump cycles**
- [ ] Explain the expander cycle's thrust limit from surface-area scaling
- [ ] Explain cavitation and the role of the inducer
- [ ] **Write the solid burn rate law and derive the $n<1$ stability requirement**
- [ ] Relate grain geometry to progressive/neutral/regressive thrust
- [ ] **Size a thrust chamber: $c^*$, $C_F$, $A_t$, $\dot m$, $I_{sp}$** (worked example above)

---

## Links

- Previous: [L23 — Rocket Engines 1](L23-rocket-engines-1.md)
- Next: [L25 — Testing and Performance Characteristics](L25-testing-performance-characteristics.md)
- Nozzle theory: [L13 — Nozzles](L13-nozzles.md), [L05 — Gas Dynamics](L05-gas-dynamics.md)
- Turbopump turbomachinery: [L22 — Centrifugal Compressors](L22-centrifugal-compressors.md)
- Combustion instability (gas turbine version): [L11 — Combustors](L11-combustors.md)
- Course hub: [EAS4300](../EAS4300.md)
