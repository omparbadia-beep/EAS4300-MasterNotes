# L03 — Combustion Thermodynamics 1

**Course:** EAS 4300 Aerospace Propulsion · **Syllabus topic:** 3 · **Date:** Fri 28 Aug 2026
**Book §:** 2.4 *Equilibrium Combustion Thermodynamics* — ✅ verified
**Tags:** #combustion #stoichiometry #fuel-air-ratio #equivalence-ratio #heating-value #enthalpy-of-formation #first-law-reacting

---

## Why this lecture matters

The combustor is where the energy enters the engine. Everything downstream — turbine inlet
temperature, cycle efficiency, thrust — is set by how much heat you can release and how hot you're
willing to let the gas get. This lecture builds the **accounting system** for chemical energy: how much
fuel goes with how much air, and how much enthalpy that releases. Lecture 4 uses that accounting to
find the resulting temperature.

---

## Core concepts

### 1. Stoichiometry — the bookkeeping of atoms

A **stoichiometric** mixture has exactly enough oxidizer to convert all fuel to fully oxidized
products (CO₂ and H₂O) with nothing left over. Balance atoms, not molecules.

For a general hydrocarbon $\mathrm{C}_x\mathrm{H}_y$ burning in air, with air modeled as
**1 mol O₂ + 3.76 mol N₂** (the standard approximation — 79/21 = 3.76):

$$
\mathrm{C}_x\mathrm{H}_y + a\left(\mathrm{O}_2 + 3.76\,\mathrm{N}_2\right)
\;\longrightarrow\; x\,\mathrm{CO}_2 + \frac{y}{2}\,\mathrm{H}_2\mathrm{O} + 3.76a\,\mathrm{N}_2
$$

Balancing oxygen:

$$
a = x + \frac{y}{4}
$$

Nitrogen is carried through as inert **diluent** — it absorbs a large share of the released energy,
which is precisely why flame temperatures in air are ~2,200 K rather than the ~5,000 K you'd get in
pure oxygen. (At high temperature N₂ is *not* truly inert — it forms NOₓ — but that's a pollutant
question, not an energy-balance one.)

### 2. Fuel-air ratio and equivalence ratio

Two ratios, constantly confused, both essential.

**Fuel-air ratio $f$** is a mass ratio, and it's the one that shows up in every cycle equation as
$\dot m_e = \dot m_a (1+f)$:

$$
f = \frac{\dot{m}_{\text{fuel}}}{\dot{m}_{\text{air}}}
$$

**Equivalence ratio $\phi$** normalizes $f$ against stoichiometric, making it dimensionless and
fuel-independent:

$$
\phi = \frac{f}{f_{\text{stoich}}}
= \frac{(\text{fuel/air})_{\text{actual}}}{(\text{fuel/air})_{\text{stoich}}}
$$

| $\phi$ | Name | Character |
|---|---|---|
| $\phi < 1$ | **Lean** | Excess air. Cooler, complete burn, excess O₂ in products. |
| $\phi = 1$ | **Stoichiometric** | Near-maximum flame temperature. |
| $\phi > 1$ | **Rich** | Excess fuel. Cooler, incomplete burn, CO and H₂ in products, soot. |

**Key result worth internalizing:** peak flame temperature occurs slightly **rich** of
stoichiometric ($\phi \approx 1.05$), not exactly at $\phi = 1$. Rich mixtures produce more moles of
lighter products and dissociation is slightly suppressed, which nudges the peak over. Both lean and
rich sides fall off from the peak.

**Gas turbine reality:** the *overall* combustor equivalence ratio is very lean, $\phi \approx 0.2$–$0.3$
($f \approx 0.015$–$0.025$), because the turbine cannot survive a stoichiometric flame. But a
$\phi = 0.25$ mixture won't sustain a flame at all. The resolution — burning near $\phi \approx 1$ in a
small primary zone, then diluting hard — is the central design idea of [L11](L11-combustors.md).

### 3. Heating values

