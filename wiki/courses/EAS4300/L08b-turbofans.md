# L08b — Turbofans

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 8 (part 2 of 2)
**Dates:** Mon 21 Sep, Wed 23 Sep 2026 · **HW3 assigned** 21 Sep
**Book §:** ⚠️ syllabus says **5.6**, but **§5.6 is "Turboprop and Turboshaft Engines."**
**Turbofans are §5.5** (p. 177). Read **5.5**.

> 📖 **Reconciled 2026-08-25.** The syllabus reference is off by one. §5.5 *Turbofan Engines* is the
> section this lecture is about; §5.6 covers turboprops and turboshafts, which appear nowhere else in
> the schedule. Either read 5.5 (near-certain intent) or, if the instructor meant it literally, 5.6
> adds turboprops — a topic this page touches only in passing.
> See [textbook-section-map](textbook-section-map.md).
**Tags:** #turbofan #bypass-ratio #fan-pressure-ratio #optimum-bypass #mixed-flow #separate-flow #geared-turbofan #propulsive-efficiency

---

## Why this lecture matters

The turbofan is **the** engine of modern aviation, and it exists for exactly one reason: the propulsive
efficiency argument from [L01](L01-introduction.md) and [L06](L06-thermodynamics-of-jet-engines.md).
The turbojet in [L08a](L08a-turbojets.md) achieved 36% propulsive efficiency at cruise. This lecture
shows how splitting the flow into two streams pushes that past 80%, and what it costs.

---

## Core concepts

### 1. The core idea

Extract **extra** work in the turbine — more than the compressor needs — and use it to drive a **fan**
that accelerates a large secondary (bypass) stream by a modest amount.

Result: the **same total thrust** from a **much larger mass flow** at a **much lower velocity increment**.
By the Froude relation $\eta_p = 2/(1+u_e/u_a)$, lower $u_e$ means higher $\eta_p$.

This is the concrete realization of the $F/\dot E = 2/(u_e+u_a)$ argument from
[L01](L01-introduction.md): *move a lot of air slowly, not a little air quickly.*

### 2. Bypass ratio — the defining parameter

$$
\alpha = B = \frac{\dot{m}_{\text{bypass}}}{\dot{m}_{\text{core}}} = \frac{\dot{m}_{19}}{\dot{m}_{9}}
$$

Total airflow:

$$
\dot{m}_{\text{total}} = \dot{m}_{\text{core}}(1+\alpha)
$$

**Historical progression — this table *is* the history of jet aviation:**

| Era | Engine | $\alpha$ | Notes |
|---|---|---|---|
| 1950s | J57 turbojet | 0 | Pure jet |
| 1960s | JT8D | 1.0 | Low bypass, 727/737-100 |
| 1970s | JT9D, CF6 | 5 | The widebody revolution |
| 1990s | GE90 | 9 | 777 |
| 2010s | GEnx, Trent 1000 | 10–11 | 787 |
| 2010s+ | PW1000G (geared) | 12+ | A320neo |
| Military | F110, F119 | 0.3–0.8 | Low bypass for specific thrust |

**Fighters use low bypass deliberately.** They need high specific thrust and small frontal area, and
they operate supersonically where high $u_e$ is appropriate. Airliners need fuel economy. Same physics,
opposite optimum.

### 3. Fan pressure ratio and the second knob

$$
\pi_f = \frac{p_{013}}{p_{02}}, \qquad
\tau_f = \frac{T_{013}}{T_{02}}
$$

$\alpha$ and $\pi_f$ are **not independent** — they're linked by the turbine work available. For a given
amount of extra turbine work you can either:
- accelerate **a lot** of air **a little** (high $\alpha$, low $\pi_f$), or
- accelerate **a little** air **a lot** (low $\alpha$, high $\pi_f$)

Typical modern values: $\pi_f \approx 1.4$–$1.7$ for high-bypass civil engines.

**The physical ceiling on $\pi_f$:** a single fan stage with $\pi_f > \sim1.8$ needs blade tip speeds
that go strongly transonic, bringing shock losses and noise (→ [L18](L18-transonic-fan-stage.md)).
So high bypass ratio is the practical route to low $u_e$.

### 4. Separate-flow vs. mixed-flow

