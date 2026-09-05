# L05 — Gas Dynamics (3 sessions)

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 5
**Dates:** Wed 2 Sep (§3.1–3.3) · Fri 4 Sep (§3.4–3.5) · Wed 9 Sep (§3.6) 2026
*(Mon 7 Sep — Labor Day holiday, no class)*
**Book §:** 3.1 *Introduction* · 3.2 *General One-Dimensional Flow of a Perfect Gas* · 3.3 *Isentropic
Flow* · 3.4 *Nonisentropic Flow* · 3.5 *Frictionless Constant-Area Flow with Stagnation Temperature
Change* (Rayleigh) · 3.6 *Constant-Area Flow with Friction* (Fanno) — ✅ verified

> 📖 **Reconciled 2026-08-25.** The section titles confirm this page's structure — including that
> **§3.5 is Rayleigh flow and §3.6 is Fanno flow**, exactly as covered in Part 3 below.
>
> ⚠️ **But §3.7 is "Shocks" — one section past the assigned range.** Parts 2 below (normal shocks,
> oblique shocks, Prandtl-Meyer) therefore sits *just outside* what the syllabus assigns. **Study it
> anyway:** §6.3 Supersonic Inlets ([L10](L10-inlets.md)) is assigned and is unintelligible without
> shocks. Worth confirming with the instructor, but treat shocks as in scope.
> See [textbook-section-map](textbook-section-map.md).
**Tags:** #gas-dynamics #isentropic #area-mach #choking #normal-shock #oblique-shock #fanno #rayleigh #compressible-flow #nozzle-flow

---

## Why this lecture matters

This is the **longest single topic in the course** (three class meetings) and the most heavily used.
Inlets, nozzles, and every transonic turbomachinery blade row are gas dynamics problems. If you can
answer "given $M$ and an area change, what happens?" instantly, [L10](L10-inlets.md) and
[L13](L13-nozzles.md) become easy. If not, they won't.

The single governing idea: **in compressible flow, density changes are not a detail — they reverse
your intuition.** A converging duct accelerates subsonic flow and decelerates supersonic flow. Nothing
in incompressible fluids prepares you for that.

---

# Part 1 — Isentropic flow, area relations, choking (§3.1–3.3)

## Core concepts

### 1. Speed of sound and the Mach number

Sound is an infinitesimal pressure disturbance propagating isentropically:

$$
a^2 = \left(\frac{\partial p}{\partial \rho}\right)_s = \gamma R T
$$

$$
M = \frac{V}{a}
$$

**$M$ is the ratio of directed kinetic energy to random thermal energy.** That's why it, and not
velocity, is the natural variable: it measures how much the flow's own motion matters compared to the
molecular motion that transmits pressure signals.

**The information-propagation view (the one that explains everything else):** pressure disturbances
travel at $a$ relative to the fluid. If $M<1$, disturbances can travel upstream — downstream
conditions are "felt" upstream. If $M>1$, they cannot — **the flow is deaf to what's ahead of it.**
This is why supersonic flow needs shocks (abrupt adjustment, since gradual adjustment is impossible)
and why a choked nozzle's mass flow is immune to back pressure.

### 2. Isentropic relations

Restated from [L02](L02-basic-concepts.md), because you'll use them a hundred times:

$$
\frac{T_0}{T} = 1 + \frac{\gamma-1}{2}M^2
$$

$$
\frac{p_0}{p} = \left(1 + \frac{\gamma-1}{2}M^2\right)^{\frac{\gamma}{\gamma-1}}
$$

$$
\frac{\rho_0}{\rho} = \left(1 + \frac{\gamma-1}{2}M^2\right)^{\frac{1}{\gamma-1}}
$$

**Critical (sonic, $M=1$) values** — the reference state for all "starred" quantities:

$$
\frac{T^*}{T_0} = \frac{2}{\gamma+1}, \qquad
\frac{p^*}{p_0} = \left(\frac{2}{\gamma+1}\right)^{\frac{\gamma}{\gamma-1}}, \qquad
\frac{\rho^*}{\rho_0} = \left(\frac{2}{\gamma+1}\right)^{\frac{1}{\gamma-1}}
$$

For $\gamma = 1.4$ these are the numbers to memorize:

$$
\frac{T^*}{T_0} = 0.8333, \qquad \frac{p^*}{p_0} = 0.5283, \qquad \frac{\rho^*}{\rho_0} = 0.6339
$$