The **heating value** is the energy released per unit mass of fuel burned completely, with products
returned to the reactants' temperature.

- **Higher heating value (HHV):** water in products counted as **liquid** — includes the latent heat
  of vaporization.
- **Lower heating value (LHV):** water counted as **vapor**.

**In propulsion, always use LHV.** Exhaust leaves the nozzle hot; the water never condenses, so that
latent heat is never recovered. LHV is often written $Q_R$, $h_{PR}$, or $\Delta h_c$.

$$
Q_{R,\text{Jet-A}} \approx 43\ \mathrm{MJ/kg}
\qquad
Q_{R,\mathrm{H_2}} \approx 120\ \mathrm{MJ/kg}
$$

Hydrogen's ~2.8× advantage **per unit mass** is why it's perennially attractive for aerospace — and
its terrible density is why it's rarely adopted. Compare on a per-*volume* basis and it loses badly.

### 3b. Real jet fuels (cross-referenced content)

*Cross-referenced against a parallel offering's lecture — worth knowing the actual fuel names, since
exam problems and industry discussion use them freely.*

Jet fuels are complex mixtures of hundreds of hydrocarbons (paraffins, cycloparaffins, aromatics),
approximated for calculation as a single formula like Jet-A ≈ $\mathrm{C}_{11.4}\mathrm{H}_{21.7}$.

| Fuel | Character |
|---|---|
| **Jet-A / Jet A-1** | Kerosene-based, the civil standard. Jet A-1 has a lower freeze point (−47°C) for long-haul/cold-soak flights. |
| **JP-8** | Military kerosene-based, essentially Jet A-1 plus additives (icing inhibitor, corrosion inhibitor, anti-static). High stability. |
| **JP-5** | Naval — a **higher flash point** than JP-8 for shipboard fire safety, similar thermochemistry otherwise. |
| **JP-4** | Older military fuel, a wide-cut (naphtha + kerosene) blend — **more volatile**, lower flash point. Mostly phased out for JP-8. |

### 4. Enthalpy of formation — why reacting flows need a new datum

For non-reacting flow you can set $h=0$ anywhere; only differences matter. In a reacting flow the
chemical species *change*, so every substance must be referenced to a **common datum**.

Convention: the **enthalpy of formation** $\bar h_f^\circ$ is the enthalpy change to form one mole of
a species from its **elements in their stable reference state** at the standard state
(298.15 K, 1 atm). By definition, stable elemental forms — O₂, N₂, H₂, C(graphite) — have
$\bar h_f^\circ = 0$.

The total (**absolute**) molar enthalpy of a species at temperature $T$:

$$
\bar{h}(T) = \bar{h}_f^\circ + \left[\bar{h}(T) - \bar{h}(298\ \mathrm{K})\right]
\;\equiv\; \bar{h}_f^\circ + \Delta \bar{h}_s(T)
$$

**chemical energy + sensible (thermal) energy.** This split is the whole trick: combustion converts
the first term into the second.

Useful values (kJ/mol at 298 K):

| Species | $\bar h_f^\circ$ |
|---|---|
| CO₂(g) | −393.52 |
| H₂O(g) | −241.83 |
| H₂O(l) | −285.83 |
| CO(g) | −110.53 |
| CH₄(g) | −74.87 |
| O₂, N₂, H₂, C(s) | 0 |

The H₂O(g) vs. H₂O(l) difference, −241.83 vs. −285.83, is exactly the 44 kJ/mol latent heat that
separates LHV from HHV.

### 5. First law for a reacting flow

Apply the SFEE from [L02](L02-basic-concepts.md) to a combustor, with the crucial modification that
enthalpies are now **absolute** (formation + sensible):

$$
\dot{Q} - \dot{W}_s = \sum_{\text{prod}} \dot{n}_i \bar{h}_i - \sum_{\text{react}} \dot{n}_j \bar{h}_j
$$

For a combustor there is **no shaft work**, so $\dot W_s = 0$, and the equation reduces to a balance
between heat removed and the enthalpy difference between products and reactants.

