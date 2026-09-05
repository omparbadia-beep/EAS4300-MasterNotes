# L07 — Ramjets

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 7 · **Date:** Mon 14 Sep 2026
**Book §:** 5.3 *The Ramjet* (p. 155) — ✅ verified · **HW2 assigned**
**Tags:** #ramjet #scramjet #ram-compression #no-turbomachinery #thermal-choking #cycle-analysis #supersonic

---

## Why this lecture matters

The ramjet is the **simplest complete engine** — an inlet, a burner, and a nozzle, with no moving
parts. That makes it the ideal first full cycle analysis: you get the whole method with none of the
turbomachinery bookkeeping. It also isolates one idea cleanly: **all compression comes from flight
speed alone**, which lets you see exactly what ram compression can and cannot buy you.

---

## Core concepts

### 1. Architecture and stations

```
Free stream → [ Inlet/Diffuser ] → [ Combustor ] → [ Nozzle ] → Exhaust
     0                 0→2              3→4           7→9
```

For a ramjet, stations 2, 3 and 4, 7 collapse (no compressor, no turbine), so the practical set is:

| Station | Meaning |
|---|---|
| **0** | Free stream, flight Mach $M_0$ |
| **2 (=3)** | Diffuser exit / burner entry — subsonic, $M \approx 0.2$–0.3 |
| **4 (=7)** | Burner exit / nozzle entry — this is the max-temperature point |
| **9** | Nozzle exit |

**No shaft, no work extraction.** Everything follows from that.

### 2. Ram compression — the whole idea

The inlet decelerates the incoming supersonic flow, converting kinetic energy into pressure. From
[L05](L05-gas-dynamics.md), the **ram pressure ratio** is just the isentropic stagnation relation:

$$
\frac{p_{02}}{p_0} = \eta_r\left(1 + \frac{\gamma-1}{2}M_0^2\right)^{\frac{\gamma}{\gamma-1}}
$$

where $\eta_r = \pi_d$ is the inlet stagnation pressure recovery (< 1 because of shocks and friction).

**Ideal ram pressure ratio vs. flight Mach ($\gamma=1.4$, isentropic):**

| $M_0$ | $p_{02}/p_0$ | Comment |
|---|---|---|
| 0.5 | 1.19 | Useless — no cycle |
| 1.0 | 1.89 | Still poor |
| 2.0 | 7.8 | Comparable to a modest compressor |
| 3.0 | 36.7 | Excellent — this is ramjet territory |
| 4.0 | 152 | Enormous, but recovery $\eta_r$ collapses |
| 5.0 | 529 | Temperature becomes the limit, not pressure |

**Two conclusions define the ramjet's flight envelope:**

- **Below $M_0 \approx 2$, ram compression is too weak** to make a worthwhile cycle. And at $M_0 = 0$,
  $p_{02}/p_0 = 1$ — no pressure rise, no cycle, **zero thrust**. A ramjet cannot self-start; it must be
  boosted (by a rocket, a turbojet, or a launch aircraft) to ~M 0.5–2 before it produces net thrust.
  This is *the* defining ramjet limitation.
- **Above $M_0 \approx 5$, the stagnation temperature itself becomes the problem.** Not the pressure.

### 3. The high-Mach temperature wall

Stagnation temperature after ram deceleration:

$$
T_{02} = T_0\left(1 + \frac{\gamma-1}{2}M_0^2\right)
$$

At $T_0 = 220$ K (stratosphere):

| $M_0$ | $T_{02}$ |
|---|---|
| 2 | 396 K |
| 3 | 616 K |
| 4 | 924 K |
| 5 | 1,320 K |
| 6 | 1,804 K |
| 8 | 2,992 K |