**$p^*/p_0 = 0.528$** is the most useful single number in the course: if the pressure ratio across a
converging nozzle exceeds ~1.89, it is choked.

### 3. The area-velocity relation — the counterintuitive core

Combine continuity, momentum, and the isentropic relation (derivation below):

$$
\frac{dA}{A} = \left(M^2 - 1\right)\frac{dV}{V}
$$

Everything follows from the sign of $(M^2-1)$:

| | **Subsonic ($M<1$)** | **Supersonic ($M>1$)** |
|---|---|---|
| **Converging** $dA<0$ | Accelerates | **Decelerates** |
| **Diverging** $dA>0$ | Decelerates | **Accelerates** |

**Physical reason:** in continuity $\rho A V = $ const, going supersonic means density falls *faster*
than velocity rises. To keep $\dot m$ constant while $V$ increases, area must therefore *increase*.
The dominance flips exactly at $M=1$.

**Corollary — the converging-diverging (de Laval) nozzle.** To accelerate from rest to supersonic you
must converge to a throat where $M=1$, then diverge. There is no other geometry that does it.
And: **$M=1$ can only occur where $dA = 0$**, i.e. at a throat (or in a constant-area duct with
friction or heat addition — see Part 3).

### 4. Choking and the area ratio

Once the throat reaches $M=1$, the mass flow is **fixed**. Lowering back pressure further cannot
increase $\dot m$ — the "lower the pressure downstream" signal physically cannot propagate upstream
past the sonic throat.

**Choked mass flow** (the single most-used formula in nozzle problems):

$$
\dot{m} = \frac{p_0 A^*}{\sqrt{T_0}}\sqrt{\frac{\gamma}{R}}
\left(\frac{2}{\gamma+1}\right)^{\frac{\gamma+1}{2(\gamma-1)}}
$$

Note what it depends on: **$p_0$, $T_0$, and $A^*$ only.** Not back pressure. This is the origin of the
"corrected mass flow" grouping used on every compressor and turbine map —
see [corrected-parameters](../../concepts/corrected-parameters.md).

General mass flow at any $M$:

$$
\dot{m} = \frac{p_0 A}{\sqrt{T_0}}\sqrt{\frac{\gamma}{R}}\;
M\left(1+\frac{\gamma-1}{2}M^2\right)^{-\frac{\gamma+1}{2(\gamma-1)}}
$$

**Area-Mach relation** — dividing the two:

$$
\frac{A}{A^*} = \frac{1}{M}\left[\frac{2}{\gamma+1}\left(1+\frac{\gamma-1}{2}M^2\right)\right]^{\frac{\gamma+1}{2(\gamma-1)}}
$$

**Critical property: $A/A^*$ has two solutions for every value > 1** — one subsonic, one supersonic.
The geometry alone doesn't tell you which; the **boundary conditions** (back pressure) do. Picking the
wrong root is the #1 error in nozzle problems.

### 5. Nozzle operating regimes

For a converging-diverging nozzle with fixed $p_0$ and falling back pressure $p_b$:

1. **Fully subsonic.** Throat not choked, acts like a venturi. $\dot m$ increases as $p_b$ drops.
2. **Choked, subsonic diverging section.** Throat hits $M=1$. $\dot m$ now fixed. Flow decelerates
   after the throat.
3. **Normal shock inside the diverging section.** Supersonic after throat, shock, then subsonic to
   exit at $p_b$. As $p_b$ drops the shock moves downstream.
4. **Shock at the exit plane.**
5. **Overexpanded ($p_e < p_b$).** Oblique shocks outside the nozzle. Exhaust plume contracts.
6. **Design / perfectly expanded ($p_e = p_b$).** No waves. Maximum thrust for that geometry.
7. **Underexpanded ($p_e > p_b$).** Expansion fans outside. Plume spreads.

**Only regimes 3 and later have supersonic flow at the throat exit; only 5–7 have no shocks inside.**
Rocket nozzles at sea level are typically overexpanded and at altitude underexpanded, which is exactly
why altitude-compensating nozzles are attractive — see [L24](L24-rocket-engines-2.md).

---

# Part 2 — Shock waves (§3.4–3.5)

## Core concepts

### 6. Normal shocks

A **shock** is an extremely thin (a few mean free paths) region of abrupt, **irreversible** adjustment.
It exists because supersonic flow cannot receive advance warning of a downstream obstruction, so the
adjustment must be discontinuous.

