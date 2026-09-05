# L22 — Centrifugal Compressors *(or Engine Controls/Test — see banner)*

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 22 · **Date:** Wed 4 Nov 2026
**Book §:** ⚠️ syllabus says **8.7**, but **§8.7 is "Turbine and Compressor Matching."**
Centrifugal compressors are **Chapter 9** — read **9.1–9.2** (pp. 425, 427).

> 📖 **Reconciled 2026-08-25.** Chapter 9 is *The Centrifugal Compressor*: 9.1 Introduction · 9.2 Stage
> Dynamics · 9.3 The Inducer and Impeller · 9.4 The Diffuser · 9.5 Performance Characteristics ·
> 9.6 Stage Design. This page's original content maps onto **9.1–9.4**. Note §8.7 (Turbine and
> Compressor Matching) is genuinely useful material — it's covered on [L21](L21-turbines-3.md).
>
> 🚨 **Updated 2026-09-05 — real evidence this lecture may not be about centrifugal compressors at
> all.** Cross-referenced against lecture slides from a parallel offering (Section 5041, Spring 2026,
> a different instructor — Mr. Marcos): that course's **Lecture 22 is titled "Controls, Test, and
> Analysis"** — engine control systems, starting, throttle response — with **zero centrifugal-compressor
> content**, and that offering has **no separate centrifugal-compressor lecture anywhere** in its
> 24-lecture sequence. This doesn't prove your Fall 2026 syllabus is wrong (different instructors can
> and do split material differently, and yours explicitly names "Centrifugal Compressors" here), but it
> is real evidence the two courses diverge exactly at this point, for the second time (L17 was the
> first — see that page). **§0 below adds the Controls content**, since it's valuable either way and
> doesn't overlap with your syllabus's centrifugal-compressor topic. The original centrifugal-compressor
> material (§1 onward) is kept in full — it's correct book content regardless of which lecture number
> it belongs under. **Ask the instructor which is actually taught in this slot.**
> See [textbook-section-map](textbook-section-map.md).

**Tags:** #centrifugal-compressor #radial #impeller #diffuser #slip-factor #inducer #vaneless-diffuser #specific-speed #radial-turbine #engine-controls #fadec #starting

---

## Why this lecture matters

Centrifugal compressors achieve in **one stage** what an axial machine needs four or five stages to do.
They dominate small engines, turbochargers, and rocket turbopumps. And the reason for their advantage
falls directly out of the three-term Euler equation you already know from
[L14](L14-compressors-1.md) — the centrifugal term that vanishes in axial machines.

---

## Core concepts

### 0. Engine controls, starting, and thrust management (cross-referenced content)

*Cross-referenced against a parallel offering's actual "Controls, Test, and Analysis" lecture. This
material has no overlap with the testing/instrumentation content on [L25](L25-testing-performance-characteristics.md)
— it's specifically about how the engine is *commanded* and *started*, not how it's measured.*

#### The control system

A modern engine control has: **sensors** (rpm, pressure, temperature), **actuators** (hydraulic
pistons for variable vanes and bleed valves), a **processor**, **fuel metering unit**, **fuel/oil
pumps**, **igniters**, a **generator** (electrical power for the aircraft and backup power for the
control itself), a **communication bus** to the cockpit, and **solenoids/air valves** for the
reverser, bleed, and turbine clearance control.

The processor is the **FADEC** — *Full Authority Digital Electronic Control*. "Full authority" means
exactly what it says: the control laws live entirely in the FADEC, with no mechanical backup path in
modern engines, which is why FADEC reliability and redundancy is itself a major certification topic.

#### Ground starts and airstarts

A **ground start** sequence: external air (ground cart, APU, or a running adjacent engine) spins an
air-impulse starter turbine → core rpm rises → pumps and the generator come online → the fuel valve
opens → after the manifolds fill (a few seconds), ignition → the turbine begins producing power → once
the turbine can self-sustain the acceleration to idle, the starter disengages and start bleeds close.
**Burner lighting and adequate compressor stall margin during the light-off transient are the two
things that make or break a start** — directly connecting to the stability-audit transient tip-gap
discussion on [L17 §0](L17-compressors-4.md).

An **airstart** (engine relit in flight after a shutdown) is either **windmill** (forward airspeed
alone spins the fan/LPC fast enough to supply the core and light the burner — works only above a
minimum airspeed) or **starter-assisted** (APU-supplied air drives the starter, used if core rpm has
decayed below the windmill-relight minimum). Rare, but certified across the full flight envelope.