**At $M_0 \approx 6$ the air arrives at the burner already near the turbine-limit temperatures of
[L04](L04-combustion-thermodynamics-2.md) — before any fuel is added.** Since thrust depends on the
*ratio* $T_{04}/T_{02}$, and $T_{04}$ is capped by materials, the available temperature rise shrinks
toward zero. Beyond that, adding fuel just dissociates the products without producing useful
expansion.

**This is precisely why the scramjet exists.** Instead of decelerating to subsonic (which converts *all*
the kinetic energy to heat), a scramjet decelerates only partially and burns in supersonic flow,
keeping much of the energy as directed motion. The engineering cost is severe — fuel must mix and burn
in roughly a millisecond of residence time.

### 4. Ideal ramjet cycle analysis

**Assumptions:** isentropic inlet and nozzle, constant-pressure burner, perfectly expanded nozzle
($p_9 = p_0$), and $f \ll 1$.

The chain is short because there is no work:

$$
T_{02} = T_0\left(1+\frac{\gamma-1}{2}M_0^2\right), \qquad
p_{02} = p_0\left(1+\frac{\gamma-1}{2}M_0^2\right)^{\frac{\gamma}{\gamma-1}}
$$

Burner: $T_{04}$ is set by the fuel-air ratio (or by the material limit). Ideal burner has
$p_{04}=p_{02}$.

Since there's no turbine, all of $p_{04}$ goes to the nozzle. With $p_9 = p_0$ and an isentropic
nozzle, the exit Mach comes out equal to the flight Mach:

$$
M_9 = M_0 \qquad \text{(ideal ramjet, perfectly expanded)}
$$

That elegant result holds because the pressure ratio available to the nozzle is exactly the ram
pressure ratio built by the inlet. Then:

$$
\frac{u_9}{u_0} = \frac{M_9\sqrt{\gamma R T_9}}{M_0 \sqrt{\gamma R T_0}} = \sqrt{\frac{T_9}{T_0}}
= \sqrt{\frac{T_{04}}{T_{02}}}
$$

Defining the **cycle temperature ratio**:

$$
\tau_\lambda = \frac{T_{04}}{T_0}, \qquad
\tau_r = \frac{T_{02}}{T_0} = 1 + \frac{\gamma-1}{2}M_0^2
$$

**Specific thrust:**

$$
\frac{F}{\dot{m}_a} = u_0\left(\frac{u_9}{u_0} - 1\right)
= a_0 M_0\left(\sqrt{\frac{\tau_\lambda}{\tau_r}} - 1\right)
$$

**Fuel-air ratio** from the burner energy balance ([L03](L03-combustion-thermodynamics-1.md)):

$$
f = \frac{c_p T_0\left(\tau_\lambda - \tau_r\right)}{\eta_b Q_R - c_p T_0 \tau_\lambda}
$$

**Thermal efficiency of the ideal ramjet** — remarkably clean:

$$
\eta_{th} = 1 - \frac{1}{\tau_r} = 1 - \frac{1}{1+\frac{\gamma-1}{2}M_0^2}
$$

**Compare to the ideal Brayton result $\eta_{th} = 1 - 1/r_p^{(\gamma-1)/\gamma}$ from
[L06](L06-thermodynamics-of-jet-engines.md).** They are the *same formula* — the ramjet's "compressor"
is simply the ram process, and $\tau_r$ plays the role of the compressor temperature ratio. The ramjet
is a Brayton cycle whose compression is free but speed-dependent.

### 5. The characteristic thrust curve

Plot specific thrust against $M_0$ and you get the ramjet's signature shape:

$$
\frac{F}{\dot{m}_a} = a_0 M_0\left(\sqrt{\frac{\tau_\lambda}{\tau_r}}-1\right)
$$