**Across a normal shock:**

| Quantity | Change |
|---|---|
| $M$ | Always $M_1 > 1 \to M_2 < 1$ |
| $p$, $T$, $\rho$ | **Increase** |
| $V$ | Decreases |
| $T_0$ | **Constant** (adiabatic, no work) |
| $p_0$ | **Decreases** (irreversible) |
| $s$ | Increases |

**A shock can only go supersonic → subsonic.** The reverse would decrease entropy — forbidden. This is
the second law doing real engineering work.

**Normal shock relations** (all functions of $M_1$ and $\gamma$ alone):

$$
M_2^2 = \frac{1 + \frac{\gamma-1}{2}M_1^2}{\gamma M_1^2 - \frac{\gamma-1}{2}}
$$

$$
\frac{p_2}{p_1} = \frac{2\gamma M_1^2 - (\gamma-1)}{\gamma+1}
$$

$$
\frac{\rho_2}{\rho_1} = \frac{V_1}{V_2} = \frac{(\gamma+1)M_1^2}{(\gamma-1)M_1^2 + 2}
$$

$$
\frac{T_2}{T_1} = \frac{\left[2\gamma M_1^2-(\gamma-1)\right]\left[(\gamma-1)M_1^2+2\right]}{(\gamma+1)^2 M_1^2}
$$

**Stagnation pressure ratio — the loss metric that matters for propulsion:**

$$
\frac{p_{02}}{p_{01}} = \left[\frac{(\gamma+1)M_1^2}{(\gamma-1)M_1^2+2}\right]^{\frac{\gamma}{\gamma-1}}
\left[\frac{\gamma+1}{2\gamma M_1^2 - (\gamma-1)}\right]^{\frac{1}{\gamma-1}}
$$

Equivalently $p_{02}/p_{01} = A_1^*/A_2^*$ — the shock effectively enlarges the sonic area.

**Numbers worth carrying** ($\gamma=1.4$): the loss is negligible at low supersonic Mach and brutal at
high Mach. That asymmetry is the entire justification for multi-shock supersonic inlets.

| $M_1$ | $M_2$ | $p_2/p_1$ | $p_{02}/p_{01}$ |
|---|---|---|---|
| 1.0 | 1.000 | 1.00 | 1.000 |
| 1.5 | 0.701 | 2.46 | 0.930 |
| 2.0 | 0.577 | 4.50 | 0.721 |
| 2.5 | 0.513 | 7.13 | 0.499 |
| 3.0 | 0.475 | 10.33 | 0.328 |
| 4.0 | 0.435 | 18.50 | 0.139 |

**At $M=3$, a single normal shock throws away two-thirds of your stagnation pressure.** Since engine
thrust scales roughly with $p_0$ delivered to the combustor, that is catastrophic — hence
[L10](L10-inlets.md)'s multi-shock designs.

### 7. Oblique shocks

A shock at angle $\beta$ to the flow, produced when supersonic flow is turned into itself by angle
$\theta$ (a wedge, a cone, a compression ramp).

**The decomposition trick:** only the **normal component** of Mach number matters for the shock jump.
The tangential component is unchanged.

$$
M_{n1} = M_1 \sin\beta
$$

Then apply **every normal-shock relation** using $M_{n1}$ in place of $M_1$, and recover:

$$
M_2 = \frac{M_{n2}}{\sin(\beta - \theta)}
$$

**θ-β-M relation** (the one you read off charts):

$$
\tan\theta = 2\cot\beta\,\frac{M_1^2\sin^2\beta - 1}{M_1^2\left(\gamma + \cos 2\beta\right)+2}
$$

**Three facts about this relation that get examined:**

1. **For each $\theta$ below a maximum, there are two solutions** — a **weak** shock (smaller $\beta$,
   usually $M_2 > 1$) and a **strong** shock (larger $\beta$, $M_2 < 1$). Nature picks the weak one
   unless back pressure forces otherwise.
2. **Above $\theta_{max}$ there is no attached solution** — the shock **detaches** and stands off as a
   curved bow shock. $\theta_{max} \approx 34°$ at $M=2$, rising toward ~45° at high $M$.
3. **Oblique shocks are far less lossy than normal shocks** for the same total turning, because
   $M_{n1} = M_1\sin\beta < M_1$. Splitting one strong shock into several weak ones dramatically
   reduces total $p_0$ loss. **This is the design principle of the supersonic inlet.**