**Worked example — ignition fuel flow.** An 8-can combustor has igniters in only 2 cans, but fuel is
scheduled to all 8. Idle compressor airflow is 25 lbm/s, motoring dilution is 10%, and stoichiometric
fuel-air ratio for Jet-A is $f_{\text{stoich}} = 0.0678$:

$$
\dot m_{\text{motoring}} = 25 \times 0.10 = 2.5\ \mathrm{lbm/s}
\;\Rightarrow\;
\dot m_{\text{per can}} = \frac{2.5}{8} = 0.3125\ \mathrm{lbm/s}
$$

$$
\dot m_{f,\text{per can}} = f_{\text{stoich}} \times \dot m_{\text{per can}} \times 3600 \approx 30.5\ \mathrm{lbm/hr}
\;\Rightarrow\;
\dot m_{f,\text{total}} = 8 \times 30.5 \approx 244\ \mathrm{lbm/hr}
$$

The control schedules a **stoichiometric-per-can** fuel split at light-off regardless of which 2 cans
actually have spark — cross-lighting through interconnect tubes carries the flame to the rest.

#### Thrust control modes

Two main modes for a fixed-nozzle engine: **corrected fan speed** ($N_1/\sqrt\theta$) or **engine
pressure ratio** (EPR $=P_5/P_2$, exit over inlet stagnation pressure). EPR tracks *actual* delivered
thrust better as the engine deteriorates, since it's a direct pressure measurement rather than an rpm
proxy; N1 control is mechanically simpler. Idle is governed separately, by a minimum burner pressure or
minimum corrected core speed floor.

**Thrust ratings** matter commercially: an engine is certified to its highest required rating, but
operators can select a **de-rated** thrust for a lighter load or a shorter-runway mission — and
de-rated operation measurably extends time between overhauls, since it runs at lower TIT
(see [L04 §6](L04-combustion-thermodynamics-2.md) on the TIT/blade-life tradeoff).

#### Transient (acceleration/deceleration) control

Burner airflow isn't directly measurable in flight, so the fuel control uses **combustor pressure as a
proxy for airflow**, scheduling upper and lower limits on $\dot m_f / P_b$ (fuel flow over burner
pressure): the **upper limit protects against compressor stall** during acceleration (too much fuel too
fast spikes $T_4$, exactly the transient-operating-line mechanism from
[L17 §0](L17-compressors-4.md)), and the **lower limit protects against lean blowout** during
deceleration. An engine with reliable starts and a fast, stable throttle response is said to have good
**operability** — the connecting thread between this lecture and L16/L17.

### 1. Why centrifugal machines get so much pressure ratio

Recall the alternative form of Euler's equation from [L14](L14-compressors-1.md) §4:

$$
w = \underbrace{\frac{C_2^2-C_1^2}{2}}_{\text{absolute KE}}
+ \underbrace{\frac{U_2^2-U_1^2}{2}}_{\text{centrifugal}}
+ \underbrace{\frac{W_1^2-W_2^2}{2}}_{\text{relative diffusion}}
$$

**In an axial machine, $U_1 = U_2$ and the middle term vanishes.** All the work must come from
diffusing the relative flow — and that's exactly the term limited by de Haller
([L14](L14-compressors-1.md) §7).

**In a centrifugal machine, $U_2 \gg U_1$** (the flow moves from a small inlet radius to a large exit
radius), so the centrifugal term is large and **free of any diffusion limit.** The fluid is simply
flung outward; there's no boundary layer to separate.

**That's the whole story.** The pressure rise available from $\left(U_2^2-U_1^2\right)/2$ has no
aerodynamic ceiling — only a mechanical (stress) one.

**Result:**

| | Axial stage | Centrifugal stage |
|---|---|---|
| Pressure ratio | 1.2–1.4 | **3–8** (up to 12 in extreme designs) |
| Efficiency | 88–92% | 78–85% |
| Frontal area | Small | **Large** |
| Length | Long (many stages) | Short |
| Mass flow capacity | High | Lower |
| Robustness | Lower | **Higher** (thick blades) |
| Cost | High | **Low** |

### 2. Architecture

```
Inlet → [ Inducer ] → [ Impeller ] → [ Diffuser ] → [ Volute/Scroll ] → Exit
                                     (vaneless or vaned)
```