Two limiting cases define the two lectures:
- **Products returned to reactant temperature** → $\dot Q$ = heat of reaction (this lecture).
- **$\dot Q = 0$ (adiabatic)** → products get as hot as possible = adiabatic flame temperature
  ([L04](L04-combustion-thermodynamics-2.md)).

### 6. Combustion efficiency and how heat release enters the cycle

Real combustors don't release 100% of the chemical energy — incomplete combustion, unburned
hydrocarbons, CO, and heat loss through the liner all take a cut.

$$
\eta_b = \frac{\text{actual heat released}}{\dot{m}_f\, Q_R}
$$

Modern gas turbine combustors run $\eta_b = 0.98$–$0.99+$ at design point (much worse at altitude
relight or idle). The **energy balance across the burner**, which you'll use in every cycle analysis
from [L07](L07-ramjets.md) onward:

$$
\dot{m}_f \, \eta_b \, Q_R = \dot{m}_a (1+f)\, c_{p,\text{hot}} T_{04} - \dot{m}_a\, c_{p,\text{cold}} T_{03}
$$

Divide by $\dot m_a$ and solve for $f$:

$$
f = \frac{c_{p,\text{hot}} T_{04} - c_{p,\text{cold}} T_{03}}
{\eta_b Q_R - c_{p,\text{hot}} T_{04}}
$$

A frequently used simplification with a single $c_p$:

$$
f \approx \frac{c_p (T_{04}-T_{03})}{\eta_b Q_R - c_p T_{04}}
$$

**Do not forget the $-c_p T_{04}$ in the denominator.** It accounts for the fact that the fuel mass
itself must also be heated to $T_{04}$. Dropping it is a standard error worth a couple of points every
time.

---

## Key equations — summary

### Stoichiometric air-fuel ratio by mass

For $\mathrm{C}_x\mathrm{H}_y$ with $a = x + y/4$:

$$
\left(\frac{A}{F}\right)_{\text{stoich}}
= \frac{a\,(32 + 3.76 \times 28)}{12x + 1.008y}
= \frac{137.3\,a}{12x + 1.008y}
$$

$$
f_{\text{stoich}} = \left(\frac{A}{F}\right)^{-1}_{\text{stoich}}
$$

Benchmarks: **Jet-A / kerosene** $\approx \mathrm{C}_{12}\mathrm{H}_{23}$,
$(A/F)_{\text{stoich}} \approx 14.7$, $f_{\text{stoich}} \approx 0.068$.
Methane: $(A/F) \approx 17.2$. Hydrogen: $(A/F) \approx 34.3$.

### Heat of reaction (constant pressure, products at reactant temperature)

$$
\Delta H_R = \sum_{\text{prod}} n_i \bar{h}_{f,i}^\circ - \sum_{\text{react}} n_j \bar{h}_{f,j}^\circ
$$

$$
Q_R = \frac{-\Delta H_R}{m_{\text{fuel}}}
$$

Negative $\Delta H_R$ = exothermic. $Q_R$ is defined positive.

### Mixture properties

Mole fraction and mass fraction:

$$
y_i = \frac{n_i}{n_{\text{tot}}}, \qquad
Y_i = \frac{m_i}{m_{\text{tot}}} = \frac{y_i M_i}{\sum_j y_j M_j}
$$

Mixture molar mass and gas constant:

$$
M_{\text{mix}} = \sum_i y_i M_i, \qquad
R_{\text{mix}} = \frac{R_u}{M_{\text{mix}}}, \qquad
R_u = 8.314\ \mathrm{J/(mol\cdot K)}
$$

Mixture specific heat (mass-weighted):

$$
c_{p,\text{mix}} = \sum_i Y_i\, c_{p,i}
$$

Dalton's law of partial pressures:

$$
p_i = y_i\, p
$$

---

## Worked logic — burning methane in air

Balance CH₄ at stoichiometric ($x=1$, $y=4$, so $a = 1 + 4/4 = 2$):

