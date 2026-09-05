# Velocity Triangles

**Type:** cross-cutting concept
**Used in:** [EAS4300](../courses/EAS4300.md) — L14–L22 (all turbomachinery)
**Tags:** #velocity-triangles #euler-equation #turbomachinery #rotor #stator #relative-frame #rothalpy

---

## The one idea

**Turbomachinery has two observers**, and every equation belongs to one of them:

- **Absolute frame** (stationary casing): velocity $\mathbf C$
- **Relative frame** (rotating with the rotor): velocity $\mathbf W$

$$
\mathbf{C}=\mathbf{W}+\mathbf{U}, \qquad U = \omega r
$$

**Rules that follow:**
- **Stators** are stationary ⇒ absolute frame
- **Rotors** move ⇒ relative frame
- $U$ is purely **tangential**
- The **axial component is the same in both frames**: $C_a = W_a$

**Applying a relation in the wrong frame is the single most common error in the turbomachinery half of
the course.** Draw the triangle and label both frames before writing anything.

---

## Notation

| Symbol | Meaning |
|---|---|
| $C$ | Absolute velocity |
| $W$ | Relative velocity |
| $U = \omega r$ | Blade speed |
| $C_a$ ($=W_a$) | Axial component |
| $C_w$, $W_w$ | Tangential (whirl) components |
| $\alpha$ | Absolute flow angle from axial |
| $\beta$ | Relative flow angle from axial |

$$
C_w = C_a\tan\alpha, \qquad W_w = C_a\tan\beta
$$

$$
C^2 = C_a^2+C_w^2, \qquad W^2 = C_a^2+W_w^2
$$

---

## Euler's turbomachinery equation

From angular momentum conservation on a control volume around the rotor:

$$
\boxed{\ w = U_2 C_{w2}-U_1 C_{w1}\ }
$$

Axial machine, constant mean radius:

$$
w = U\,\Delta C_w = c_p\,\Delta T_0
$$

**Three things to know about it:**

1. **It is exact.** It holds for real, lossy machines. Losses determine how much *pressure rise* you get
   from the work, not the work itself.
2. **Work scales with $U$** — blade speed is the dominant design lever, limited by stress and tip Mach.
3. **Sign:** compressor $\Delta C_w > 0$ (work in); turbine $\Delta C_w < 0$ (work out).

### Alternative three-term form

$$
w = \underbrace{\frac{C_2^2-C_1^2}{2}}_{\text{absolute KE}}
+\underbrace{\frac{U_2^2-U_1^2}{2}}_{\text{centrifugal}}
+\underbrace{\frac{W_1^2-W_2^2}{2}}_{\text{relative diffusion}}
$$

**The middle term vanishes for axial machines** ($U_1 = U_2$) and **dominates for centrifugal machines**
— which is exactly why a centrifugal stage gets $\pi = 3$–8 while an axial stage gets 1.3–1.4
([L22](../courses/EAS4300/L22-centrifugal-compressors.md)).

---

## Rothalpy

The rotating-frame conserved quantity — what $h_0$ is to the stationary frame:

$$
I = h+\frac{W^2}{2}-\frac{U^2}{2}, \qquad I_1 = I_2 \ \text{(adiabatic rotor)}
$$

For an axial rotor: **relative stagnation enthalpy is conserved.**

---

## Compressor vs. turbine — the contrast table

| | **Compressor** ([L14](../courses/EAS4300/L14-compressors-1.md)) | **Turbine** ([L19](../courses/EAS4300/L19-turbines-1.md)) |
|---|---|---|
| Stage order | **Rotor → Stator** | **Stator (NGV) → Rotor** |
| Pressure gradient | Adverse | Favorable |
| Rotor relative flow | **Diffuses** ($W_2<W_1$) | **Accelerates** ($W_2>W_1$) |
| Turning per row | 20–45° | 70–120° |
| $\Delta T_0$ per stage | 25–35 K | 150–300 K |
| Stages for a gas generator | 10–15 | 1–2 |
| Diffusion limit | **de Haller $W_2/W_1\ge0.72$** | none — flow accelerates |
| $\psi = \Delta C_w/U$ | 0.3–0.5 | 1–2.5 |
| $\phi = C_a/U$ | 0.4–0.7 | 0.5–1.0 |
| Failure mode | Stall / surge | Creep / thermal |

