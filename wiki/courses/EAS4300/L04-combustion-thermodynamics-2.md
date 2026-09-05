# L04 — Combustion Thermodynamics 2

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 4 · **Date:** Mon 31 Aug 2026
**Book §:** 2.4 *Equilibrium Combustion Thermodynamics* — ✅ verified · **HW1 assigned**
**Tags:** #combustion #adiabatic-flame-temperature #dissociation #chemical-equilibrium #gibbs #equilibrium-constant #TIT #NOx #emissions

---

## Why this lecture matters

Lecture 3 counted the energy. This one asks: **how hot does the gas actually get, and why is the
answer always lower than the naive calculation?** The gap between the two — dissociation — is the
difference between a textbook answer and a real one, and turbine inlet temperature is *the* limiting
design parameter of the entire gas turbine.

---

## Core concepts

### 1. Adiabatic flame temperature (AFT)

Burn the mixture with **no heat loss** ($\dot Q = 0$) and **no work** ($\dot W_s = 0$). All the
chemical energy goes into raising the products' sensible enthalpy. The resulting temperature is the
**adiabatic flame temperature** — the theoretical maximum for that mixture and initial state.

From the reacting-flow first law:

$$
\sum_{\text{prod}} n_i \bar{h}_i(T_{ad}) = \sum_{\text{react}} n_j \bar{h}_j(T_{\text{in}})
$$

i.e. **total enthalpy of products = total enthalpy of reactants**. Expanded into formation + sensible
parts:

$$
\sum_{\text{prod}} n_i \left[\bar{h}_{f,i}^\circ + \Delta\bar{h}_{s,i}(T_{ad})\right]
= \sum_{\text{react}} n_j \left[\bar{h}_{f,j}^\circ + \Delta\bar{h}_{s,j}(T_{\text{in}})\right]
$$

**This is implicit in $T_{ad}$** — the unknown sits inside $\Delta\bar h_s(T_{ad})$, which is tabulated
or polynomial, not linear. Solving requires iteration (or a constant-$c_p$ approximation).

**Key dependencies:**
- **Rises** with reactant temperature $T_{\text{in}}$ (preheating helps, but less than 1:1)
- **Peaks near $\phi \approx 1$** (slightly rich), falls both lean and rich
- **Rises** with pressure (pressure suppresses dissociation — see §3)
- **Falls** with diluent (why air gives ~2,200 K and pure O₂ gives ~3,000 K+)

### 2. Constant-pressure vs. constant-volume AFT

Gas turbine and rocket combustors are essentially **constant pressure** (steady flow through a duct),
so the enthalpy balance above applies. A constant-**volume** explosion (piston engine knock, a closed
bomb calorimeter) conserves **internal energy** instead:

$$
\sum_{\text{prod}} n_i \bar{u}_i(T_{ad}) = \sum_{\text{react}} n_j \bar{u}_j(T_{\text{in}})
$$

$$
\bar{u} = \bar{h} - R_u T
$$

Constant-volume AFT is **higher**, because no flow work is done pushing products out against the
ambient. For this course, unless told otherwise, assume **constant pressure**.

### 3. Dissociation — why real flames are cooler

Above roughly **1,800 K**, product molecules start tearing apart. CO₂ and H₂O are not stable at flame
temperatures:

$$
\mathrm{CO_2} \rightleftharpoons \mathrm{CO} + \tfrac{1}{2}\mathrm{O_2}
$$

$$
\mathrm{H_2O} \rightleftharpoons \mathrm{H_2} + \tfrac{1}{2}\mathrm{O_2}
$$

$$
\mathrm{H_2O} \rightleftharpoons \mathrm{OH} + \tfrac{1}{2}\mathrm{H_2}
$$

plus $\mathrm{O_2} \rightleftharpoons 2\mathrm{O}$, $\mathrm{H_2} \rightleftharpoons 2\mathrm{H}$,
$\mathrm{N_2} + \mathrm{O_2} \rightleftharpoons 2\mathrm{NO}$.

Each of these is **endothermic in the forward direction** — it *absorbs* energy that would otherwise
have gone into sensible heat. Consequences:

- **AFT drops.** Complete-combustion calculations overpredict by **200–400 K** for hydrocarbon-air at
  1 atm; more at low pressure and high temperature.