**Separate-flow (unmixed):** the two streams exhaust through separate nozzles. Standard for high-bypass
civil engines — simpler, lighter, and the streams have very different pressures and temperatures anyway.

$$
F = \dot{m}_c\left[(1+f)u_9 - u_0\right] + \dot{m}_b\left[u_{19}-u_0\right] + \text{pressure terms}
$$

Per unit **core** flow:

$$
\frac{F}{\dot{m}_c} = \left[(1+f)u_9 - u_0\right] + \alpha\left[u_{19}-u_0\right]
$$

**Mixed-flow:** streams merge in a mixer before a single nozzle. Used for low-bypass military engines
(needed anyway if there's an afterburner) and some business jets. Gains a small thrust benefit from
mixing to a uniform state, and reduces noise, but adds weight, length, and mixing pressure loss.

**Requirement for mixing:** static pressures must be nearly matched at the mixer,
$p_{13} \approx p_{5}$, which constrains $\pi_f$ relative to the core.

**A concrete size of the "small thrust benefit"** (cross-referenced from a prior Anup Mannem-taught
offering): at BPR=8, comparing exhaust at matched exit pressure but different temperatures (core hot,
bypass cool), mixing to a common exit velocity before expansion gives $F_{\text{mixed}}/F_{\text{unmixed}}
\approx 1.008$ — **under 1% more thrust**. The real reason mixed-flow architectures exist is rarely
this sliver of thrust; it's the **noise reduction** (mixing the high-velocity core jet down before it
meets ambient air softens the shear-layer noise source — [L06](L06-thermodynamics-of-jet-engines.md))
and, for military engines, that an afterburner needs a single duct anyway.

### 5. The optimum fan pressure ratio

For a given $\alpha$ and available turbine work, thrust is maximized when the two streams have
**equal exhaust velocities**:

$$
u_9 = u_{19} \qquad \text{(optimum, ideal case)}
$$

**Why:** for fixed total energy, thrust $\sum \dot m_i(u_i - u_0)$ is maximized by distributing the
velocity increment evenly. Any imbalance wastes energy in the faster stream (KE scales as $u^2$ while
thrust scales as $u$).

Real engines run slightly *off* this optimum — the core stream is typically a bit faster — because of
nozzle losses, mixing considerations, and the mass/weight of a larger fan.

**The optimum bypass ratio** for given $\tau_\lambda$, $\pi_c$, $\pi_f$, and flight condition comes from
setting $\partial(F/\dot m)/\partial\alpha = 0$. Qualitatively:

$$
\alpha_{\text{opt}} \ \uparrow \quad\text{as}\quad \tau_\lambda \uparrow,\ \ \pi_c \uparrow,\ \ M_0 \downarrow
$$

- **Hotter core (higher TIT)** ⇒ more surplus work ⇒ can drive a bigger fan
- **Lower flight Mach** ⇒ lower $u_0$ ⇒ lower optimum $u_e$ ⇒ bigger fan
- **Supersonic flight** ⇒ small or zero optimum bypass ⇒ **turbojet**

Again the continuum: **ramjet ← turbojet ← low-bypass ← high-bypass ← turboprop**, ordered by
decreasing design Mach number.

### 6. Ideal separate-flow turbofan analysis

**Fan stream (2 → 13 → 19):**

$$
T_{013} = T_{02}\tau_f, \qquad p_{013} = p_{02}\pi_f
$$

Perfectly expanded:

$$
M_{19}^2 = \frac{2}{\gamma-1}\left[\left(\frac{\pi_r \pi_f p_0}{p_0}\right)^{\frac{\gamma-1}{\gamma}}-1\right]
= \frac{2}{\gamma-1}\left[\left(\pi_r\pi_f\right)^{\frac{\gamma-1}{\gamma}}-1\right]
$$

$$
u_{19} = M_{19}\sqrt{\gamma R T_{19}}, \qquad
T_{19} = \frac{T_0\tau_r\tau_f}{1+\frac{\gamma-1}{2}M_{19}^2}
$$

**Core stream:** identical to [L08a](L08a-turbojets.md), **except the turbine work balance now includes
the fan**:

$$
c_p\left(T_{04}-T_{05}\right) = c_p\left(T_{03}-T_{02}\right) + \alpha\, c_p\left(T_{013}-T_{02}\right)
$$