**Mach wave** — the limiting infinitely weak case:

$$
\mu = \arcsin\frac{1}{M}
$$

### 8. Prandtl-Meyer expansion

The opposite of a shock: supersonic flow turning *away* from itself expands through a smooth,
**isentropic** fan. $M$ increases, $p$/$T$/$\rho$ decrease, and — critically — **$p_0$ is conserved**.

$$
\nu(M) = \sqrt{\frac{\gamma+1}{\gamma-1}}\arctan\sqrt{\frac{\gamma-1}{\gamma+1}\left(M^2-1\right)}
- \arctan\sqrt{M^2-1}
$$

$$
\theta = \nu(M_2) - \nu(M_1)
$$

**Asymmetry to remember:** compression through shocks is lossy; expansion through fans is free. Which
is why nozzle expansion (all fan) is efficient and inlet compression (all shock) is not.

---

# Part 3 — Flow with friction and heat addition (§3.6)

Constant-area ducts where the driver is *not* area change. These are the models for combustors,
afterburners, and long ducts.

### 9. Fanno flow — adiabatic flow with friction

Constant area, adiabatic, with wall friction. **$T_0$ constant, $p_0$ falls, $s$ increases.**

$$
\frac{4 f_F L^*}{D} = \frac{1-M^2}{\gamma M^2}
+ \frac{\gamma+1}{2\gamma}\ln\left[\frac{(\gamma+1)M^2}{2\left(1+\frac{\gamma-1}{2}M^2\right)}\right]
$$

$$
\frac{p}{p^*} = \frac{1}{M}\left[\frac{\gamma+1}{2+(\gamma-1)M^2}\right]^{1/2}
$$

$$
\frac{T}{T^*} = \frac{\gamma+1}{2+(\gamma-1)M^2}
$$

**The headline result: friction drives *both* subsonic and supersonic flow toward $M=1$.**
- Subsonic flow **accelerates** toward $M=1$
- Supersonic flow **decelerates** toward $M=1$

Sonic is the maximum-entropy point on the Fanno line, and friction can only increase entropy. You
cannot pass through $M=1$ by friction alone — attempting a longer duct than $L^*$ causes **choking**,
and the upstream flow adjusts (reduced $\dot m$, or the shock repositions).

### 10. Rayleigh flow — frictionless flow with heat addition

Constant area, no friction, with heat transfer. **This is the combustor model.**

$$
\frac{T_0}{T_0^*} = \frac{(\gamma+1)M^2\left[2+(\gamma-1)M^2\right]}{\left(1+\gamma M^2\right)^2}
$$

$$
\frac{p}{p^*} = \frac{\gamma+1}{1+\gamma M^2}
$$

$$
\frac{T}{T^*} = \frac{M^2(\gamma+1)^2}{\left(1+\gamma M^2\right)^2}
$$

$$
\frac{p_0}{p_0^*} = \frac{\gamma+1}{1+\gamma M^2}
\left[\frac{2+(\gamma-1)M^2}{\gamma+1}\right]^{\frac{\gamma}{\gamma-1}}
$$

**Again, heating drives flow toward $M=1$ from both sides.** And there is a **maximum heat addition**:
once $M=1$ is reached, adding more heat **thermally chokes** the duct and forces the upstream flow to
adjust — reduced mass flow, or a shock system moving.

**Two results that matter enormously for propulsion:**

1. **Rayleigh $p_0$ loss.** Heating a compressible flow *always* reduces stagnation pressure, even with
   zero friction. This is a fundamental thermodynamic cost, not a design deficiency, and it's why
   combustors are kept at low Mach number ($M \approx 0.05$–$0.2$) — the loss scales roughly with $M^2$.
2. **Thermal choking limits afterburners and ramjets.** You cannot add unlimited heat to a
   constant-area duct. This directly caps ramjet performance ([L07](L07-ramjets.md)) and drives
   afterburner duct sizing ([L12](L12-afterburners-ramjet-combustors.md)).

**A subtlety students get wrong:** in *subsonic* Rayleigh flow, heat addition raises $T_0$ but the
**static** temperature can actually *decrease* near $M = 1/\sqrt{\gamma}$, because the flow accelerates
so strongly that kinetic energy grows faster than total enthalpy. Counterintuitive, and a favorite
exam question.

### 11. Summary table — what drives flow toward sonic