$$
\mathrm{CH_4} + 2(\mathrm{O_2} + 3.76\,\mathrm{N_2})
\longrightarrow \mathrm{CO_2} + 2\,\mathrm{H_2O} + 7.52\,\mathrm{N_2}
$$

Air-fuel ratio by mass:

$$
\left(\frac{A}{F}\right)_{\text{stoich}}
= \frac{2 \times 4.76 \times 28.85}{16.04} \approx 17.1
\;\Longrightarrow\;
f_{\text{stoich}} \approx 0.0584
$$

Heat of reaction, using $\bar h_f^\circ$ values with **H₂O as vapor** (gives LHV):

$$
\Delta H_R = \left[(-393.52) + 2(-241.83)\right] - \left[(-74.87) + 0\right]
= -802.31\ \mathrm{kJ/mol\ CH_4}
$$

$$
Q_R = \frac{802.31\ \mathrm{kJ/mol}}{0.01604\ \mathrm{kg/mol}} \approx 50.0\ \mathrm{MJ/kg}
$$

which matches the tabulated LHV of methane. Repeat with H₂O(l) at −285.83 and you get 55.5 MJ/kg —
the HHV. **The only difference is the phase of the product water.**

### Sanity check on a gas turbine fuel-air ratio

Take $T_{03} = 700$ K (compressor exit), $T_{04} = 1600$ K (turbine inlet), $Q_R = 43$ MJ/kg,
$\eta_b = 0.98$, and a single $c_p = 1100$ J/(kg·K):

$$
f \approx \frac{1100(1600-700)}{0.98 \times 43\times10^6 - 1100 \times 1600}
= \frac{9.9\times 10^5}{4.214\times10^7 - 1.76\times10^6} \approx 0.0245
$$

Compare to $f_{\text{stoich}} \approx 0.068$: $\phi \approx 0.36$. **Deeply lean overall** — exactly as
argued in §2, and exactly why combustors need a staged primary/dilution architecture.

---

## Worked logic — adiabatic combustion of Jet-A with excess air

*Cross-referenced from a parallel offering's in-class problem — a full numeric working of §5's
reacting-flow energy balance, in the mixed-unit (BTU, °R, lb-mole) system common in US industry
practice. Good practice converting the SI-flavored derivation above into these units.*

**Given:** air at 300°F mixes with Jet-A ($\mathrm{C}_{11.4}\mathrm{H}_{21.7}$, $M_f\approx158.5$
lb/lb-mole, LHV $=18{,}550$ Btu/lb) at **20% excess air**. Find the product composition and adiabatic
flame temperature.

**Step 1 — stoichiometric oxygen and air**, from §1's $a=x+y/4$:

$$
\nu_{O_2,\text{stoich}} = 11.4+\frac{21.7}{4}=16.825\ \text{lb-mol } O_2 \text{ per lb-mol fuel}
$$

$$
\text{Air}_{\text{stoich}} = \nu_{O_2,\text{stoich}}\times 4.76 = 80.1\ \text{lb-mol air per lb-mol fuel}
$$

**Step 2 — with 20% excess air**, per lb-mol of fuel:

$$
\nu_{O_2,\text{supplied}} = 1.2\times16.825=20.19, \qquad
\nu_{O_2,\text{excess}}=20.19-16.825=3.365
$$

$$
\nu_{N_2}=20.19\times3.76=75.9
$$

**Product composition** (per lb-mol Jet-A): $\mathrm{CO_2}=11.40$, $\mathrm{H_2O(g)}=10.85$
(= $21.7/2$), $\mathrm{O_2}=3.365$, $\mathrm{N_2}=75.90$ — all lb-mol.

**Step 3 — energy balance**, exactly §5's $\dot Q=0$ statement, worked with a single mean $c_p$ per
species rather than integrated enthalpy tables:

$$
Q_{\mathrm{LHV}} = 18{,}550\times158.5 \approx 2{,}939{,}700\ \mathrm{Btu/lb\text{-}mol\ fuel}
$$

