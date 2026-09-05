# Corrected Parameters

**Type:** cross-cutting concept
**Used in:** [EAS4300](../courses/EAS4300.md) — L09, L16, L21, L25
**Tags:** #corrected-parameters #theta-delta #compressor-map #similarity #dimensional-analysis #testing

---

## What they are

Non-dimensional-ish groupings that collapse an engine's performance so **one map covers every flight
condition**. Without them, you'd need a separate compressor map for every altitude and every ambient
temperature.

**Reference conditions** (standard sea-level day):

$$
\theta = \frac{T_{02}}{288.15\ \mathrm{K}}, \qquad \delta = \frac{p_{02}}{101.325\ \mathrm{kPa}}
$$

**The corrected quantities:**

$$
\dot m_{\text{corr}}=\frac{\dot m\sqrt\theta}{\delta}, \qquad
N_{\text{corr}}=\frac{N}{\sqrt\theta}
$$

$$
F_{\text{corr}}=\frac{F}{\delta}, \qquad
\dot m_{f,\text{corr}}=\frac{\dot m_f}{\delta\sqrt\theta}, \qquad
\mathrm{TSFC}_{\text{corr}}=\frac{\mathrm{TSFC}}{\sqrt\theta}
$$

**Note the TSFC correction is $1/\sqrt\theta$, not $1/\delta$** — a very common slip. It follows from
TSFC $=\dot m_f/F$ with $\dot m_f\propto\delta\sqrt\theta$ and $F\propto\delta$.

---

## Why they work — the physical reading

Don't memorize them as dimensional analysis. Read them as **Mach numbers**:

**$\dot m\sqrt\theta/\delta$ is the flow function** — essentially the Mach number at the compressor
face. From [L05](../courses/EAS4300/L05-gas-dynamics.md) §4:

$$
\frac{\dot m\sqrt{T_0}}{p_0 A}=\sqrt{\frac{\gamma}{R}}\,M\left(1+\frac{\gamma-1}{2}M^2\right)^{-\frac{\gamma+1}{2(\gamma-1)}}
$$

**Same corrected flow ⇒ same $M$ at the face ⇒ same axial velocity ratio.**

**$N/\sqrt\theta$ is the blade Mach number.** Since $a = \sqrt{\gamma R T}$:

$$
\frac{U}{a}=\frac{\omega r}{\sqrt{\gamma R T_{02}}} \propto \frac{N}{\sqrt{T_{02}}}
$$

**Same corrected speed ⇒ same $U/a$ ⇒ same blade Mach.**

**Together, the two fix the velocity triangles** ([velocity-triangles](velocity-triangles.md)). Same
triangles ⇒ same aerodynamics ⇒ same $\pi_c$ and $\eta_c$:

$$
\pi_c,\ \eta_c = \mathrm{fn}\left(\dot m_{\text{corr}},\ N_{\text{corr}}\right)
$$

**That's the whole theorem.** It's similarity, not magic.

---

## Where they get used

### 1. Component maps

Compressor and turbine maps are **always** plotted in corrected quantities
([L16](../courses/EAS4300/L16-compressors-3.md), [L21](../courses/EAS4300/L21-turbines-3.md)).
Using raw values on a map is meaningless.

### 2. Choked-turbine matching

The choked turbine NGV gives:

$$
\frac{\dot m\sqrt{T_{04}}}{p_{04}}=\text{constant}
$$

**This single relation sets the compressor's operating line**
([L21](../courses/EAS4300/L21-turbines-3.md)). It's the most consequential application of the idea in
the course.

### 3. Altitude testing

An altitude test cell conditions inlet air to the flight $T_{02}$ and $p_{02}$ and pumps the exhaust to
the flight $p_a$. **Matching $\theta$ and $\delta$ on the ground reproduces the flight aerodynamic
state exactly** ([L25](../courses/EAS4300/L25-testing-performance-characteristics.md)). This is the
practical payoff of the whole framework.

### 4. Thrust lapse

Corrected thrust $F/\delta$ is nearly a function of $N_{corr}$ alone, so:

$$
F \approx \delta \times \mathrm{fn}\left(\frac{N}{\sqrt\theta}\right)
$$

Thrust falls with altitude essentially because $\delta$ falls
([L09](../courses/EAS4300/L09-engine-aircraft-performance.md)).

---

## Hot-day and altitude behavior

| Condition | $\theta$ | $\delta$ | Effect |
|---|---|---|---|
| **Altitude** | ↓ slightly | **↓↓** | Thrust falls with $\delta$; aerodynamics preserved |
| **Hot day** | **↑** | ~ | $N_{corr}$ falls at same physical $N$ ⇒ less corrected flow, lower $\pi_c$, less thrust |
| **Cold day** | ↓ | ~ | $N_{corr}$ rises ⇒ more thrust, but risk of hitting $N$ or $p_{03}$ limits |
| **High Mach** | ↑ (ram) | ↑ (ram) | Both rise; net effect depends on engine type |

**Flat rating** is the standard response to hot-day lapse: the engine is derated so it holds constant
thrust up to a reference ambient temperature, protecting TIT and blade life
([L20](../courses/EAS4300/L20-turbines-2.md)) at the cost of hot-day takeoff performance.

---

## Common errors

- **Using uncorrected values on a map.**
- **Correcting TSFC by $\delta$ instead of $\sqrt\theta$.**
- **Using free-stream $T_0$, $p_0$ instead of station-2 values.** $\theta$ and $\delta$ are referenced to
  the **compressor face**, which includes inlet recovery $\pi_d$.
- **Using compressor reference conditions for turbine corrected flow.** Reference to $T_{04}$, $p_{04}$.
- **Forgetting that corrected parameters preserve *aerodynamics*, not absolute values.** Corrected thrust
  is the same; actual thrust is not.

---

## Links

- [L16 — Compressors 3](../courses/EAS4300/L16-compressors-3.md) — maps, main treatment
- [L21 — Turbines 3](../courses/EAS4300/L21-turbines-3.md) — matching
- [L25 — Testing](../courses/EAS4300/L25-testing-performance-characteristics.md) — altitude cells
- [L09 — Engine/Aircraft Performance](../courses/EAS4300/L09-engine-aircraft-performance.md) — thrust lapse
- [L05 — Gas Dynamics](../courses/EAS4300/L05-gas-dynamics.md) — flow function origin
- [velocity-triangles](velocity-triangles.md)
- [stagnation-properties](stagnation-properties.md)
- [EAS4300 course hub](../courses/EAS4300.md)
