# L01 — Introduction

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 1 · **Date:** Fri 21 Aug 2026
**Book §:** 1.1 *Introduction* · 1.2 *Fluid Momentum and Reactive Force* · 1.4 ***Propellers*** (p. 16)
— ✅ verified

> 📖 **Reconciled 2026-08-25.** Note what the assignment includes and excludes. **§1.4 is
> "Propellers"** — so propellers are explicitly in scope for Lecture 1 (see §7 below, added for this).
> Meanwhile **§1.3 (Rockets) and §1.5 (Turbojets, Turbofans, and Ramjets) are *not* assigned** here —
> those engines get full treatment later, in Ch. 5 and Ch. 10.
> See [textbook-section-map](textbook-section-map.md).
**Tags:** #intro #thrust #engine-types #specific-impulse #propulsion-taxonomy #newton-third-law

---

## Why this lecture matters

Everything in this course is an elaboration of one sentence: **a propulsion system produces thrust by
throwing mass backwards.** The rest of the semester is about *where you get the mass*, *how you
energize it*, and *how efficiently you do both*. Lecture 1 sets the vocabulary and the taxonomy so
that when you meet a turbofan in Lecture 8 you already know what question you're asking of it.

---

## Core concepts

### 1. Thrust is a reaction force

Newton's third law, applied to a control volume around the engine. The engine accelerates a working
fluid rearward; the fluid pushes the engine forward. Crucially, **thrust does not require pushing
against anything external** — a rocket works in vacuum. The "pushing against air" intuition is wrong
and will cost you points.

The rigorous statement is a **momentum balance on a control volume**: thrust equals the net rate of
momentum flux out of the CV, plus any net pressure force on the CV boundary. That's developed
properly in [L02](L02-basic-concepts.md) and [L06](L06-thermodynamics-of-jet-engines.md); here you
just need the shape of it.

### 2. The fundamental split: air-breathing vs. rocket

This is the organizing distinction of the whole course, and of the catalog description
("air-breathing **and** rocket engines").

| | **Air-breathing** | **Rocket** |
|---|---|---|
| Oxidizer source | Atmospheric air (free) | Carried onboard |
| Propellant mass | Mostly ingested air | 100% onboard |
| Works in vacuum? | No | Yes |
| Thrust vs. altitude | Falls off with air density | Rises slightly (lower back-pressure) |
| Thrust vs. flight speed | Falls off (ram drag grows) | Independent of flight speed |
| Typical $I_{sp}$ | 2,000–6,000 s | 250–450 s (chemical) |
| Best for | Sustained atmospheric flight | Space access, vacuum, very high Mach |

**Why air-breathers have such enormous $I_{sp}$:** specific impulse is thrust per unit weight flow of
*propellant carried*. An air-breather carries only fuel; the ~15–60× larger air mass is free. It's not
that jets are thermodynamically better — it's that the bookkeeping only counts what you brought.

### 3. Taxonomy of air-breathing engines

Ordered roughly by increasing flight Mach number, and by decreasing amount of turbomachinery:

- **Turboprop / turboshaft** — gas turbine core drives a propeller (or a rotor/shaft). Most of the
  useful output leaves as shaft power, not jet momentum. Best at low subsonic speed, M ≲ 0.6.
- **Turbofan** — core drives a ducted fan. Fan air (the *bypass* stream) is accelerated modestly; the
  core stream is accelerated a lot. Dominant for M ≈ 0.7–0.9 transport aircraft.
  → [L08b](L08b-turbofans.md)
- **Turbojet** — all the air goes through the core. Simple, high jet velocity, poor propulsive
  efficiency at subsonic speed but competitive supersonically. → [L08a](L08a-turbojets.md)
- **Afterburning turbojet/turbofan** — extra fuel burned downstream of the turbine for thrust boost at
  terrible fuel economy. → [L12](L12-afterburners-ramjet-combustors.md)
- **Ramjet** — no turbomachinery at all; compression comes entirely from *ram* deceleration of the
  incoming supersonic flow. Cannot produce static thrust (needs to already be moving, M ≳ 2–3 to be
  useful). → [L07](L07-ramjets.md)
- **Scramjet** — ramjet with supersonic combustion, for M ≳ 5–6, where decelerating to subsonic would
  produce intolerable temperatures and shock losses.

**The pattern to remember:** as design flight Mach rises, ram compression does more of the work, so
you need less machinery. The turbomachinery exists to provide pressure rise that the flight speed
can't.

### 4. Taxonomy of rockets

- **Chemical** — liquid bipropellant, solid, hybrid. Energy is stored in the propellant's chemical
  bonds; the same substance is both energy source and reaction mass. High thrust, modest $I_{sp}$.
  → [L23](L23-rocket-engines-1.md), [L24](L24-rocket-engines-2.md)