- Dissociation acts as a **thermodynamic buffer** — it soaks up energy at high $T$ and releases it
  back on cooling (recombination in the nozzle, which partly recovers the loss).
- **Pressure suppresses dissociation.** Reactions like CO₂ → CO + ½O₂ increase the mole count, so by
  Le Chatelier's principle higher pressure pushes them back toward the associated side. This is one
  reason high-pressure rocket chambers run hotter and perform better.

### 4. Chemical equilibrium

At a given $T$ and $p$, a reacting mixture settles at the composition that **minimizes Gibbs free
energy**:

$$
G = H - TS, \qquad dG\big|_{T,p} = 0 \ \text{ at equilibrium}
$$

For a reaction $\;\nu_A A + \nu_B B \rightleftharpoons \nu_C C + \nu_D D$, this yields the
**equilibrium constant**:

$$
K_p = \frac{\left(p_C/p^\circ\right)^{\nu_C}\left(p_D/p^\circ\right)^{\nu_D}}
{\left(p_A/p^\circ\right)^{\nu_A}\left(p_B/p^\circ\right)^{\nu_B}}
$$

related to the standard Gibbs change by:

$$
\ln K_p = -\frac{\Delta G^\circ(T)}{R_u T}
$$

Written in mole fractions with $p_i = y_i p$:

$$
K_p = \left(\prod_i y_i^{\nu_i}\right)\left(\frac{p}{p^\circ}\right)^{\Delta \nu},
\qquad \Delta\nu = \sum_{\text{prod}}\nu - \sum_{\text{react}}\nu
$$

**Read that pressure exponent carefully — it's the whole story of §3.** If $\Delta\nu > 0$ (more moles
of products, as in dissociation), raising $p$ must *decrease* the product mole fractions to keep $K_p$
fixed. Dissociation is suppressed.

Temperature dependence (van 't Hoff):

$$
\frac{d\ln K_p}{dT} = \frac{\Delta H^\circ}{R_u T^2}
$$

Endothermic ($\Delta H^\circ > 0$) ⇒ $K_p$ rises with $T$ ⇒ **more dissociation as it gets hotter**.

### 5. Solving an equilibrium AFT problem

The full problem couples three things:
1. **Atom balances** — C, H, O, N are conserved regardless of speciation
2. **Equilibrium relations** — one $K_p$ per independent reaction
3. **Energy balance** — the adiabatic enthalpy equality

That's a nonlinear system solved numerically (NASA CEA, Cantera, or the textbook's charts). **In this
course you will most likely be asked to either (a) do a complete-combustion AFT by hand and iteration,
or (b) explain qualitatively how dissociation changes the answer** — not to solve the full coupled
system by hand. Know the structure; expect the exam to test understanding, not brute force.

### 6. The practical consequence: turbine inlet temperature

Everything above exists to set **$T_{04}$, the turbine inlet temperature (TIT)** — the single most
important design parameter in a gas turbine.

- Higher $T_{04}$ ⇒ more specific work, more thrust per unit airflow, better thermal efficiency
- But $T_{04}$ is capped by **turbine blade material limits**, not by combustion

Modern engines run $T_{04} \approx 1,700$–**2,000 K**, well **above** the melting point of the nickel
superalloys the blades are made from (~1,600 K). That's possible only through:
- **Film and internal cooling** with compressor bleed air (→ [L20](L20-turbines-2.md))
- **Thermal barrier coatings** (ceramic, low conductivity)
- **Single-crystal blades** (no grain boundaries to creep along)

And because AFT at $\phi \approx 1$ is ~2,300 K — hotter than any turbine can take — the combustor must
**dilute** rather than burn lean everywhere. See [L11](L11-combustors.md).

**The cost of cooling:** bleed air (typically 15–25% of core flow) bypasses the combustor, so it does
no work in the turbine and represents a real cycle penalty. Raising TIT is only worth it while the
gain exceeds the growing bleed cost.

---

## Key equations — summary

### AFT, constant-$c_p$ approximation

Useful for a fast estimate or a first iterate. Treat products as a single gas with mean $\bar c_p$:

$$
T_{ad} \approx T_{\text{in}} + \frac{f\, \eta_b\, Q_R}{(1+f)\,\bar{c}_p}
$$

