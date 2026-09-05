# L12 — Afterburners and Ramjet Combustors

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 12 · **Date:** Fri 2 Oct 2026
**Book §:** 6.5 *Afterburners and Ramjet Combustors* (p. 257) — ✅ verified
**Tags:** #afterburner #reheat #thrust-augmentation #flameholder #v-gutter #screech #thermal-choking #dump-combustor #variable-nozzle

**⚠️ Last new material before Midterm 1** (5 Oct review, 7 Oct exam).

---

## Why this lecture matters

The afterburner is the crudest and most effective thrust augmentation device in aviation: it can raise
thrust by 50% at the cost of tripling fuel flow. Understanding *why* that trade is so lopsided ties
together the cycle analysis of [L06](L06-thermodynamics-of-jet-engines.md), the Rayleigh flow of
[L05](L05-gas-dynamics.md), and the stabilization physics of [L11](L11-combustors.md).

---

## Core concepts

### 1. Why an afterburner works at all

**The key enabling fact:** gas turbine combustors run **overall lean**, $\phi \approx 0.25$–0.3
([L11](L11-combustors.md)). So turbine exhaust at station 5 still contains **~70% of its original
oxygen**. You can simply burn more fuel in it.

**Why burn it downstream instead of in the main combustor?** Because the main combustor's exit
temperature is capped by the **turbine** — that's the whole constraint of
[L04](L04-combustion-thermodynamics-2.md). Downstream of the turbine there is no rotating machinery to
protect; the only limits are the liner, the nozzle, and the structure. So you can go to **2,000–2,200 K**
versus the turbine's 1,700–1,900 K.

```
... → Turbine → 5 → [ Diffuser | Flameholders | Burning | Liner ] → 7 → [ Variable Nozzle ] → 9
```

### 2. Where the thrust comes from

Adding heat at station 6–7 raises $T_{07}$ substantially. Since exit velocity scales as:

$$
u_9 = \sqrt{2 c_p T_{07}\left[1 - \left(\frac{p_0}{p_{07}}\right)^{\frac{\gamma-1}{\gamma}}\right]}
$$

and the nozzle pressure ratio is essentially unchanged, exit velocity scales as:

$$
\frac{u_{9,AB}}{u_{9,dry}} \approx \sqrt{\frac{T_{07,AB}}{T_{05}}}
$$

**Thrust augmentation ratio:**

$$
\frac{F_{AB}}{F_{dry}} \approx \frac{u_{9,AB}-u_0}{u_{9,dry}-u_0}
$$

**Typical numbers:** $T_{05} \approx 900$ K, $T_{07} \approx 2000$ K:

$$
\frac{u_{9,AB}}{u_{9,dry}} = \sqrt{\frac{2000}{900}} = 1.49
$$

Roughly **50% more thrust** at static conditions (more at speed, because $u_0$ subtracts).

### 3. Why it's so inefficient — the crucial argument

**The heat is added at low pressure.** Recall ideal Brayton efficiency
([L06](L06-thermodynamics-of-jet-engines.md)):

$$
\eta_{th} = 1 - \frac{1}{r_p^{\frac{\gamma-1}{\gamma}}}
$$

Main combustor heat is added at station 3, after the full compressor pressure ratio — say $p_{03}/p_0 = 30$.
Afterburner heat is added at station 6, after the turbine has already expanded the flow — perhaps
$p_{06}/p_0 = 3$.

**A useful way to see it:** the afterburner is a Brayton cycle with a pressure ratio of ~3, bolted onto
an engine with a pressure ratio of ~30. Its thermal efficiency is correspondingly poor.

**Quantitatively:**

$$
\eta_{th,\text{main}} = 1 - 30^{-0.286} = 0.62
\qquad
\eta_{th,\text{AB}} = 1 - 3^{-0.286} = 0.27
$$

**Consequences:**
- **TSFC roughly doubles to triples.** Typical dry TSFC ~0.8 lbm/(lbf·hr); wet ~2.0–2.5.
- Afterburning is used in **short bursts**: takeoff, transonic acceleration, combat maneuver, emergency.
- A fighter can empty its tanks in **minutes** in full afterburner.