- **Nuclear thermal** — external heat source, so you can use low-molecular-weight H₂ as reaction mass.
  Roughly 2× chemical $I_{sp}$.
- **Electric (ion, Hall, arcjet)** — electrical energy accelerates a small mass flow to very high
  velocity. $I_{sp}$ of thousands of seconds, but thrust measured in millinewtons. Power-limited, not
  energy-limited.

**The decoupling insight:** in a chemical rocket, energy source and reaction mass are the *same
stuff*, which caps $I_{sp}$ at what the chemistry allows. Every non-chemical concept exists to break
that coupling.

### 5. The two figures of merit

Introduced here, used all semester:

- **Specific impulse $I_{sp}$** — thrust per unit weight flow of propellant. "How much bang per kg
  carried." Dominates *rocket* and mission design.
- **Thrust-specific fuel consumption (TSFC)** — fuel mass flow per unit thrust. "How much fuel to hold
  a given thrust." Dominates *aircraft* economics. It is essentially the reciprocal of $I_{sp}$ for an
  air-breather.

They answer different questions and are used in different communities; know both, and know they are
inverses of one another up to the factor $g_0$.

### 6. Thrust vs. power — don't conflate them

**Thrust** is a force. **Power** delivered to the vehicle is thrust × flight velocity. A static engine
on a test stand produces thrust but delivers *zero* propulsive power to a vehicle. This is why
propulsive efficiency is zero at zero flight speed no matter how good the engine is, and it's the
seed of the whole efficiency discussion in [L06](L06-thermodynamics-of-jet-engines.md).

---

### 7. Propellers (§1.4 — assigned, and easy to overlook)

The book gives propellers their own section in Chapter 1, so they're fair game.

**A propeller is the extreme case of the §5 argument:** it accelerates an enormous mass of air by a
very small velocity increment. That's why propeller propulsive efficiency (0.85–0.90) beats every
turbofan — and why the turbofan is best understood as a propeller that has been ducted and slowed down
enough to work at high subsonic speed.

**The blade is a rotating wing.** The air approaches a blade section with a velocity that is the vector
sum of the **flight velocity $u$** (axial) and the **local blade speed $U = \omega r$** (tangential).
The relative approach velocity $W$ and its angle therefore **change along the span** — the tip sees far
more tangential velocity than the root.

$$
W = \sqrt{u^2 + (\omega r)^2}, \qquad \tan\phi = \frac{u}{\omega r}
$$

**This is why propeller blades are twisted**: to hold a sensible angle of attack at every radius when
the inflow angle $\phi$ varies from root to tip. It is exactly the same argument that twists compressor
and turbine blades ([velocity-triangles](../../concepts/velocity-triangles.md)) — the first appearance
in the course of a idea that recurs constantly.

**Two limits the book highlights:**

1. **Turning angle must stay small.** Ask a blade section for too much turning and the flow
   **separates**, just as in a compressor cascade ([L16](L16-compressors-3.md) §0). Same adverse
   pressure gradient, same consequence.
2. **Tip Mach number.** Since $W$ is largest at the tip, the tip approaches sonic conditions well
   before the aircraft does. Compressibility losses and noise rise sharply, which **caps useful
   propeller flight speed at roughly M 0.6–0.7.** Beyond that you must duct the fan and put a nacelle
   around it — i.e. build a turbofan.

**Swirl is unavoidable.** Applying torque to the airstream necessarily leaves a tangential velocity
component $u_\theta$ in the wake. That swirl is **wasted kinetic energy**, which is why contra-rotating
propellers and stator vanes behind ducted fans exist — to recover it.

---

## Key equations

### Uninstalled thrust (general air-breathing form)

$$
F = \dot{m}_e u_e - \dot{m}_a u_a + (p_e - p_a) A_e
$$

with $\dot m_a$ = air mass flow in, $\dot m_e = \dot m_a + \dot m_f$ = exhaust mass flow,
$u_a$ = flight (free-stream) velocity, $u_e$ = exhaust velocity, $A_e$ = nozzle exit area,
$p_e$/$p_a$ = exit and ambient static pressure.

Neglecting fuel flow ($\dot m_f \ll \dot m_a$) and for a perfectly expanded nozzle ($p_e = p_a$):

$$
F \approx \dot{m}_a (u_e - u_a)
$$

This is the form to carry in your head. **Thrust comes from the *change* in velocity, not the exhaust
velocity alone** — which is exactly why thrust decays as the aircraft speeds up.

### Rocket thrust

$$
F = \dot{m}_p u_e + (p_e - p_a) A_e \;\equiv\; \dot{m}_p \, c
$$