| Mechanism | Subsonic effect | Supersonic effect | $T_0$ | $p_0$ |
|---|---|---|---|---|
| **Area decrease** | $M \uparrow$ | $M \downarrow$ | const | const (isentropic) |
| **Area increase** | $M \downarrow$ | $M \uparrow$ | const | const (isentropic) |
| **Friction (Fanno)** | $M \to 1$ | $M \to 1$ | const | ↓ |
| **Heating (Rayleigh)** | $M \to 1$ | $M \to 1$ | ↑ | ↓ |
| **Cooling** | $M \to 0$ | $M \to \infty$ | ↓ | ↑ |
| **Normal shock** | — | $M>1 \to M<1$ | const | ↓↓ |

**Learn this table.** Nearly every conceptual gas-dynamics exam question is a lookup in it.

---

## Worked logic — deriving the area-velocity relation

Start with the differential forms.

Continuity (log-differentiated):

$$
\frac{d\rho}{\rho} + \frac{dA}{A} + \frac{dV}{V} = 0
$$

Euler / momentum for inviscid steady flow:

$$
dp + \rho V\, dV = 0 \quad\Longrightarrow\quad \frac{dp}{\rho} = -V\,dV
$$

Isentropic, so $dp = a^2 d\rho$:

$$
\frac{a^2 d\rho}{\rho} = -V\,dV
\quad\Longrightarrow\quad
\frac{d\rho}{\rho} = -\frac{V\,dV}{a^2} = -M^2\frac{dV}{V}
$$

Substitute into continuity:

$$
-M^2\frac{dV}{V} + \frac{dA}{A} + \frac{dV}{V} = 0
$$

$$
\boxed{\ \frac{dA}{A} = \left(M^2-1\right)\frac{dV}{V}\ }
$$

**Read the physics off the algebra:** the term $-M^2 \, dV/V$ is the density change. When $M<1$, density
changes slowly, velocity dominates, and the incompressible intuition (converge ⇒ accelerate) holds.
When $M>1$, the density term wins and the sign flips.

---

## Worked logic — Fanno flow, solving *backwards* from a choked exit