**Supercruise** — sustained supersonic flight *without* afterburner (F-22) — is valuable precisely
because it avoids this penalty. It requires very high dry thrust, which means high TIT and low bypass.

### 4. Flame stabilization at 150 m/s

Afterburner flow is much faster than main combustor flow:
**Main combustor:** ~30 m/s after diffusion. **Afterburner:** **120–200 m/s.**

A swirler is impractical (too much pressure loss, too much length), so afterburners use **bluff-body
flameholders**:

- **V-gutter (vee-gutter)** — annular and radial V-section rings. The wake behind each creates a
  recirculation zone that continuously re-ignites the incoming mixture. Standard practice.
- **Radial spraybars** upstream inject and distribute fuel.
- **Perforated/screech liner** — a double-wall liner with cooling air and thousands of small holes.

**Blowout limit:** the flame holds only if the recirculation zone can ignite incoming mixture faster
than the flow sweeps it away. A common correlation form:

$$
\frac{u_{\text{blowout}}\,\tau_{\text{chem}}}{d_{\text{holder}}} < \mathrm{const}
$$

**Bigger flameholders are more stable but cost more pressure loss** — the fundamental afterburner
trade. Dry loss from the flameholders alone is typically **2–5% of $p_0$**, and you pay it *even when
the afterburner is off*. That standing penalty is one reason afterburners are absent from civil
engines.

### 5. Thermal choking and the variable nozzle

**This is the single most examinable point in the lecture.**

The afterburner is essentially a **constant-area duct with heat addition** — textbook Rayleigh flow
([L05](L05-gas-dynamics.md) §10). Heating drives the Mach number toward 1, and there is a **maximum
heat addition** before the duct thermally chokes.

**The consequence for the engine:** heating the gas lowers its density, so at fixed mass flow it needs
**more area** to pass. If the nozzle throat area $A_8$ stayed fixed, lighting the afterburner would
back the flow up — raising pressure at the turbine exit, reducing turbine expansion, unloading the
turbine, slowing the spool, and potentially **surging the compressor**
([L16](L16-compressors-3.md)).

**Therefore every afterburning engine has a variable-area nozzle.** $A_8$ must open when the
afterburner lights, by roughly:

$$
\frac{A_{8,AB}}{A_{8,dry}} \approx \sqrt{\frac{T_{07,AB}}{T_{07,dry}}}
$$

For the numbers in §2, $\sqrt{2000/900} \approx 1.5$ — **the throat must open ~50%.** The nozzle and
afterburner are scheduled together by the control system; they cannot be operated independently.

This is a beautiful illustration of the course's recurring theme: **components cannot be designed in
isolation.** A combustion decision (light the AB) propagates through gas dynamics (choking) to
mechanical design (variable nozzle) to compressor stability (surge margin).

### 6. Screech and rumble

Afterburners are extremely prone to **combustion instability** — worse than main combustors because
the duct is long, largely open, and acoustically resonant.

- **Screech** — high-frequency (500–3,000 Hz), typically **transverse/circumferential** acoustic modes.
  Can destroy hardware in **seconds** through fatigue.
- **Rumble/buzz** — low-frequency (50–200 Hz), longitudinal modes.

**Rayleigh's criterion** again: instability grows when heat release oscillates *in phase* with pressure.

**The fix:** the **screech liner** — a perforated inner liner backed by a cooling annulus. It acts as a
distributed **Helmholtz resonator array**, absorbing acoustic energy at the troublesome frequencies,
while the through-flow cools the liner. It is doing two jobs at once, and the perforation pattern is
acoustically tuned, not merely a cooling choice.

### 7. Ramjet combustors — the same physics, harder

A ramjet combustor ([L07](L07-ramjets.md)) faces afterburner-like conditions but without a turbine
upstream to condition the flow:

- **Inlet air is very hot** from ram compression — 600–1,300 K at M 3–5 — which actually *helps*
  ignition and flame speed
- **No turbine downstream**, so temperature limits are set by the liner and nozzle only
- **Dump combustor** geometry — a sudden area expansion whose recirculating step wake anchors the
  flame, sometimes with additional V-gutters or cavity flameholders
- **Thermal choking is a hard performance limit**, not just a control constraint — it directly caps
  achievable $T_{04}$ and therefore thrust