- **$M_0 = 0$:** $\tau_r = 1$, but the leading $M_0$ factor is zero ⇒ **$F = 0$**. No static thrust.
- **Rising $M_0$:** the $M_0$ factor grows fast, dominating ⇒ thrust rises steeply.
- **Peak** typically around **$M_0 \approx 3$** for a fixed $T_{04}$.
- **High $M_0$:** $\tau_r$ approaches $\tau_\lambda$, the bracket $\to 0$ ⇒ thrust collapses.
- **Cutoff:** when $\tau_r = \tau_\lambda$, i.e. $T_{02} = T_{04}$ — **no temperature rise is possible and
  thrust is exactly zero.** That defines the ramjet's absolute maximum Mach number for a given material
  limit.

**Learn this curve as a shape, not a formula.** "Zero at zero, peak near 3, zero when ram temperature
reaches the material limit" is the answer to most conceptual ramjet questions.

### 6. Thermal choking — the ramjet's other hard limit

From Rayleigh flow ([L05](L05-gas-dynamics.md) §10): a constant-area duct accepts only a **finite**
amount of heat before reaching $M=1$. Adding more heat doesn't raise $T_{04}$; it **reduces the mass
flow** the engine can swallow and can unstart the inlet.

Two consequences for design:
- Burner entry Mach is kept low ($M \approx 0.2$) so there's Rayleigh margin
- Combustors are often mildly **diverging** in area to relieve the choking constraint

This is a genuine physical limit on ramjet performance, not merely a design preference.

### 7. Inlet unstart — the failure mode

Supersonic inlets ([L10](L10-inlets.md)) rely on a carefully positioned shock system. If back pressure
rises too far — too much fuel, thermal choking, or an angle-of-attack excursion — the terminal shock
is **expelled forward** out of the inlet. Mass flow drops abruptly, thrust collapses, and large
asymmetric loads appear. Recovery requires reducing fuel and often descending/accelerating.

Unstart is the dominant operational hazard of ramjet and scramjet vehicles, and it directly couples
combustor behavior (this lecture) to inlet behavior (L10). They cannot be designed independently.

### 8. Where ramjets are actually used

- **Missiles** — boosted to speed by a rocket stage, then ramjet cruise (e.g. integral rocket-ramjet
  designs). This is the dominant real application.
- **The SR-71's J58** — a *turbo-ramjet* hybrid. At high Mach, bypass doors routed most airflow around
  the core directly to the afterburner, so the engine progressively behaved like a ramjet. At Mach 3.2
  the majority of thrust came from the inlet/ejector system, not the turbomachinery — a vivid
  demonstration of §2's argument that ram compression displaces machinery as Mach rises.
- **Scramjet demonstrators** — X-43A (M ≈ 9.6), X-51A (M ≈ 5, ~200 s burn).

---

## Worked logic — ramjet at M 3

**Given:** $M_0 = 3$, $T_0 = 220$ K, $\gamma = 1.4$, $c_p = 1005$ J/(kg·K), $T_{04} = 2000$ K,
$Q_R = 43$ MJ/kg, ideal components.

**Step 1 — ram conditions:**

$$
\tau_r = 1 + 0.2(3)^2 = 2.8
\quad\Longrightarrow\quad
T_{02} = 220 \times 2.8 = 616\ \mathrm{K}
$$

$$
\frac{p_{02}}{p_0} = (2.8)^{3.5} = 36.7
$$

**Step 2 — cycle temperature ratio:**

$$
\tau_\lambda = \frac{2000}{220} = 9.09
$$

**Step 3 — velocity ratio and specific thrust:**

$$
\frac{u_9}{u_0} = \sqrt{\frac{9.09}{2.8}} = \sqrt{3.25} = 1.80
$$

$$
a_0 = \sqrt{1.4 \times 287 \times 220} = 297\ \mathrm{m/s}, \qquad u_0 = 3 \times 297 = 892\ \mathrm{m/s}
$$

$$
\frac{F}{\dot{m}_a} = 892\,(1.80 - 1) = 714\ \mathrm{N\cdot s/kg}
$$

**Step 4 — fuel-air ratio:**