In ratio form — **the single most important equation in this lecture**:

$$
\tau_t = 1 - \frac{\tau_r}{\tau_\lambda}\left[\left(\tau_c-1\right) + \alpha\left(\tau_f-1\right)\right]
$$

Compare with the turbojet's $\tau_t = 1 - (\tau_r/\tau_\lambda)(\tau_c-1)$. **The $\alpha(\tau_f-1)$ term
is the whole turbofan.** It's the extra work the turbine must produce, and it's why $T_{05}$ and
$p_{05}$ are lower than a turbojet's — the core jet is weaker by design.

**Total specific thrust** (per unit total airflow, which is what sizes the engine):

$$
\frac{F}{\dot{m}_{\text{total}}} = \frac{1}{1+\alpha}\left[(1+f)u_9 - u_0\right]
+ \frac{\alpha}{1+\alpha}\left[u_{19}-u_0\right]
$$

**TSFC:**

$$
\mathrm{TSFC} = \frac{\dot m_f}{F} = \frac{f}{(1+\alpha)\left(F/\dot m_{\text{total}}\right)}
$$

### 7. What high bypass costs

The trade is not free, and exam questions love the downsides:

- **Specific thrust drops hard.** Turbojet ~900 N·s/kg vs. high-bypass turbofan ~250 N·s/kg. You need
  3–4× the airflow for the same thrust.
- **Fan diameter grows.** GE90 fan is 3.25 m across — comparable to a 737 fuselage. Nacelle drag and
  weight scale with it, and eventually the drag penalty eats the fuel saving. This is the practical
  ceiling on $\alpha$, around 12–15.
- **Ground clearance and installation.** Larger nacelles force longer landing gear or pylon
  compromises. The 737 MAX's handling issues trace ultimately to fitting big-fan engines under a low
  wing designed in the 1960s.
- **Fan/LP-turbine speed mismatch.** A big fan wants to turn *slowly* (tip speed limit); an LP turbine
  wants to turn *fast* (to be efficient with few stages). On a direct-drive shaft, both are stuck at the
  same speed and both are compromised.
- **Poor high-Mach performance.** At supersonic speed the bypass stream contributes little and the
  large frontal area is pure drag.

### 8. The geared turbofan

The fan/turbine speed mismatch has a direct fix: put a **reduction gearbox** (≈3:1) between the LP
turbine and the fan.

**Gains:** fan turns slowly (good tip speed, quiet, efficient); LP turbine turns fast (fewer stages,
lighter). Enables $\alpha > 12$ with a shorter, lighter LP turbine.

**Costs:** the gearbox must transmit tens of megawatts continuously with ~99.5% efficiency; the ~0.5%
loss is real heat that must be rejected, requiring a dedicated oil cooling system. Weight, complexity,
and certification burden are substantial.

The PW1000G family put this into production after decades of development — a good illustration that
the physics was never in doubt; the mechanical engineering was.

### 9. Noise — an underrated driver

Jet mixing noise scales approximately as:

$$
\text{Acoustic power} \propto u_e^8
$$

**An eighth power.** Halving exhaust velocity cuts jet noise by ~24 dB. High-bypass turbofans are
dramatically quieter than turbojets almost entirely because of this scaling, not because of acoustic
treatment (though liners and chevrons help). Airport noise regulations have been as strong a driver of
bypass ratio as fuel price.

---

## Worked logic — turbofan vs. turbojet, matched conditions

Same conditions as [L08a](L08a-turbojets.md): $M_0 = 0.85$, $T_0 = 220$ K, $\pi_c = 20$ (core),
$T_{04} = 1600$ K, plus $\alpha = 8$, $\pi_f = 1.6$. Ideal components, $\gamma = 1.4$,
$c_p = 1005$ J/(kg·K).

**Step 1 — ram (unchanged):**

$$
\tau_r = 1.1445, \qquad \pi_r = 1.604, \qquad T_{02}=251.8\ \mathrm{K}, \qquad a_0 = 297\ \mathrm{m/s},\ u_0 = 252\ \mathrm{m/s}
$$

**Step 2 — fan:**

$$
\tau_f = (1.6)^{0.2857} = 1.1435
\quad\Longrightarrow\quad T_{013} = 251.8\times1.1435 = 287.9\ \mathrm{K}
$$

