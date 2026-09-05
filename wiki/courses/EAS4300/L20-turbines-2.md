# L20 — Axial Turbines 2: Efficiency, Losses, and Cooling

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 20 · **Date:** Fri 30 Oct 2026
**Book §:** 8.4 *Rotor Blade and Disc Stresses* (p. 384) · 8.5 *Blade Cooling* (p. 393) — ✅ verified

> 📖 **Reconciled 2026-08-25.** §8.5 Blade Cooling is covered thoroughly below (§4–§7). But **§8.4 is
> "Rotor Blade and Disc Stresses"** — a *mechanical* section on centrifugal stress, the $AN^2$
> parameter, disc design, and creep life. That was the thinnest part of this page, so **a new §0
> covers it properly.**
>
> Note that §8.3 Stage Efficiency (the reheat/polytropic material in §1–§2 below) is assigned to
> [L19](L19-turbines-1.md), not here. See [textbook-section-map](textbook-section-map.md).
**Tags:** #turbine-efficiency #reheat-effect #blade-cooling #film-cooling #thermal-barrier-coating #single-crystal #creep #tip-leakage #secondary-flow #total-to-total

---

## Why this lecture matters

Turbine inlet temperature is the single most valuable parameter in a gas turbine
([L04](L04-combustion-thermodynamics-2.md)), and modern engines run it **above the melting point of the
blade material**. That is only possible through cooling — and cooling costs cycle performance. This
lecture is where that trade is quantified, along with turbine loss mechanisms and the correct
efficiency definitions.

---

## Core concepts

### 0. Rotor blade and disc stresses (§8.4 — the assigned section)

**The turbine is the most mechanically brutal component in the engine:** the hottest gas, the highest
stress, and the tightest life requirement, simultaneously. §8.4 is about why blade speed $U$ — the
thing every velocity triangle wants to maximize — is capped by structures, not aerodynamics.

#### Centrifugal stress and the $AN^2$ parameter

A rotating blade carries its own weight outward. For an **untapered** blade of uniform cross-section
spanning hub radius $r_h$ to tip $r_t$, the tensile stress at the root is:

$$
\sigma_{c} = \rho_b\,\omega^2\,\frac{r_t^2 - r_h^2}{2}
$$

with $\rho_b$ the **blade material** density (not gas density). Now substitute the annulus area
$A = \pi\left(r_t^2 - r_h^2\right)$ and $\omega = 2\pi N$ with $N$ in **revolutions per second**:

$$
\boxed{\ \sigma_c = 2\pi\,\rho_b\,A\,N^2\ }
$$

**This is the famous $AN^2$ result, and it deserves a moment.** Root stress depends on the annulus
area and rotational speed *only* — **not on blade height, chord, or aspect ratio separately.** So:

- $AN^2$ is a single number that tells you whether a turbine stage is mechanically feasible
- **You cannot get more flow area without paying in stress**, at fixed speed
- Wanting higher $U$ (better aerodynamics, fewer stages) and wanting larger $A$ (more mass flow)
  are in **direct competition**, and $AN^2$ is the referee

**Tapering the blade** — thinner at the tip, since the tip carries no outboard mass — relieves the root:

$$
\sigma_c = 2\pi\,\rho_b\,A\,N^2\,K_t, \qquad K_t \approx 0.5\text{–}0.7
$$

Typical turbine blade root centrifugal stress lands around **150–250 MPa**, on top of which sit gas
bending loads, thermal stress, and vibratory stress.

#### Why this couples to temperature — the real bind

Stress alone would be manageable. **Stress at 1,200 K is not.** Nickel superalloys lose strength
rapidly with temperature, and the failure mode isn't yield — it's **creep**, slow time-dependent
extension under sustained load.

Design criterion is typically *"stress that produces no more than 1% creep extension in 100,000 hours
at temperature."* Creep life is correlated by the **Larson–Miller parameter**:

$$
\mathrm{LMP} = T\left(C + \log_{10} t\right), \qquad C \approx 20
$$

with $T$ in K (or °R) and $t$ in hours. Curves of allowable stress vs. LMP collapse a whole family of
time-temperature combinations onto one line.