Reactant sensible enthalpy above the 77°F reference ($\Delta T = 300-77=223°\mathrm R$), using
$c_p\approx8.12$ (O₂), $7.54$ (N₂), $12.4$ (liquid fuel), Btu/(lb-mol·°R):

$$
\bar c_{p,\text{react}} = 20.19(8.12)+75.9(7.54)+1(12.4) \approx 748.3\ \mathrm{Btu/(lb\text{-}mol\cdot{}^\circ R)}
$$

$$
\Delta h_{\text{react}} = 748.3\times223 \approx 167{,}000\ \mathrm{Btu/lb\text{-}mol}
$$

Product sensible-enthalpy capacity, using $c_p\approx8.12$ (CO₂), $9.70$ (H₂O(g)), $8.12$ (O₂),
$7.54$ (N₂):

$$
\bar c_{p,\text{prod}} = 11.40(8.12)+10.85(9.70)+3.365(8.12)+75.9(7.54) \approx 797.2\ \mathrm{Btu/(lb\text{-}mol\cdot{}^\circ R)}
$$

**Step 4 — solve for $T_{ad}$:**

$$
T_{ad}-T_{\text{ref}} = \frac{Q_{\mathrm{LHV}}+\Delta h_{\text{react}}}{\bar c_{p,\text{prod}}}
= \frac{2{,}939{,}700+167{,}000}{797.2} \approx 3{,}897°\mathrm R
$$

$$
T_{ad} \approx 536.7+3{,}897 = 4{,}437°\mathrm R \approx 3{,}977°\mathrm F
$$

**This is the [L04](L04-combustion-thermodynamics-2.md) complete-combustion overprediction, in
concrete numbers.** Real dissociation and temperature-varying $c_p$ pull the actual flame temperature
down to roughly **3,300–3,600°F** — a **~400–700°F correction**, on the high end of the
"200–400 K" figure quoted in L04 §3, because this is a genuinely near-stoichiometric mixture ($\phi$
is close to 1, unlike the gas-turbine-overall example above).

---

## Common pitfalls

- **Confusing $f$ with $\phi$.** $f$ is dimensional (mass/mass); $\phi$ is normalized. Cycle equations
  take $f$; combustion charts take $\phi$.
- **Using HHV.** Always LHV in propulsion.
- **Forgetting nitrogen.** It's 3.76 mol per mol O₂ and it carries most of the products' heat capacity.
- **Dropping $-c_p T_{04}$ from the $f$ denominator.**
- **Using $\gamma=1.4$ for the products.** Post-combustion gas is hot and has $\gamma \approx 1.33$.
- **Assuming peak flame temperature is exactly at $\phi=1$.** It's slightly rich.
- **Mixing molar and mass bases mid-problem.** Formation enthalpies are per *mole*; heating values and
  $f$ are per *mass*. Convert deliberately and write units.

---

## Exam checklist

- [ ] Balance a hydrocarbon-air combustion equation and compute $a$, $(A/F)_{\text{stoich}}$, $f_{\text{stoich}}$
- [ ] Define $\phi$ and classify lean/stoichiometric/rich, with the products expected in each
- [ ] State why LHV, not HHV, is used
- [ ] Explain the formation + sensible enthalpy decomposition and why a common datum is required
- [ ] Compute a heat of reaction from a table of $\bar h_f^\circ$
- [ ] Derive $f$ from the combustor energy balance, including the $-c_p T_{04}$ term
- [ ] Explain why gas turbine combustors are overall lean but locally near-stoichiometric

---

## Links

- Previous: [L02 — Basic Concepts](L02-basic-concepts.md)
- Next: [L04 — Combustion Thermodynamics 2](L04-combustion-thermodynamics-2.md) (adiabatic flame temperature, dissociation)
- Hardware realization: [L11 — Combustors](L11-combustors.md)
- Afterburner version: [L12](L12-afterburners-ramjet-combustors.md)
- Course hub: [EAS4300](../EAS4300.md)
