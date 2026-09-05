# Station Numbering

**Type:** cross-cutting concept · **Standard:** SAE ARP755
**Used in:** [EAS4300](../courses/EAS4300.md) — every lecture from L06 onward
**Tags:** #station-numbering #convention #gas-turbine #notation

---

## What it is

The standardized subscript convention for locations along a gas turbine's flow path. Every equation in
propulsion carries these subscripts, and mixing them up makes otherwise-correct work unmarkable.

## The stations

| Station | Location | Notes |
|---|---|---|
| **0** (or **a**, **∞**) | Free stream, far upstream | Ambient $p_a$, $T_a$, flight Mach $M_0$ |
| **1** | Inlet highlight / diffuser entry | Capture plane |
| **2** | Compressor or fan face | End of inlet. $\pi_d = p_{02}/p_{00}$ |
| **13** | Fan exit / bypass duct | Turbofans only |
| **2.5** | LPC exit / HPC entry | Two-spool engines |
| **3** | Compressor exit / combustor entry | $p_{03}$, $T_{03}$ — key cycle point |
| **4** | Combustor exit / **turbine inlet** | **$T_{04}$ = TIT**, the critical parameter |
| **4.5** | Between HP and LP turbine | Two-spool; EGT often measured near here |
| **5** | Turbine exit | Everything after this goes to the nozzle |
| **6** | Afterburner entry / mixer exit | |
| **7** | Nozzle entry (afterburner exit) | |
| **8** | Nozzle **throat** | $A_8$ — the primary control area |
| **9** (or **e**) | Nozzle **exit** plane | $p_9$, $u_9$ for thrust |
| **19** | Bypass nozzle exit | Separate-flow turbofans |

## Component → station mapping

| Component | Stations |
|---|---|
| Inlet / diffuser | 0 → 2 |
| Fan | 2 → 13 (bypass), 2 → 2.5 (core) |
| Compressor | 2 → 3 (or 2.5 → 3 for HPC) |
| Combustor | 3 → 4 |
| Turbine | 4 → 5 |
| Afterburner | 6 → 7 |
| Nozzle | 7 → 9 |

## Why the numbering matters

**Two stations get confused constantly:**
- **Station 3 is compressor *exit*.** Not the combustor exit.
- **Station 4 is turbine *inlet*.** $T_{04}$ is TIT — the material-limited parameter.

**Two areas are control variables, not just geometry:**
- **$A_8$** (nozzle throat) sets engine mass flow and back-pressures the turbine.
  Must open ~50% when an afterburner lights ([L12](../courses/EAS4300/L12-afterburners-ramjet-combustors.md)).
- **$A_{\text{NGV}}$** (turbine nozzle throat) sets the compressor operating line
  ([L21](../courses/EAS4300/L21-turbines-3.md)).

## Subscript convention

- **No zero** = static property: $p_3$, $T_3$
- **With zero** = stagnation property: $p_{03}$, $T_{03}$

Both appear in the same problem constantly. Label them. See
[stagnation-properties](stagnation-properties.md).

## Ratio notation

$$
\pi_x = \frac{p_{0,\text{out}}}{p_{0,\text{in}}}, \qquad
\tau_x = \frac{T_{0,\text{out}}}{T_{0,\text{in}}}
$$

| Symbol | Component |
|---|---|
| $\pi_r$, $\tau_r$ | Ram (free stream → station 2, isentropic part) |
| $\pi_d$ | Diffuser/inlet recovery, $p_{02}/p_{00}$ |
| $\pi_f$, $\tau_f$ | Fan |
| $\pi_c$, $\tau_c$ | Compressor |
| $\pi_b$ | Burner pressure ratio (~0.94–0.98) |
| $\pi_t$, $\tau_t$ | Turbine |
| $\pi_n$ | Nozzle |
| $\tau_\lambda$ | $T_{04}/T_0$ — cycle temperature ratio |

## Links

- [L06 — Thermodynamics of Jet Engines](../courses/EAS4300/L06-thermodynamics-of-jet-engines.md) — where this is introduced
- [stagnation-properties](stagnation-properties.md)
- [propulsion-efficiencies](propulsion-efficiencies.md)
- [EAS4300 course hub](../courses/EAS4300.md)