**Inducer.** The axial-flow inlet portion of the impeller. Its job is to accept axial flow and turn it
toward radial with acceptable incidence. **The inducer tip is where the relative Mach number is
highest**, and it usually sets the machine's limit — the same transonic problem as
[L18](L18-transonic-fan-stage.md).

**Impeller.** The radial portion. Vanes may be:
- **Radial (straight)** — $\beta_2 = 0$, simplest, highest stress capability, most common in aero
- **Backswept** — vanes curved opposite to rotation, $\beta_2 < 0$. Lower work but **wider stable
  operating range** and better efficiency. Standard in turbochargers and modern aero designs.
- **Forward-swept** — high work, but unstable and rarely used

**Splitter vanes** — shorter vanes between the main vanes, starting partway along. They reduce blade
loading in the outer region without adding blockage at the inducer where the passage is already tight.

**Diffuser.** Converts the large exit kinetic energy into static pressure. **This is critical** —
50–70% of the total pressure rise can occur in the diffuser, because the impeller exit velocity is
enormous.

**Volute/scroll.** Collects the flow and delivers it to the next component.

### 3. Slip factor — the correction that always appears

Even with radial vanes ($\beta_2 = 0$), the flow does **not** leave purely radially in the relative
frame. The fluid has inertia and cannot be perfectly guided by a finite number of vanes; a
counter-rotating **relative eddy** forms in each passage, so the exit swirl is less than ideal.

$$
\sigma = \frac{C_{w2,\text{actual}}}{C_{w2,\text{ideal}}} = \frac{C_{w2}}{U_2} \quad (\text{radial vanes})
$$

**Stanitz correlation** (widely used):

$$
\sigma \approx 1 - \frac{0.63\pi}{Z}
$$

**Stodola:**