Equivalently, for the burner in cycle analysis (the form you'll actually use):

$$
T_{04} = T_{03} + \frac{f\,\eta_b\, Q_R}{(1+f)\, c_{p,\text{hot}}}
$$

### Gibbs function and equilibrium

$$
\Delta G^\circ(T) = \sum_{\text{prod}} \nu_i \bar{g}_i^\circ(T) - \sum_{\text{react}} \nu_j \bar{g}_j^\circ(T)
$$

$$
K_p = \exp\left(-\frac{\Delta G^\circ}{R_u T}\right)
$$

### Entropy of a mixture (needed for Gibbs)

$$
\bar{s}_i(T,p_i) = \bar{s}_i^\circ(T) - R_u \ln\frac{p_i}{p^\circ}
= \bar{s}_i^\circ(T) - R_u \ln\left(\frac{y_i\,p}{p^\circ}\right)
$$

The $-R_u \ln y_i$ term is the **entropy of mixing** — it's what makes dissociation favorable at high
$T$ even though it costs enthalpy.

---

## Worked logic — estimating AFT for stoichiometric methane-air

**Step 1 — complete combustion, constant $c_p$ estimate.**
From [L03](L03-combustion-thermodynamics-1.md), stoichiometric CH₄ gives per mole of fuel:
1 CO₂ + 2 H₂O + 7.52 N₂ = **10.52 mol of products**, and $Q_R$ releases 802.3 kJ/mol CH₄.

Take a mean product molar $\bar c_p \approx 45$ J/(mol·K) at high temperature (products are
mostly N₂, but polyatomics CO₂/H₂O run higher; 45 is a reasonable blend):

$$
\Delta T \approx \frac{802{,}310\ \mathrm{J/mol}}{10.52\ \mathrm{mol} \times 45\ \mathrm{J/(mol\cdot K)}}
\approx 1{,}695\ \mathrm{K}
$$

$$
T_{ad} \approx 298 + 1{,}695 \approx 1{,}993\ \mathrm{K}
$$

**Step 2 — the real answer.** Proper tabulated $\Delta\bar h_s(T)$ with complete combustion gives
≈ **2,320 K** (the constant-$c_p$ estimate is crude because $c_p$ rises a lot over that range).
Including **dissociation**, the measured/CEA value is ≈ **2,225 K**.

**The ~100 K gap between 2,320 and 2,225 is dissociation** — energy sunk into breaking CO₂ and H₂O
apart instead of heating the gas. For hydrogen-oxygen or high-temperature rocket chambers the gap is
several hundred K and cannot be ignored.

**Step 3 — the engineering point.** 2,225 K at $\phi = 1$, versus a turbine that tolerates ~1,700–2,000 K.
The combustor must therefore run overall lean ($\phi \approx 0.25$, from
[L03](L03-combustion-thermodynamics-1.md)) — but a $\phi = 0.25$ mixture is below the lean flammability
limit and won't burn. Hence the staged combustor. The numbers on this page **are** the design driver.

### 7. NOₓ formation — dissociation as a pollutant, not just an energy sink (cross-referenced content)

Among the dissociation products in §3, $\mathrm{N_2 + O_2 \rightleftharpoons 2NO}$ deserves its own
mention: at flame temperature it forms in **trace but environmentally significant** amounts (10s–1,000s
of ppm), reacting downstream in the atmosphere toward smog and acid rain.

**The "frozen chemistry" problem.** $K_p$ for this reaction is small at typical combustor exit
temperatures (§4), so equilibrium NO would be tiny after cooling. But the reaction rate to **revert**
NO back to N₂/O₂ is slow compared to how fast gas cools through the turbine — so the NO formed at
*peak local flame temperature* gets kinetically **"locked in"** and survives to the exhaust in
concentrations well above what the *exit-temperature* equilibrium alone would predict. This is why
NOₓ control is fundamentally a **combustor design** problem (staged/lean-premixed combustion to avoid
ever reaching peak stoichiometric flame pockets — see [L11](L11-combustors.md)), not something that
can be fixed downstream.

---

## Worked logic — equilibrium NOₓ estimate

*Cross-referenced from a parallel offering's in-class problem.* $\mathrm{CH_2}$ (a simplified
hydrocarbon) burns with 30% excess air to a product temperature of 2,200 K at 1 atm. Estimate the
equilibrium NO mole fraction, given $K_p = e^{-6.866}$ at 2,200 K for $\mathrm{N_2+O_2 \rightleftharpoons 2NO}$.