$$
f = \frac{1005 \times 220\,(9.09-2.8)}{0.98\times43\times10^6 - 1005\times220\times9.09}
= \frac{1.391\times10^6}{4.214\times10^7 - 2.01\times10^6} \approx 0.0346
$$

**Step 5 — efficiencies:**

$$
\eta_{th} = 1 - \frac{1}{2.8} = 0.643
$$

$$
\eta_p = \frac{2}{1+1.80} = 0.714
\quad\Longrightarrow\quad
\eta_o = 0.643 \times 0.714 = 0.459
$$

$$
I_{sp} = \frac{F/\dot m_a}{f\, g_0} = \frac{714}{0.0346 \times 9.81} \approx 2{,}100\ \mathrm{s}
$$

**Sanity check:** ~2,100 s is right for a ramjet at M 3 — well above any rocket (§L01) and below a
subsonic turbofan. The 64% thermal efficiency looks spectacular but is only achievable *because* the
vehicle is already at M 3; the boost stage that got it there paid the bill.

---

## Worked logic — M 4 ramjet nozzle area ratio (ties together L05, L07, L13)

*Cross-referenced from a parallel offering's worked example — a genuinely integrated problem that
uses Rayleigh flow ([L05](L05-gas-dynamics.md) §10), the ramjet cycle (this page), and nozzle area
ratios ([L13](L13-nozzles.md)) in a single calculation.*

**Given:** $M_a=4$, $T_a=-58°\mathrm F=402°\mathrm R$, $P_a=1.68$ psia, inlet recovery loss 5%, burner
entrance $M_2=0.3$, burner-inlet $\gamma=1.4$, burner-exit $\gamma=1.3$, $T_4=3{,}970°\mathrm F=4{,}430°\mathrm R$.

**Step 1 — stagnation conditions behind the inlet:**

$$
T_0 = T_a\left(1+\frac{\gamma-1}{2}M_a^2\right) = 402\left(1+0.2\times16\right) = 1{,}687°\mathrm R
$$

$$
P_0 = P_a\left(1+0.2M_a^2\right)^{3.5} = 1.68\times(1+3.2)^{3.5} = 255.1\ \mathrm{psia}
$$

Apply the 5% inlet recovery loss: $P_2 = P_0(1-0.05)=242.3$ psia, $T_2=T_0=1{,}687°\mathrm R$ (adiabatic
inlet — $T_0$ survives, $p_0$ doesn't, exactly [L02](L02-basic-concepts.md)'s rule).

**Step 2 — Rayleigh flow across the burner**, using $T_4/T_2 = 4{,}430/1{,}687 = 2.626$ and reading the
Rayleigh curve at the *entrance* $M_2=0.3$ to get $T_2/T_2^* = 0.31$:

$$
\frac{T_4}{T_4^*} = \frac{T_4}{T_2}\times\frac{T_2}{T_2^*} = 2.626\times0.31 = 0.814
$$