**The consequence to internalize: LMP depends on $\log t$ but on $T$ linearly.** So temperature
dominates overwhelmingly. A rule of thumb from the correlation — **a ~15–20 K increase in metal
temperature can halve blade life.** That single sentence explains why:

- cooling ([§4–§7 below](#4-the-cooling-problem)) is worth its considerable cycle cost
- **turbine blade temperature is controlled far more tightly than any other engine parameter**
- EGT margin is the parameter airlines actually manage an engine's life around
  ([L25](L25-testing-performance-characteristics.md))

#### Disc stresses

The blades hang off a **disc**, which carries both the blade pull and its own rotational load. The disc
sees **radial** and **hoop** stresses, with the hoop stress peaking at the bore. Because the bore is
thick and slow to heat, discs also see large **transient thermal stress** during acceleration — the
rim heats fast while the bore lags, a major driver of **low-cycle fatigue** and the reason engine life
is counted in *cycles* (takeoffs) as well as hours.

Classic disc profiles, in increasing sophistication:

| Profile | Character |
|---|---|
| **Constant thickness** | Simple, heavy, high bore stress |
| **Hyperbolic** | Thickness falls with radius; better stress distribution |
| **Constant-stress (de Laval) disc** | Exponentially tapered so stress is uniform — lightest for a given duty |

Blades attach through **fir-tree roots**, whose multiple lobes spread the enormous pull over several
bearing surfaces while still allowing assembly and thermal growth.

#### The design loop this creates

$$
\text{want high } U \;\to\; \text{high } \sigma_c \;\to\; \text{need stronger/cooler blade}
\;\to\; \text{more cooling bleed} \;\to\; \text{cycle penalty}
$$

**Aerodynamics, heat transfer, and structures are not separable in a turbine.** That is the actual
takeaway of §8.4–8.5 together, and it's a likely conceptual exam question.

### 1. Total-to-total vs. total-to-static efficiency

**A definitional distinction that gets examined and is easy to get wrong.**

**Total-to-total** — appropriate when the **exit kinetic energy is useful** (e.g. an HP turbine feeding
an LP turbine, or an LP turbine feeding a nozzle):

$$
\eta_{tt}=\frac{h_{00}-h_{02}}{h_{00}-h_{02s}}=\frac{T_{00}-T_{02}}{T_{00}-T_{02s}}
$$

**Total-to-static** — appropriate when the **exit KE is wasted** (e.g. the last stage of a stationary
power turbine exhausting to atmosphere):

$$
\eta_{ts}=\frac{h_{00}-h_{02}}{h_{00}-h_{2s}}
$$

**Always $\eta_{ts} < \eta_{tt}$**, because the total-to-static denominator includes the exit kinetic
energy as available-but-lost work. The gap is large when exit velocity is high.

**In aero engines, use total-to-total** for all stages — exit KE always feeds either the next stage or
the nozzle. Get this wrong and your numbers are systematically off.

### 2. Polytropic efficiency and the reheat effect — sign flips from compressors

$$
\eta_{p,t}=\frac{\ln\tau_t}{\frac{\gamma-1}{\gamma}\ln\pi_t}
$$

$$
\tau_t = \pi_t^{\frac{(\gamma-1)\eta_{p,t}}{\gamma}}
$$

**The crucial contrast with [L15](L15-compressors-2.md):**

| | Compressor | Turbine |
|---|---|---|
| Losses heat the gas... | before the *next compression* | before the *next expansion* |
| Effect on downstream stages | **Harmful** (preheat — more work needed) | **Helpful** (reheat — more work available) |
| Relationship | $\eta_c < \eta_p$ | **$\eta_t > \eta_p$** |
| Gap grows with | Pressure ratio | Pressure ratio |

**The reheat effect explained:** losses in an early turbine stage appear as heat in the gas. That
hotter gas enters the next stage, which — because constant-pressure lines diverge on a $T$-$s$
diagram — can extract *more* work from the same pressure ratio. Some of the loss is recovered.

**So a multistage turbine's overall isentropic efficiency exceeds any individual stage's.** This is the
mirror image of the compressor's preheat penalty and is a favorite short-answer question. Getting the
direction backwards is a common error.

**Example:** $\eta_p = 0.90$, $\gamma = 1.33$:

| $\pi_t$ (expansion) | $\eta_t$ |
|---|---|
| 2 | 0.906 |
| 4 | 0.913 |
| 8 | 0.919 |

### 3. Turbine loss mechanisms

Similar categories to compressors ([L15](L15-compressors-2.md)) but with different weights and one
addition:

| Loss | Share | Notes |
|---|---|---|
| **Profile loss** | ~30% | Boundary layers and wakes. *Lower* than a compressor's because the favorable gradient keeps BLs thin. |
| **Secondary/endwall** | ~35% | **The dominant turbine loss.** Large turning ⇒ strong passage vortices. |
| **Tip leakage** | ~25% | Driven by the pressure difference across the rotor |
| **Cooling/mixing loss** | ~10%+ | **Unique to turbines** — injecting cooling air disturbs the main flow |
| **Trailing edge** | few % | TE thickness is large because cooling air must exit there |

**Secondary flows dominate** because turbine blades turn the flow 70–120°. The endwall boundary layer
has low momentum, so the same blade-to-blade pressure gradient over-turns it dramatically, rolling it
into strong **passage vortices** plus horseshoe and corner vortices. This is why endwall contouring and
blade lean/bow matter so much in turbines.

**Tip leakage.** Unshrouded HP blades (shrouds can't survive the stress and temperature) leak over the
tip driven by the rotor pressure difference. Mitigations: **squealer tips** (a thin raised rim that acts
as a labyrinth restriction and can rub away safely), and **shrouding** on cooler LP stages where the
stress allows it. Note that an **impulse** stage ($R=0$) has no pressure difference across the rotor and
therefore minimal leakage — one of its genuine advantages
([L19](L19-turbines-1.md) §5).

**Zweifel criterion** — optimum blade spacing, balancing profile loss (fewer blades = less wetted area)
against loading (fewer blades = each must do more turning):

$$
Z = \frac{2s}{c_x}\cos^2\alpha_2\left(\tan\alpha_1 + \tan\alpha_2\right) \approx 0.8
$$

### 4. The cooling problem

**The core fact:** modern TIT is **1,700–2,000 K**; nickel superalloys soften around **1,300 K** and melt
near **1,600 K**. The gas is hotter than the melting point of the metal. The blade survives only because
it is continuously cooled.

**Why the gain is worth it** — from [L06](L06-thermodynamics-of-jet-engines.md), specific work scales
with TIT. Roughly:

- **+100 K of TIT ⇒ ~10–15% more specific thrust**
- Over the jet age, TIT has risen ~500 K, roughly doubling specific thrust

**Where the capability came from** (each contributes ~100–200 K):

| Technology | Gain |
|---|---|
| **Convection cooling** (internal passages) | ~100 K |
| **Impingement cooling** (jets onto the inner wall, esp. leading edge) | ~100 K |
| **Film cooling** (air ejected to form a protective layer) | ~200 K |
| **Thermal barrier coating (TBC)** | ~100–150 K |
| **Single-crystal casting** | ~50–100 K (via allowable metal temperature) |

### 5. Cooling technologies in detail

**Internal convection.** Serpentine passages inside the blade with turbulators (**trip strips**/ribs)
and **pin fins** near the thin trailing edge to enhance heat transfer.

**Impingement cooling.** Jets of air directed onto the inside of the wall. Very high local heat transfer
coefficient — used at the **leading edge**, where the external heat load is highest (stagnation point).

**Film cooling.** Air ejected through rows of shaped holes forms an insulating film over the external
surface.
- **Most effective single technique**, but the **most disruptive** to the main flow
- Shaped (fan/diffuser) holes spread the film with less penetration and mixing loss than cylindrical
  holes
- **Film effectiveness:**

$$
\eta_f = \frac{T_g - T_{aw}}{T_g - T_c}
$$

with $T_g$ the mainstream gas, $T_{aw}$ the adiabatic wall temperature, $T_c$ the coolant.

**Transpiration cooling.** Porous wall, uniform coolant seepage. Theoretically the most effective, but
the pores clog with combustion products and oxidation. Not in production use.

**Thermal barrier coatings (TBC).** A ceramic layer (typically yttria-stabilized zirconia, ~100–300 μm)
with very low thermal conductivity, over a metallic bond coat. Sustains a 100–150 K drop across itself.
The failure mode is **spallation** — thermal-expansion mismatch causes the ceramic to flake off, after
which the metal is exposed.

**Materials and casting:**
- **Equiaxed** castings have grain boundaries in all directions — the weak paths for **creep**
- **Directionally solidified (DS)** — grains aligned along the spanwise (centrifugal load) direction,
  eliminating transverse boundaries
- **Single crystal (SX)** — **no grain boundaries at all.** Since creep occurs preferentially at grain
  boundaries, removing them raises the usable temperature substantially. Modern HP blades are
  essentially all single crystal.

### 6. The cost of cooling — the trade that matters

Cooling air is **compressor bleed**, and it is expensive in three separate ways:

1. **It bypasses the combustor**, so it doesn't get heated and doesn't contribute its share of turbine
   work
2. **It was compressed**, so the compressor work spent on it is largely wasted
3. **Mixing loss** — injecting it back into the main flow at a different velocity and temperature
   generates entropy

**Typical bleed:** 15–25% of core flow for a modern HP turbine.

**Approximate net effect:**

$$
\Delta\eta_{\text{cycle}} \approx -0.3\ \text{to}\ -0.5\%\ \text{per 1\% of bleed}
$$

**Therefore raising TIT is only worth it while the specific-work gain exceeds the growing bleed
penalty.** There is a genuine optimum, and it moves upward as cooling technology improves. This is why
TIT has risen steadily rather than jumping — each increment required cooling advances to stay on the
right side of the trade.

**A subtlety worth knowing:** in cycle analysis, cooled turbines are sometimes characterized with a
"**cooled efficiency**" that lumps the mixing and thermodynamic penalties together, or with the
**rotor inlet temperature (RIT)** rather than the combustor exit temperature — since the cooling air
mixes in before the rotor, RIT is lower than $T_{04}$. Check which definition a problem intends.

### 7. Creep, oxidation, and blade life

**Creep** — time-dependent plastic deformation under stress at high temperature. The **life-limiting**
failure mode for HP blades. Centrifugal stress at the root plus 1,300 K metal temperature means the
blade slowly elongates until it rubs the casing.

**Larson-Miller parameter** — the standard way to trade temperature against time:

$$
\mathrm{LMP} = T\left(C + \log_{10} t_r\right)
$$

with $T$ in kelvin (or rankine), $t_r$ rupture time in hours, and $C \approx 20$ for many superalloys.
Constant LMP means equivalent damage — so **a modest temperature increase costs enormous life**. A rule
of thumb: **+15 K of metal temperature halves blade life.** That number explains why turbine
temperature control and TBC integrity are treated so seriously.

**Other degradation modes:**
- **Oxidation and hot corrosion** — sulfidation from fuel sulfur and ingested salt
- **Thermal fatigue** — cycling between idle and takeoff cracks coatings and blade surfaces
- **Erosion** — sand and dust ingestion, a serious issue in desert operation

---

## Worked logic — cooling bleed and the net cycle benefit

**Question:** an engine currently runs $T_{04}=1600$ K with 12% cooling bleed. Increasing TIT to
1,750 K requires 20% bleed. Is it worth it?

**Step 1 — specific work gain from higher TIT.** Turbine specific work scales roughly with $T_{04}$:

$$
\frac{\Delta w}{w}\approx \frac{1750-1600}{1600}=9.4\%
$$

**Step 2 — bleed penalty.** Bleed rises from 12% to 20%, an increase of 8 percentage points. At
0.4% cycle efficiency loss per point:

$$
\Delta\eta_{\text{cycle}} \approx -8 \times 0.4\% = -3.2\%
$$

Additionally, the 8% of flow that now bypasses the combustor doesn't produce turbine work:

$$
\text{effective work loss} \approx 8\% \times (\text{fraction of work it would have done}) \approx 4\text{–}5\%
$$

**Step 3 — net:**

$$
\text{Net specific work gain} \approx +9.4\% - 4.5\% \approx +4.9\%
$$

$$
\text{Net efficiency change} \approx +2\text{–}3\%\ \text{(from higher cycle temperature)} - 3.2\% \approx -0.5\ \text{to}\ +0\%
$$

**Conclusion: marginal.** The specific thrust gain is real (~5%), which helps a **fighter** where engine
size dominates. The fuel efficiency gain is roughly a wash, which means it's **not** obviously
worthwhile for a **transport** unless cooling technology improves so that 1,750 K needs less than 20%
bleed.

**This is exactly the calculation that drives turbine cooling R&D** — the goal isn't higher TIT per se,
it's *achieving a given TIT with less bleed*. Better film-hole shaping, TBCs, and single-crystal alloys
all move the same lever.

**Step 4 — sanity check on blade life.** If the metal temperature rises with the gas temperature and the
cooling doesn't fully compensate, then by the +15 K rule:

$$
\text{150 K rise, uncompensated} \Rightarrow \text{life reduced by } 2^{150/15}=2^{10}\approx 1000\times
$$

**A thousandfold life reduction.** The cooling must therefore hold metal temperature essentially
*constant* while gas temperature rises 150 K — which is precisely why 8 more points of bleed are
needed. The two halves of this problem are the same problem.

---

## Worked logic — stress-constrained tip speed, then stage work and mass flow

*Cross-referenced from a parallel offering — starts from §0's stress limit and, unusually, works
**forward** to find the maximum allowable tip speed, then chains into a full stage-work and mass-flow
calculation. A good end-to-end review of L19 + L20 together.*

**Given:** allowable root stress $\sigma=150$ MPa, blade material density $\rho_b=8{,}200$ kg/m³,
hub/tip radius ratio $\zeta=r_{\text{root}}/r_{\text{tip}}=0.9$, tip diameter $=0.75$ m, 50% reaction,
$T_1=1{,}300$ K, $\gamma=1.3$, $R=0.287$ kJ/(kg·K), nozzle exit swirl $\alpha_2=68°$, zero swirl at
rotor exit ($\beta_3=\alpha_3=0$).

**Step 1 — max tip speed from the stress limit**, rearranging §0's $AN^2$-equivalent relation
(here expressed via hub/tip ratio $\zeta$ rather than annulus area, but the same physics):

$$
\sigma = \rho_b\,\frac{U_{\text{tip}}^2}{2}\left(1-\zeta^2\right)
\;\Rightarrow\;
U_{\text{tip}} = \sqrt{\frac{2\sigma}{\rho_b\left(1-\zeta^2\right)}}
= \sqrt{\frac{2(150\times10^6)}{8{,}200(1-0.81)}} = 439\ \mathrm{m/s}
$$

$$
\Omega = \frac{U_{\text{tip}}}{r_{\text{tip}}} = \frac{439}{0.375} = 1{,}170\ \mathrm{rad/s}
\;\Rightarrow\;
N = 1{,}170\times\frac{60}{2\pi} = 11{,}180\ \mathrm{RPM}
$$

**This is the practical use of the $AN^2$/stress relation**: given a material limit, it directly caps
the shaft speed — every other cycle parameter must live within that constraint.

**Step 2 — work coefficient at the mean radius.** For **zero exit swirl** ($\alpha_3=0$, all the swirl
imparted by the nozzle is fully extracted by the rotor — the ideal, no-wasted-KE case from
[propulsion-efficiencies](../../concepts/propulsion-efficiencies.md)'s Froude argument, applied here to
the turbine stage):

$$
\psi = \frac{\Delta h_0}{U^2} = 1 \quad (\text{zero-swirl condition, a standard simplification})
$$

$$
r_{\text{mean}} = \frac{r_{\text{root}}+r_{\text{tip}}}{2} = 0.95\,r_{\text{tip}}
\;\Rightarrow\;
U_m = U_{\text{tip}}\times0.95 = 417\ \mathrm{m/s}
$$

$$
\Delta h_0 = U_m^2 = 174\ \mathrm{kJ/kg}, \qquad
\Delta T_0 = \frac{\Delta h_0}{c_p} = \frac{174}{1.244} = 140\ \mathrm{K}
$$

**Step 3 — isentropic pressure ratio and mass flow**, chaining through the same isentropic and
continuity relations as [L02](L02-basic-concepts.md):

$$
T_3 = T_1-\Delta T_0 = 1{,}160\ \mathrm K, \qquad
\frac{P_3}{P_1} = \left(\frac{T_3}{T_1}\right)^{\gamma/(\gamma-1)} = 0.611
$$

Working the velocity triangle at the mean radius with zero exit swirl
($C_{a} = U_m/(\tan\alpha_2-\tan\beta_2)$, here simplified since $\beta_2=0$ at the mean line in this
idealization) gives $C_a = 168$ m/s, $C_2=450$ m/s, from which static conditions and density follow
($\rho_2 \approx 6.5$ kg/m³), and finally:

$$
\dot m = \rho_2 A_2 C_a, \qquad A_2 = \pi r_{\text{tip}}^2\left(1-\zeta^2\right) = 0.084\ \mathrm{m^2}
\;\Rightarrow\; \dot m \approx 91.6\ \mathrm{kg/s}
$$

**The end-to-end chain to internalize**: a **material stress limit** → caps **shaft speed** → sets
**blade speed** at every radius → fixes the **velocity triangles** (L19) → gives **stage work** → gives
**mass flow capacity** (via continuity). Nothing here is optional or independently chosen — a turbine
stage design is one fully coupled calculation, not a sequence of unrelated lookups.

---

## Common pitfalls

- **Using total-to-static where total-to-total belongs** (or vice versa). Aero engines: total-to-total.
- **Getting the reheat direction backwards.** Turbine: $\eta_t > \eta_p$. Compressor: $\eta_c < \eta_p$.
- **Applying compressor loss weightings to a turbine.** Secondary flow dominates in turbines.
- **Forgetting cooling/mixing loss.** It's a turbine-specific loss category.
- **Assuming higher TIT is free.** It costs bleed, which costs cycle performance.
- **Confusing $T_{04}$ with rotor inlet temperature.** Cooling air mixing lowers RIT below $T_{04}$.
- **Thinking single-crystal blades are stronger in tension.** The benefit is **creep** resistance via
  eliminating grain boundaries.
- **Underestimating the life sensitivity.** +15 K halves life.
- **Ignoring that impulse stages have less tip leakage** (no rotor pressure difference).

---

## Exam checklist

- [ ] Define $\eta_{tt}$ and $\eta_{ts}$ and state when each applies
- [ ] **Explain the reheat effect and why $\eta_t > \eta_p$ for turbines**
- [ ] Contrast reheat with the compressor's preheat effect
- [ ] List turbine loss mechanisms with shares; explain why secondary flow dominates
- [ ] Explain tip leakage and why impulse stages suffer less
- [ ] State the Zweifel criterion and what it balances
- [ ] **Explain how TIT can exceed the blade melting point** — list the cooling technologies
- [ ] Describe convection, impingement, film, and transpiration cooling
- [ ] Explain TBCs and their failure mode
- [ ] Explain equiaxed vs. DS vs. single crystal in terms of creep
- [ ] **State the three ways cooling bleed costs performance and quantify the trade**
- [ ] Write the Larson-Miller parameter and use the +15 K life rule

---

## Links

- Previous: [L19 — Turbines 1](L19-turbines-1.md)
- Next: [L21 — Turbines 3](L21-turbines-3.md) — maps and matching
- Where TIT is set: [L04 — Combustion Thermodynamics 2](L04-combustion-thermodynamics-2.md)
- Combustor exit profile: [L11 — Combustors](L11-combustors.md)
- Compressor efficiency counterpart: [L15 — Compressors 2](L15-compressors-2.md)
- Course hub: [EAS4300](../EAS4300.md)