**The pressure gradient explains all of it.** Accelerating flow keeps boundary layers thin and attached;
diffusing flow pushes them toward separation.

---

## Degree of reaction

The share of the **static** enthalpy change occurring in the rotor:

$$
R = \frac{\Delta h_{\text{rotor}}}{\Delta h_{\text{stage}}}
$$

**Compressor:**

$$
R = \frac{W_{w1}+W_{w2}}{2U} = 1-\frac{C_{w1}+C_{w2}}{2U}
$$

**Turbine:**

$$
R = \frac{C_a}{2U}\left(\tan\beta_2-\tan\beta_1\right)
$$

| $R$ | Character |
|---|---|
| 0 | **Impulse** — all pressure change in the stationary row; no rotor pressure difference ⇒ minimal tip leakage |
| 0.5 | **Symmetric** — mirror-image triangles ($\beta_1=\alpha_2$, $\beta_2=\alpha_1$), same blade shapes, best efficiency |
| 1.0 | All pressure change in the rotor |

**Typical:** compressors 0.5; turbine HP stages 0.2–0.4; turbine LP stages ~0.5.

**$R$ varies with radius** because $U = \omega r$. Designed at the mean, it falls at the hub — and if it
goes negative, the hub rotor accelerates the flow while the hub stator must diffuse impossibly hard.
This is the free-vortex hub limit ([L17](../courses/EAS4300/L17-compressors-4.md)).

---

## Design limits to check

| Check | Applies to | Criterion |
|---|---|---|
| **de Haller** | Compressor rows | $W_2/W_1 \ge 0.72$ |
| **Diffusion factor** | Compressor rows | $D \le 0.6$ |
| **Tip relative Mach** | Compressor/fan | $M_{rel} \lesssim 1.5$ (fan), $\lesssim1$ (core) |
| **Blade root stress** | All rotors | $\sigma \propto \rho_m U_t^2$ |
| **Zweifel** | Turbine spacing | $Z\approx0.8$ |
| **Work-done factor** | Multistage compressors | $\lambda = 0.98 \to 0.83$ by stage |

---

## Common errors

- **Mixing frames.** Draw and label first.
- **Sign errors in $\Delta C_w$.**
- **Thinking Euler requires isentropic flow.** It doesn't.
- **Forgetting $C_a$ is common to both frames.**
- **Skipping the de Haller check** — a triangle can be geometrically fine and aerodynamically impossible.
- **Applying de Haller to a turbine rotor.** Irrelevant — the flow accelerates.
- **Assuming $U$ is uniform with radius.**
- **Using the compressor stage order for a turbine.**
- **Inconsistent $\psi$ definitions** — some texts use $\Delta h_0/(\tfrac12 U^2)$, giving 2× values.

---

## Links

- [L14 — Compressors 1](../courses/EAS4300/L14-compressors-1.md) — main treatment
- [L15 — Compressors 2](../courses/EAS4300/L15-compressors-2.md) — reaction and losses
- [L17 — Compressors 4](../courses/EAS4300/L17-compressors-4.md) — radial variation, twist
- [L18 — Transonic Fan Stage](../courses/EAS4300/L18-transonic-fan-stage.md)
- [L19 — Turbines 1](../courses/EAS4300/L19-turbines-1.md)
- [L22 — Centrifugal Compressors](../courses/EAS4300/L22-centrifugal-compressors.md)
- [stagnation-properties](stagnation-properties.md)
- [EAS4300 course hub](../courses/EAS4300.md)