There is no incoming momentum term, because the propellant starts at rest relative to the vehicle.
$c$ is the **effective exhaust velocity**, which bundles the pressure term into an equivalent velocity.

### Specific impulse

$$
I_{sp} = \frac{F}{\dot{m}_p \, g_0} \qquad [\text{s}]
\qquad\Longleftrightarrow\qquad
c = I_{sp}\, g_0 \qquad [\text{m/s}]
$$

$$
g_0 = 9.80665 \ \mathrm{m/s^2}
$$

For an **air-breathing** engine, $\dot m_p$ is the *fuel* flow only:

$$
I_{sp,\text{air-breathing}} = \frac{F}{\dot{m}_f \, g_0}
$$

### Thrust-specific fuel consumption

$$
\mathrm{TSFC} = \frac{\dot{m}_f}{F}
\qquad\Longleftrightarrow\qquad
\mathrm{TSFC} = \frac{1}{I_{sp}\, g_0}
$$

SI units kg/(N·s); often quoted as lbm/(lbf·hr) in industry. **Check units on every problem** — this
is the single most common unit trap in the course.

### Propulsive power vs. thrust power

$$
P_{\text{propulsive}} = F \, u_a
$$

$$
P_{\text{jet, added}} = \tfrac{1}{2}\dot{m}\left(u_e^2 - u_a^2\right)
$$

The ratio of these two is propulsive efficiency — previewed here, derived in
[L06](L06-thermodynamics-of-jet-engines.md).

---

## Worked logic — why turbofans beat turbojets subsonically

You can get to the central design result of the course with only Lecture 1 material.

Hold the added kinetic energy (the fuel bill, roughly) fixed and ask what maximizes thrust:

$$
F = \dot{m}(u_e - u_a), \qquad
\dot{E} = \tfrac{1}{2}\dot{m}(u_e^2 - u_a^2) = \tfrac{1}{2}\dot{m}(u_e-u_a)(u_e+u_a)
$$

Divide:

$$
\frac{F}{\dot{E}} = \frac{2}{u_e + u_a}
$$

Thrust per unit energy expended is **maximized by making $u_e$ as close to $u_a$ as possible** — i.e.
a small velocity increment. But $F = \dot m (u_e - u_a)$ means a small increment needs a **large
$\dot m$** to keep thrust up.

**Conclusion: for a given thrust, move a lot of air slowly rather than a little air quickly.** That is
the entire argument for the turbofan, for high bypass ratio, and (taken to the limit) for the
propeller. It also explains why rockets — which cannot ingest mass — are stuck with high $u_e$ and low
propulsive efficiency in the atmosphere.

---

## Common pitfalls

- **"Thrust pushes against the air."** No. It's a momentum reaction; rockets work in vacuum.
- **Forgetting the ram drag term $\dot m_a u_a$.** Thrust is a *difference*. At high flight speed the
  incoming momentum flux is large and eats your thrust.
- **Dropping the pressure-thrust term when the nozzle isn't perfectly expanded.** It's only zero when
  $p_e = p_a$.
- **Comparing $I_{sp}$ across air-breathers and rockets as if it were an efficiency.** They use
  different denominators. A 3,000 s turbofan is not "10× better" than a 400 s rocket in any
  thermodynamic sense.
- **Unit soup in TSFC.** lbm/(lbf·hr) vs. kg/(N·s) differ by ~10⁵. Write units on every line.
- **Confusing $u_e$ (exhaust velocity, engine property) with $u_a$ (flight velocity, vehicle
  property).** Later chapters use station subscripts precisely to avoid this —
  see [station-numbering](../../concepts/station-numbering.md).

---

## Exam checklist

- [ ] State the general air-breathing thrust equation, all three terms, and say what each represents
- [ ] Reduce it to $F = \dot m(u_e - u_a)$ and state the two assumptions that permit it
- [ ] Write the rocket thrust equation and explain why the ram-drag term is absent
- [ ] Convert between $I_{sp}$, $c$, and TSFC in both unit systems
- [ ] Rank engine types by design Mach number and explain the trend (ram compression vs. machinery)
- [ ] Argue from $F/\dot E = 2/(u_e+u_a)$ why high bypass ratio improves fuel burn
- [ ] Explain why propulsive efficiency is zero on a static test stand

---

## Links

- Next: [L02 — Basic Concepts](L02-basic-concepts.md)
- Thrust equation done rigorously: [L06](L06-thermodynamics-of-jet-engines.md)
- Concept: [propulsion-efficiencies](../../concepts/propulsion-efficiencies.md)
- Concept: [station-numbering](../../concepts/station-numbering.md)
- Course hub: [EAS4300](../EAS4300.md)