*Cross-referenced from a prior Anup Mannem-taught offering's homework (dated Jan 2025/2026 — the same
instructor as your Fall 2026 syllabus, a materially stronger source than the Marcos cross-references
elsewhere in this wiki; see the note on [the course hub](../EAS4300.md#sources)).* Every Fanno example
elsewhere in this wiki gives you $M_1$ and asks for what happens downstream. This one runs the
$4fL/D$ relation **the other direction**: given the duct exactly reaches choking, find the *inlet*
Mach number.

**Given:** a $D=0.3$ m, $L=3$ m pipe, Fanning friction factor $f=0.0040$, and the flow **just reaches**
$M_2=1$ at the exit (i.e., $L$ equals the sonic length $L^*$ for whatever $M_1$ is), $\gamma=1.4$,
stagnation pressure $P_{0,1}=1.5$ MPa.

**Step 1 — set up the Fanno relation with $M_2=1$, which collapses the RHS to the sonic-length
form** (this is exactly $4fL^*/D$ from [L05](L05-gas-dynamics.md) §9, evaluated at the *inlet* Mach
number since $L=L^*$ here):

$$
\frac{4fL}{D} = \frac{1-M_1^2}{\gamma M_1^2} + \frac{\gamma+1}{2\gamma}\ln\left[\frac{(\gamma+1)M_1^2}{2+(\gamma-1)M_1^2}\right]
$$

$$
\frac{4(0.0040)(3)}{0.3} = 0.16 = \frac{1-M_1^2}{1.4M_1^2}+\frac{6}{7}\ln\left[\frac{2.4M_1^2}{1+0.2M_1^2}\right]
$$

**This is transcendental in $M_1$ — solve by iteration/lookup, not algebra.** Result: $M_1 = 0.7275$.
**The technique to take away**: whenever a problem states or implies the duct is *exactly* at its
choking length, $4fL/D$ becomes $4fL^*/D$ evaluated at the **known** end of the duct, converting an
otherwise-unknown-at-both-ends problem into a solvable one.

**Step 2 — static and stagnation pressure at the inlet**, from the isentropic relation
([L02](L02-basic-concepts.md)) since station 1 itself is *not* inside the Fanno duct yet:

$$
P_1 = \frac{P_{0,1}}{\left(1+\frac{\gamma-1}{2}M_1^2\right)^{\gamma/(\gamma-1)}} = 1.5\times0.7032 = 1.055\ \mathrm{MPa}
$$

**Step 3 — carry $P_1$ through the Fanno $P/P^*$ table** to get conditions at the (now known, since
$M_2=1$) exit:

$$
\frac{P}{P^*} = \frac{1}{M}\sqrt{\frac{\gamma+1}{2+(\gamma-1)M^2}}
\;\Rightarrow\;
\frac{P_1}{P^*} = 1.432 \;\Rightarrow\; P^* = P_2 = 0.737\ \mathrm{MPa}
$$

$$
P_{0,2} = P_2\left(1+\frac{\gamma-1}{2}\right)^{\gamma/(\gamma-1)} = 0.737(1.893) = 1.395\ \mathrm{MPa}
$$

**Sanity check on the answer**: $P_{0,2}<P_{0,1}$ (1.395 < 1.5 MPa) — stagnation pressure fell, exactly
as friction must produce ([L05](L05-gas-dynamics.md) §11's summary table). If a "solve backwards"
Fanno answer ever comes out with $P_{0,2}>P_{0,1}$, you've made a sign or table-lookup error.

---

## Common pitfalls

- **Picking the wrong root of $A/A^*$.** Every area ratio > 1 has a subsonic *and* a supersonic
  solution. Decide from boundary conditions first.
- **Assuming a converging-diverging nozzle is supersonic at exit.** Only if it's choked *and* the back
  pressure is low enough. Regimes 1–4 are subsonic at exit.
- **Applying isentropic relations across a shock.** $T_0$ carries across; $p_0$ does not. Use shock
  relations, then resume isentropic from the new $p_0$.
- **Forgetting $T_0$ is constant across a shock.** Students often "lose" energy in a shock. Energy is
  conserved; *availability* is lost.
- **Using $\gamma = 1.4$ in a hot-section nozzle.** Use ~1.33.
- **Treating combustor $p_0$ loss as purely frictional.** The Rayleigh (heat addition) contribution is
  fundamental and unavoidable.
- **Assuming heating always raises static temperature.** In subsonic Rayleigh flow near
  $M = 1/\sqrt\gamma$, $T$ can fall while $T_0$ rises.
- **Thinking a shock can turn subsonic flow supersonic.** Second law forbids it.
- **Mach-number-averaging.** $M$ is not additive; never average Machs across stations.

---

## Exam checklist

- [ ] Derive $dA/A = (M^2-1)\,dV/V$ and explain the sign flip physically
- [ ] Write the isentropic $T_0/T$, $p_0/p$ relations and the $M=1$ critical ratios for $\gamma=1.4$
- [ ] State the choked mass flow formula and explain why $\dot m$ is independent of back pressure
- [ ] Sketch and label all seven C-D nozzle operating regimes
- [ ] Use the $A/A^*$ relation and correctly select subsonic vs. supersonic root
- [ ] Apply normal shock relations; state what happens to $M$, $p$, $T$, $T_0$, $p_0$, $s$
- [ ] Explain why $p_{02}/p_{01}$ collapses at high $M_1$ and what that implies for inlet design
- [ ] Decompose an oblique shock into normal/tangential components and solve
- [ ] Explain weak vs. strong solutions and shock detachment above $\theta_{max}$
- [ ] State why expansion fans are isentropic but shocks are not
- [ ] Describe Fanno and Rayleigh trends and state why both drive toward $M=1$
- [ ] Explain thermal choking and its consequence for ramjets and afterburners
- [ ] Reproduce the summary table in §11

---

## Links

- Previous: [L04 — Combustion Thermodynamics 2](L04-combustion-thermodynamics-2.md)
- Next: [L06 — Thermodynamics of Jet Engines](L06-thermodynamics-of-jet-engines.md)
- Shocks applied: [L10 — Inlets](L10-inlets.md)
- Nozzle regimes applied: [L13 — Nozzles](L13-nozzles.md), [L24 — Rocket Engines 2](L24-rocket-engines-2.md)
- Rayleigh applied: [L11 — Combustors](L11-combustors.md), [L12 — Afterburners](L12-afterburners-ramjet-combustors.md)
- Concept: [stagnation-properties](../../concepts/stagnation-properties.md)
- Concept: [corrected-parameters](../../concepts/corrected-parameters.md)
- Course hub: [EAS4300](../EAS4300.md)