$$
M_{19}^2 = 5\left[(1.604\times1.6)^{0.2857}-1\right] = 5\left[(2.566)^{0.2857}-1\right] = 5(1.3089-1)=1.545
$$

$$
M_{19}=1.243, \qquad T_{19} = \frac{287.9}{1+0.2(1.545)} = \frac{287.9}{1.309}=219.9\ \mathrm{K}
$$

$$
u_{19} = 1.243\sqrt{1.4\times287\times219.9} = 1.243\times297.2 = 369\ \mathrm{m/s}
$$

**Step 3 — core, with the fan load in the work balance:**

$$
\tau_c = 2.354\ \text{(as before)}, \qquad \tau_\lambda = 7.273
$$

$$
\tau_t = 1 - \frac{1.1445}{7.273}\left[(2.354-1) + 8(1.1435-1)\right]
= 1 - 0.15736\left[1.354 + 1.148\right]
$$

$$
\tau_t = 1 - 0.15736(2.502) = 1-0.3937 = 0.6063
$$

$$
T_{05} = 1600\times0.6063 = 970\ \mathrm{K}, \qquad \pi_t = (0.6063)^{3.5}=0.1716
$$

$$
\frac{p_{05}}{p_0} = 1.604\times20\times0.1716 = 5.505
$$

$$
M_9^2 = 5\left[(5.505)^{0.2857}-1\right]=5(1.6236-1)=3.118, \qquad M_9 = 1.766
$$

$$
T_9 = \frac{970}{1+0.2(3.118)}=\frac{970}{1.6236}=597.4\ \mathrm{K}
$$

$$
u_9 = 1.766\sqrt{1.4\times287\times597.4}=1.766\times489.9=865\ \mathrm{m/s}
$$

**Step 4 — thrust and efficiency.** With $f \approx 0.0249$ (as in L08a):

$$
\frac{F}{\dot m_{\text{total}}} = \frac{1}{9}\left[(1.0249)(865)-252\right] + \frac{8}{9}\left[369-252\right]
$$

$$
= \frac{1}{9}(886.5-252) + \frac{8}{9}(117) = 70.5 + 104.0 = 174.5\ \mathrm{N\cdot s/kg}
$$

$$
\mathrm{TSFC} = \frac{f}{(1+\alpha)(F/\dot m_{\text{total}})} = \frac{0.0249}{9 \times 174.5}
= 1.585\times10^{-5}\ \mathrm{kg/(N\cdot s)}
$$

**Comparison:**

| | Turbojet (L08a) | Turbofan ($\alpha=8$) |
|---|---|---|
| Specific thrust (per total airflow) | 893 N·s/kg | 175 N·s/kg |
| TSFC | 2.79×10⁻⁵ | 1.59×10⁻⁵ |
| Core jet velocity $u_9$ | 1145 m/s | 865 m/s |
| Bypass jet velocity | — | 369 m/s |

**TSFC improves by ~43%** — the turbofan burns well under two-thirds the fuel for the same thrust.
**Specific thrust falls by ~80%**, meaning ~5× the airflow and a vastly larger engine.

That is the entire trade, in two numbers. Fuel is expensive and size is affordable on a transport
aircraft, so the turbofan wins. On a fighter, size and frontal area are life-or-death and fuel is a
secondary concern, so low bypass wins.

**Note the two streams aren't velocity-matched here** (865 vs. 369 m/s), so this design is off the §5
optimum — a real engine at $\alpha = 8$ would use a somewhat higher $\pi_f$ or lower $\pi_c$ to close
that gap.

**Independent cross-check, US customary units** (cross-referenced from a parallel offering — same
qualitative comparison, different flight condition and route: efficiency triad instead of specific
thrust/TSFC). At 0.85 $M$/40,000 ft, $\mathrm{OPR}=30$, $T_4=2{,}600°\mathrm F$, matched core between a
turbojet ($\mathrm{BPR}=0$) and a turbofan ($\mathrm{FPR}=1.5$, $\mathrm{BPR}=5$):