- **Combustor pressure directly couples to inlet stability** — too much heat raises back pressure and
  can **unstart** the inlet ([L10](L10-inlets.md) §7)

**Scramjet combustors** are the extreme case: flow transits in ~1 ms at M 2+, so fuel must inject, mix,
ignite, and burn in that window. Hydrogen is favored for its high reactivity and diffusivity. Cavity
flameholders and strut/ramp injectors are the usual approaches. Mixing, not chemistry, is typically the
limiting process.

---

## Worked logic — afterburner thrust and fuel penalty

**Given:** turbojet at sea-level static. Dry: $T_{05}=900$ K, $p_{05}/p_0 = 2.5$, $\dot m_a = 60$ kg/s,
$f_{\text{main}}=0.022$. Afterburner to $T_{07}=2000$ K. $c_{p,h}=1150$ J/(kg·K), $\gamma_h = 1.33$,
$Q_R = 43$ MJ/kg, $\eta_{AB}=0.95$, $\pi_{AB}=0.95$.

**Step 1 — dry exit velocity** (perfectly expanded):

$$
u_{9,dry} = \sqrt{2 c_p T_{05}\left[1-\left(\frac{1}{2.5}\right)^{\frac{0.33}{1.33}}\right]}
$$

$$
\left(\frac{1}{2.5}\right)^{0.2481} = 0.7982
$$

$$
u_{9,dry} = \sqrt{2(1150)(900)(0.2018)} = \sqrt{417{,}726} = 646\ \mathrm{m/s}
$$

**Step 2 — wet exit velocity.** $p_{07}/p_0 = 2.5\times0.95 = 2.375$:

$$
\left(\frac{1}{2.375}\right)^{0.2481}=0.7930
$$

$$
u_{9,AB}=\sqrt{2(1150)(2000)(0.2070)} = \sqrt{952{,}200}=976\ \mathrm{m/s}
$$

**Step 3 — thrust (static, so $u_0=0$):**

$$
F_{dry} \approx 60(1.022)(646) = 39{,}612\ \mathrm{N} \approx 39.6\ \mathrm{kN}
$$

$$
F_{AB} \approx 60(1.022 + f_{AB})(976)
$$

**Step 4 — afterburner fuel:**

$$
f_{AB} = \frac{(1+f_{\text{main}})c_{p,h}(T_{07}-T_{05})}{\eta_{AB}Q_R - c_{p,h}T_{07}}
= \frac{1.022 \times 1150(2000-900)}{0.95\times43\times10^6 - 1150\times2000}
$$

$$
f_{AB} = \frac{1.293\times10^6}{4.085\times10^7 - 2.3\times10^6}=\frac{1.293\times10^6}{3.855\times10^7}=0.0335
$$

$$
F_{AB} \approx 60(1.0555)(976) = 61{,}810\ \mathrm{N} \approx 61.8\ \mathrm{kN}
$$

**Step 5 — the trade:**

$$
\frac{F_{AB}}{F_{dry}} = \frac{61.8}{39.6} = 1.56
\qquad\text{(+56\% thrust)}
$$

$$
\mathrm{TSFC}_{dry}=\frac{60\times0.022}{39{,}612}=3.33\times10^{-5}\ \mathrm{kg/(N\cdot s)}
$$

$$
\mathrm{TSFC}_{AB}=\frac{60(0.022+0.0335)}{61{,}810}=\frac{3.33}{61{,}810}=5.39\times10^{-5}\ \mathrm{kg/(N\cdot s)}
$$

**Result: +56% thrust for +62% TSFC.** Fuel *flow* rises by 152% (from 1.32 to 3.33 kg/s) while thrust
rises only 56%.

**Step 6 — required nozzle area change:**

$$
\frac{A_{8,AB}}{A_{8,dry}} \approx \sqrt{\frac{2000}{900}}\times\frac{1}{0.95} \approx 1.57
$$

**The throat must open ~57%.** Without that, the engine would surge.