$$
\sigma \approx 1 - \frac{\pi\sin\beta_2'}{Z}
$$

with $Z$ the number of vanes. Typical $\sigma = 0.85$–0.92.

**Two things students get wrong:**
1. **Slip is not a loss.** It reduces the *work input* (Euler's equation gives less work), but it isn't
   an efficiency term. It's a kinematic effect. Efficiency is a *separate* multiplier.
2. **More vanes ⇒ higher $\sigma$** (better guidance), but also more blockage and friction. There's an
   optimum, typically 16–30 vanes including splitters.

**Work input with slip:**

$$
w = \sigma\, U_2^2 \quad (\text{radial vanes, axial inlet})
$$

Some texts add a **power input factor** $\psi_{\text{pf}} \approx 1.03$–1.05 for disk friction and
recirculation:

$$
w = \psi_{\text{pf}}\,\sigma\, U_2^2
$$

### 4. The diffuser problem

Impeller exit velocity is very high — often $M_2 \approx 0.9$–1.3 in the absolute frame. Diffusing that
efficiently is the hardest part of the machine.

**Vaneless diffuser.**
- An annular space; flow spirals outward conserving angular momentum ($rC_w =$ const) while $C_r$ falls
  by continuity
- **Wide operating range**, tolerant of off-design incidence, simple, cheap
- **But:** long flow path ⇒ high friction loss, and needs a large diameter for a given pressure recovery
- Standard in **turbochargers**, where range matters more than peak efficiency

**Vaned diffuser.**
- Vanes turn and diffuse the flow over a much shorter radial distance
- **Higher peak efficiency**, more compact
- **But:** narrow operating range — off-design incidence on the vanes causes stall
- Standard in **aero engines**, where the operating range is narrower and efficiency is paramount

**Pipe diffuser** — a variant with drilled conical passages rather than sheet-metal vanes. Very high
performance, used on several small aero engines.

**Vaneless space.** Even with a vaned diffuser, a gap (typically 5–15% of impeller radius) is left
before the vanes. It lets the strongly non-uniform impeller exit flow ("jet-wake" structure) mix out
before hitting the vanes, and it decouples the vane pressure field from the impeller (reducing forced
response and noise).

### 5. Where centrifugal machines are used

**Small gas turbines.** Below roughly 5–10 kg/s of airflow, axial blades become so short that tip
clearance and Reynolds effects destroy their efficiency ([L17](L17-compressors-4.md) §5). A centrifugal
stage becomes competitive and then superior.
Examples: helicopter engines (PT6, Arriel), APUs, small turbofans.

**Hybrid (axial-centrifugal) compressors.** Several axial stages followed by a centrifugal final stage —
the axials handle the high inlet flow efficiently, the centrifugal handles the last, high-density
stages where axial blades would be too short. Very common in turboshaft engines.

**Turbochargers.** Almost universally centrifugal — cheap, compact, robust, wide range with a vaneless
diffuser and backswept vanes.

**Rocket turbopumps.** Centrifugal pumps (and radial-inflow turbines) dominate because of the extreme
power density and the need for high pressure rise in minimal length and mass
([L24](L24-rocket-engines-2.md)).

**Historical note:** early jet engines (Whittle's W.1, the Rolls-Royce Derwent/Nene, the GE J31) were
centrifugal — the technology was mature from superchargers. Axials took over for large engines as soon
as the aerodynamics were understood, because the frontal-area penalty of a centrifugal machine is
severe on an aircraft.

### 6. Specific speed — choosing the machine type

The dimensionless parameter that tells you which architecture is right:

$$
N_s = \frac{N\sqrt{\dot V}}{\left(\Delta h_{0s}\right)^{3/4}}
$$

with $N$ in rad/s, $\dot V$ volumetric flow, $\Delta h_{0s}$ isentropic head.

**The Cordier diagram** relates $N_s$ to the optimal machine geometry:

| $N_s$ | Best machine |
|---|---|
| Low (< 0.5) | **Radial/centrifugal** — low flow, high head |
| Medium (0.5–1.5) | Mixed flow |
| High (> 1.5) | **Axial** — high flow, low head |

**Physical reading:** high specific speed means you want lots of flow with modest pressure rise — that's
an axial machine's natural regime. Low specific speed means high pressure rise with little flow —
centrifugal.

This is a genuinely useful first-cut design tool and a likely exam concept question.

### 7. Radial inflow turbines

The mirror image: flow enters radially at the outer radius and exits axially at the center.

- Same advantage: the centrifugal term works *for* you on expansion, giving very high work per stage
- Used in **turbochargers** (universally), small APUs, cryogenic expanders, and rocket turbopumps
- Typical single-stage expansion ratios of 3–5
- **Limitation:** the rotor is a solid, heavy, thick-hubbed piece — hard to cool, so peak temperature is
  limited. That's why they're absent from large aero engines where TIT dominates
  ([L20](L20-turbines-2.md))

---

## Worked logic — a centrifugal compressor stage

**Given:** $D_2 = 0.40$ m (impeller exit diameter), $N = 25{,}000$ rpm, radial vanes,
$Z = 20$ vanes, axial inlet ($C_{w1}=0$), $T_{01}=288$ K, $p_{01}=101.3$ kPa,
$c_p=1005$ J/(kg·K), $\gamma=1.4$, $\eta_c=0.80$, power input factor 1.04.

**Step 1 — impeller tip speed:**

$$
\omega = \frac{2\pi(25{,}000)}{60}=2618\ \mathrm{rad/s}
$$

$$
U_2 = \omega\frac{D_2}{2}=2618(0.20)=523.6\ \mathrm{m/s}
$$

**Note how high this is** — well above any axial compressor blade speed. Centrifugal impellers run
fast, and the stress limit is what caps them (~500–600 m/s for titanium/aluminium).

**Step 2 — slip factor (Stanitz):**

$$
\sigma = 1 - \frac{0.63\pi}{20}=1-\frac{1.979}{20}=1-0.0990=0.901
$$

**Step 3 — work input:**

$$
w = \psi_{\text{pf}}\,\sigma\,U_2^2 = 1.04(0.901)(523.6)^2 = 1.04(0.901)(274{,}157)
$$

$$
w = 256{,}900\ \mathrm{J/kg}
$$

**Step 4 — temperature rise:**

$$
\Delta T_0 = \frac{w}{c_p}=\frac{256{,}900}{1005}=255.6\ \mathrm{K}
$$

$$
T_{03}=288+255.6=543.6\ \mathrm{K}
$$

**255 K in a single stage.** Compare an axial stage's ~30 K ([L14](L14-compressors-1.md)) — this one
stage does the work of roughly **eight axial stages**.

**Step 5 — pressure ratio:**

$$
\pi_c = \left[1+\frac{\eta_c \Delta T_0}{T_{01}}\right]^{\frac{\gamma}{\gamma-1}}
=\left[1+\frac{0.80(255.6)}{288}\right]^{3.5}
$$

$$
=\left[1+0.710\right]^{3.5}=(1.710)^{3.5}
$$

$$
\pi_c = 6.45
$$

**A single-stage pressure ratio of 6.45.** An axial compressor would need about
$\ln(6.45)/\ln(1.35) \approx 6.2$, so **7 stages** to match it.

**Step 6 — the trade.** Efficiency is only 0.80, versus ~0.88–0.90 for a good multistage axial. And the
0.40 m diameter is large for the flow it passes. So:

- **For a helicopter engine** (small flow, tight length and cost budget, frontal area irrelevant):
  centrifugal wins decisively.
- **For a widebody turbofan** (huge flow, frontal area critical, efficiency is everything): axial wins
  decisively.

**Step 7 — check the inducer, which is the real limit.** Suppose the inducer tip radius is
$r_{1t}=0.12$ m and inlet axial velocity $C_{a1}=150$ m/s:

$$
U_{1t}=2618(0.12)=314.2\ \mathrm{m/s}
$$

$$
W_{1t}=\sqrt{150^2+314.2^2}=348.2\ \mathrm{m/s}
$$

$$
T_1 = 288-\frac{150^2}{2(1005)}=276.8\ \mathrm{K}, \qquad a_1 = \sqrt{1.4(287)(276.8)}=333.5\ \mathrm{m/s}
$$

$$
M_{\text{rel},1t}=\frac{348.2}{333.5}=1.04
$$

**Transonic at the inducer tip** — as §2 warned, this is where the design constraint bites, not at the
impeller exit. Increasing $N$ further to get more pressure ratio would push the inducer deeper into
supersonic flow and incur shock losses.

---

## Common pitfalls

- **Treating slip factor as an efficiency.** It's kinematic — it reduces work *input*, not the
  efficiency of converting that work to pressure. Apply both, separately.
- **Forgetting slip entirely.** Using $w = U_2^2$ over-predicts by 10–15%.
- **Assuming radial vanes mean radial exit flow.** Slip means the relative flow leaves with a backward
  tangential component.
- **Ignoring the diffuser.** It contributes the majority of the static pressure rise.
- **Assuming centrifugal is always worse.** Below ~5 kg/s it's genuinely better.
- **Checking only the impeller exit Mach.** The **inducer tip** usually limits the design.
- **Forgetting the frontal-area penalty** when asked why aircraft engines went axial.
- **Applying the de Haller limit to the centrifugal term.** It doesn't constrain the $U_2^2-U_1^2$ work.

---

## Exam checklist

- [ ] **Write the three-term Euler equation and explain why the centrifugal term makes radial machines
      high-pressure-ratio**
- [ ] Compare axial and centrifugal on pressure ratio, efficiency, frontal area, cost, robustness
- [ ] Label the architecture: inducer, impeller, diffuser, volute
- [ ] Compare radial, backswept, and forward-swept vanes
- [ ] **Define slip factor, apply Stanitz, and explain why it is not a loss**
- [ ] Compute $w = \sigma U_2^2$, $\Delta T_0$, and $\pi_c$ for a stage
- [ ] Compare vaneless and vaned diffusers on range vs. efficiency, and say which application uses which
- [ ] Explain the vaneless space's purpose
- [ ] Explain why small engines use centrifugal stages (blade height / Reynolds argument)
- [ ] **Define specific speed and use it to select machine type**
- [ ] Check inducer tip relative Mach number and explain why it's the limiting station
- [ ] Describe radial inflow turbines and their temperature limitation

---

## Links

- Previous: [L21 — Turbines 3](L21-turbines-3.md)
- **Midterm 2 review 6 Nov, exam 9 Nov** → [exam-midterm-2](exam-midterm-2.md)
- Next: [L23 — Rocket Engines 1](L23-rocket-engines-1.md) (after the 11 Nov holiday)
- Euler's equation: [L14 — Compressors 1](L14-compressors-1.md)
- Why small axials fail: [L17 — Compressors 4](L17-compressors-4.md)
- Inducer transonic problem: [L18 — Transonic Fan Stage](L18-transonic-fan-stage.md)
- Turbopump application: [L24 — Rocket Engines 2](L24-rocket-engines-2.md)
- Concept: [velocity-triangles](../../concepts/velocity-triangles.md)
- Course hub: [EAS4300](../EAS4300.md)