**Step 1 — product composition without dissociation**, same method as L03: for $\mathrm{CH_2}$,
$\nu_{O_2,\text{stoich}} = 1+2/4=1.5$; with 30% excess, $\nu_{O_2,\text{supplied}}=1.95$,
$\nu_{O_2,\text{excess}}=0.45$, $\nu_{N_2}=1.95\times3.76=7.332$. Per mole of fuel: 1.0 mol CO₂,
1.0 mol H₂O, 0.45 mol O₂, 7.332 mol N₂ — total 9.782 mol, giving $y_{N_2}=0.750$, $y_{O_2}=0.046$.

**Step 2 — apply the equilibrium relation.** Since $\mathrm{N_2+O_2\to2NO}$ has
$\Delta\nu = 2-2=0$, the pressure-exponent term in §4's $K_p = K_n(p/p^\circ)^{\Delta\nu}$ **vanishes**
— a rare simplification — so $K_p=K_n$ directly, and:

$$
y_{NO} = \sqrt{K_p\, y_{N_2}\, y_{O_2}} = \sqrt{e^{-6.866}\times0.750\times0.046} \approx 0.0060
$$

**≈ 6,000 ppm** — far above typical regulatory limits, and a striking illustration that even a
reaction with vanishingly small $K_p$ ($e^{-6.866}\approx0.00104$) can produce environmentally
significant concentrations, because $N_2$ and $O_2$ themselves are so abundant in the products.

**The pattern to take from this**: whenever $\Delta\nu=0$ for a dissociation reaction, mole-fraction
and partial-pressure equilibrium constants coincide, which is what makes this particular NOₓ estimate
tractable by hand rather than requiring the full coupled solve described in §5.

---

## Common pitfalls

- **Reporting complete-combustion AFT as if it were real.** Always note dissociation lowers it, and by
  roughly how much.
- **Using a constant $c_p$ evaluated at 300 K.** $c_p$ of combustion products at 2,000 K is far higher
  than at room temperature. If you must use a constant, use a high-temperature mean.
- **Forgetting that AFT depends on inlet temperature.** Preheated air (compressor discharge at
  700–900 K) gives much higher AFT than 298 K air.
- **Getting the Le Chatelier direction backwards.** Higher pressure ⇒ **less** dissociation ⇒ higher
  $T_{ad}$.
- **Assuming higher TIT is free.** It costs cooling bleed, which is a cycle penalty.
- **Confusing $T_{ad}$ with $T_{04}$.** $T_{04}$ is the *diluted, mixed* combustor exit temperature and
  is far below the local flame temperature in the primary zone.
- **Using $K_p$ without the $(p/p^\circ)^{\Delta\nu}$ factor** when working in mole fractions.

---

## Exam checklist

- [ ] Set up the adiabatic flame temperature energy balance and explain why it's implicit in $T_{ad}$
- [ ] Explain physically why dissociation lowers AFT, and name the main dissociation reactions
- [ ] State and justify the pressure effect on dissociation via Le Chatelier / the $\Delta\nu$ exponent
- [ ] Relate $K_p$ to $\Delta G^\circ$; state the van 't Hoff temperature trend
- [ ] Explain the difference between constant-$p$ and constant-$V$ AFT and which applies here
- [ ] Estimate $T_{04}$ from $f$, $Q_R$, $\eta_b$, and $T_{03}$
- [ ] Explain why TIT is material-limited, how cooling raises the limit, and what it costs
- [ ] Explain why combustors are overall lean but locally near-stoichiometric

---

## Links

- Previous: [L03 — Combustion Thermodynamics 1](L03-combustion-thermodynamics-1.md)
- Next: [L05 — Gas Dynamics](L05-gas-dynamics.md)
- Where TIT bites: [L19 — Turbines 1](L19-turbines-1.md), [L20 — Turbines 2](L20-turbines-2.md)
- Hardware: [L11 — Combustors](L11-combustors.md)
- Rocket chamber version: [L23](L23-rocket-engines-1.md)
- Course hub: [EAS4300](../EAS4300.md)