**Rigorous cross-check** (cross-referenced from a parallel offering's worked example): the approximate
$\sqrt{T_{07}/T_{05}}$ scaling above ignores that $\gamma$ **drops** in the afterburning gas (less
associated, more monatomic-like at higher $T$) and that the AB liner adds its own pressure loss. Redo
it properly with the **choked-nozzle flow parameter**
$FP_7 = \dot m\sqrt{T_7}/(A_7 P_7) = \sqrt{\gamma g_c/R}\,\left[2/(\gamma+1)\right]^{(\gamma+1)/2(\gamma-1)}$,
using $\dot m=165$ pps, $T_5=1{,}200°\mathrm F$, $P_5=35$ psia:

$$
\textbf{Non-AB } (\gamma=1.33,\ \text{no extra loss}):\quad
T_7=1{,}660°\mathrm R,\ P_7=P_5(1-0.03)=33.95\ \text{psia}
$$
$$
FP_7 = 0.522, \qquad A_7 = \frac{\dot m\sqrt{T_7}}{FP_7\,P_7} = 2.632\ \mathrm{ft^2}
$$
$$
\textbf{AB } (\gamma=1.29,\ \text{AB liner loss }8\%):\quad
T_7=2{,}800°\mathrm F+459.67=3{,}260°\mathrm R,\ P_7=P_5(1-0.08)=32.2\ \text{psia}
$$
$$
FP_7 = 0.517, \qquad A_7 = 3.931\ \mathrm{ft^2}
$$

$$
\frac{A_{7,AB}}{A_{7,dry}} = \frac{3.931}{2.632} \approx 1.49
$$

**A more careful ~49% area increase** — close to, but genuinely different from, the quick
$\sqrt{T_{07}/T_{05}}$ estimate above (~57%), because the drop in $\gamma$ partially offsets the
temperature-driven area growth. **Use the quick estimate for intuition; use the full $FP$ calculation
when a real number is needed** — the gap between the two is exactly the kind of "approximation vs.
rigorous" comparison that shows up in exam short-answer questions.

---

## Common pitfalls

- **Thinking the afterburner needs its own air supply.** It uses leftover oxygen from the lean main burn.
- **Forgetting the variable nozzle requirement.** This is the most-missed exam point on this topic.
- **Missing the low-pressure-heat-addition argument** for why AB efficiency is poor. "It just burns more
  fuel" is not an answer — the *pressure at which the heat is added* is the reason.
- **Ignoring the dry pressure loss from flameholders.** You pay 2–5% even with the AB off.
- **Applying main-combustor stabilization thinking.** Swirlers don't work at 150 m/s; bluff bodies do.
- **Forgetting thermal choking limits heat addition.**
- **Using cold $\gamma$.** Afterburner gas is very hot; $\gamma \approx 1.30$–1.33.
- **Assuming a screech liner is just cooling.** It's an acoustic damper first.
- **Comparing $F_{AB}/F_{dry}$ at static and at speed as if equal.** With $u_0$ subtracting, the
  augmentation ratio *rises* with flight speed.

---

## Exam checklist

- [ ] Explain why leftover oxygen exists in turbine exhaust
- [ ] Explain why $T_{07}$ can exceed $T_{04}$
- [ ] Derive $u_{9,AB}/u_{9,dry}\approx\sqrt{T_{07}/T_{05}}$
- [ ] **Explain the low-pressure heat addition argument for poor AB efficiency, with Brayton numbers**
- [ ] Describe V-gutter stabilization and the size/pressure-loss trade
- [ ] **Explain thermal choking and why a variable-area nozzle is mandatory; estimate $A_8$ ratio**
- [ ] Describe screech, rumble, Rayleigh's criterion, and the screech liner's dual role
- [ ] Compare afterburner and ramjet combustor conditions
- [ ] Compute AB fuel-air ratio, thrust augmentation, and TSFC penalty
- [ ] Explain what supercruise is and why it's desirable

---

## Links

- Previous: [L11 — Combustors](L11-combustors.md)
- **Midterm 1 review 5 Oct, exam 7 Oct** → [exam-midterm-1](exam-midterm-1.md)
- Next: [L13 — Nozzles](L13-nozzles.md) (after the exam and the 9 Oct holiday)
- Rayleigh flow / thermal choking: [L05 — Gas Dynamics](L05-gas-dynamics.md)
- Ramjet cycle: [L07 — Ramjets](L07-ramjets.md)
- Inlet unstart coupling: [L10 — Inlets](L10-inlets.md)
- Course hub: [EAS4300](../EAS4300.md)