Reading the Rayleigh curve **backwards** at $T_4/T_4^*=0.814$ gives the burner-exit Mach number
$M_4=0.61$ — heat addition has driven the flow toward $M=1$ exactly as
[L05 §10](L05-gas-dynamics.md#10-rayleigh-flow--frictionless-flow-with-heat-addition) predicts, but
not all the way (a ramjet burner is not thermally choked at this condition).

**Step 3 — Rayleigh pressure ratio and burner loss:**

$$
\frac{P_4}{P_4^*} = 1.07, \qquad \frac{P_2}{P_2^*} = 1.191
\;\Rightarrow\;
\frac{P_4}{P_2} = \frac{P_4/P_4^*}{P_2/P_2^*} = \frac{1.07}{1.191} = 0.899
$$

**A 10.1% stagnation pressure loss across the burner** — purely from heat addition, with zero friction
assumed. This is the Rayleigh loss from [L05 §10](L05-gas-dynamics.md) made concrete: $P_4 = 0.899
\times 242.3 = 217.8$ psia.

**Step 4 — the converging (subsonic) nozzle area ratio**, at $M_4=0.61$, $\gamma=1.3$:

$$
\frac{A_4}{A_4^*} = \frac{1}{M_4}\left[\frac{2}{\gamma+1}\left(1+\frac{\gamma-1}{2}M_4^2\right)\right]^{\frac{\gamma+1}{2(\gamma-1)}} = 1.181
$$

**Step 5 — isentropic supersonic expansion downstream**, exiting to ambient
($P_6=P_5=P_4/P_a=217.8/1.68=129.6$):

$$
\frac{P_6}{P_a}=\left(1+\frac{\gamma-1}{2}M_6^2\right)^{\gamma/(\gamma-1)} = 129.6
\;\Rightarrow\; M_6 = 3.72
$$

$$
\frac{A_6}{A_6^*} = \frac{1}{M_6}\left[\frac{2}{\gamma+1}\left(1+\frac{\gamma-1}{2}M_6^2\right)\right]^{\frac{\gamma+1}{2(\gamma-1)}} = 11.64
$$

**The overall divergent area ratio is ~11.6** — a large, genuinely supersonic nozzle, consistent with
expanding from $M=0.61$ at the throat to $M=3.72$ at exit. **The pattern to keep**: a full ramjet
nozzle problem chains *three* distinct relations — Rayleigh flow across the heat-addition section,
then isentropic area-Mach relations on *both* sides of the throat — and mixing up which relation
applies where (Rayleigh only applies where heat is being added; isentropic area-Mach only applies
downstream, where the flow is adiabatic) is the single most common error.

---

## Common pitfalls

- **Claiming a ramjet produces static thrust.** It produces exactly zero at $M_0 = 0$. Always.
- **Forgetting the high-Mach cutoff.** Thrust hits zero again when $T_{02} \to T_{04}$.
- **Using $\gamma = 1.4$ through the burner and nozzle.** Hot section is ~1.33.
- **Ignoring inlet recovery $\eta_r$.** At M 3 a poor inlet can halve $p_{02}$, and thrust with it.
- **Treating the ramjet as unrelated to Brayton.** It *is* a Brayton cycle; the compressor is the
  atmosphere.
- **Neglecting thermal choking** when asked for maximum heat addition.
- **Assuming $M_9 = M_0$ always.** That's the ideal, perfectly-expanded result only.
- **Confusing ramjet with scramjet.** Ramjet: subsonic combustion after full deceleration.
  Scramjet: supersonic combustion, partial deceleration.

---

## Exam checklist

- [ ] Draw the ramjet schematic with stations and explain why 2=3 and 4=7
- [ ] Derive $\tau_r$ and the ram pressure ratio; evaluate at a given $M_0$
- [ ] Explain why static thrust is zero and what that implies operationally
- [ ] Derive $M_9 = M_0$ for the ideal perfectly-expanded ramjet
- [ ] Write specific thrust in terms of $\tau_\lambda$, $\tau_r$, $a_0$, $M_0$
- [ ] Show $\eta_{th} = 1 - 1/\tau_r$ and connect it to ideal Brayton
- [ ] Sketch specific thrust vs. $M_0$ and explain both zeros and the peak
- [ ] Explain the high-Mach temperature limit and why scramjets follow from it
- [ ] Explain thermal choking and inlet unstart, and how they couple

---

## Links

- Previous: [L06 — Thermodynamics of Jet Engines](L06-thermodynamics-of-jet-engines.md)
- Next: [L08a — Turbojets](L08a-turbojets.md) — add a compressor and turbine to fix the static-thrust problem
- Inlet detail: [L10 — Inlets](L10-inlets.md)
- Ramjet combustors: [L12](L12-afterburners-ramjet-combustors.md)
- Gas dynamics used here: [L05](L05-gas-dynamics.md)
- Course hub: [EAS4300](../EAS4300.md)