| | Turbojet | Turbofan ($\mathrm{BPR}=5$) |
|---|---|---|
| Core exit velocity $V_e$ | 3,834 ft/s | 3,272 ft/s (core) |
| Fan exit velocity | — | 1,131 ft/s |
| TSFC | 1.02 lbm/(lbf·hr) | 0.78 lbm/(lbf·hr) |
| Thermal efficiency $\eta_{th}$ | 0.57 | 0.64 |
| Propulsive efficiency $\eta_p$ | 0.35 | 0.71 |
| Overall efficiency $\eta_o$ | **0.20** | **0.45** |

**Same conclusion as the SI example, from the efficiency side rather than the specific-thrust side**:
adding a BPR-5 fan to an identical core **more than doubles overall efficiency** (0.20→0.45) and cuts
TSFC by ~24%, almost entirely through the **propulsive efficiency** jump (0.35→0.71) — thermal
efficiency barely moves (0.57→0.64), because it's set mostly by $\mathrm{OPR}$ and $T_4$, which are
identical for both engines here. **This is the cleanest possible illustration of the
[propulsion-efficiencies](../../concepts/propulsion-efficiencies.md) decomposition**: the core sets
$\eta_{th}$; the bypass architecture sets $\eta_p$; and it's $\eta_p$ that the turbofan is really
buying.

---

## Common pitfalls

- **Forgetting the fan term in the turbine work balance.** $\alpha(\tau_f-1)$ is the entire point.
- **Using $\dot m_{\text{core}}$ where $\dot m_{\text{total}}$ belongs (or vice versa).** State your basis
  explicitly on every specific-thrust number — this is the single most common turbofan error.
- **Applying $\pi_c$ to the total flow.** The compressor sees only the core stream.
- **Assuming the fan pressure ratio applies to the core too.** In most architectures the core flow
  passes through the fan root *and then* the compressor, so the core's total pressure ratio is
  $\pi_f \times \pi_c$. Read the problem's definition carefully.
- **Assuming higher $\alpha$ is always better.** Nacelle drag, weight, and installation eventually
  dominate.
- **Ignoring that the core jet is weaker in a turbofan.** More turbine work extracted ⇒ lower $p_{05}$.
- **Forgetting bypass-stream pressure thrust** if its nozzle is choked.
- **Dropping $g_c$ in the specific-thrust formula when working in US customary (imperial) units.**
  A real instructor correction on this exact point (cross-referenced): the textbook's specific-thrust
  formula $F_s = (1+f)\dot m_{\text{core}}V_{e,\text{core}} + \mathrm{BPR}\cdot\dot m\, V_{e,\text{fan}}
  - (1+\mathrm{BPR})\dot m\, V_0$ is written in a mixed unit system where **every velocity term must be
  divided by $g_c=32.174\ \mathrm{lbm\cdot ft/(lbf\cdot s^2)}$** to come out in lbf, not just left as
  lbm·ft/s². Omitting it is invisible in SI (where $g_c\equiv1$) but silently wrong by a factor of ~32
  in imperial units — always check that a "specific thrust" answer in lbf/(lbm/s) is a plausible
  number (tens to low hundreds), not off by an order of magnitude.

---

## Exam checklist

- [ ] Define bypass ratio and write total flow in terms of core flow
- [ ] Derive $\tau_t = 1-(\tau_r/\tau_\lambda)[(\tau_c-1)+\alpha(\tau_f-1)]$
- [ ] Write separate-flow specific thrust per total airflow, and TSFC
- [ ] Explain why $u_9 = u_{19}$ maximizes thrust for given energy
- [ ] State how $\alpha_{opt}$ varies with TIT, $\pi_c$, and $M_0$, with reasons
- [ ] Explain the fan/LP-turbine speed mismatch and how a gearbox resolves it
- [ ] List at least four costs of high bypass ratio
- [ ] Explain the $u_e^8$ noise scaling and its regulatory consequence
- [ ] Compare turbojet and turbofan on specific thrust and TSFC, and say which aircraft picks which

---

## Links

- Previous: [L08a — Turbojets](L08a-turbojets.md)
- Next: [L09 — Engine/Aircraft Performance](L09-engine-aircraft-performance.md)
- Fan aerodynamics: [L18 — Transonic Fan Stage](L18-transonic-fan-stage.md)
- Efficiency theory: [L06](L06-thermodynamics-of-jet-engines.md), [propulsion-efficiencies](../../concepts/propulsion-efficiencies.md)
- Course hub: [EAS4300](../EAS4300.md)
