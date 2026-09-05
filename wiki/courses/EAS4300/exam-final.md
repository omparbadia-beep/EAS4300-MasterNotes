# Final Exam — Scope and Prep

**Course:** EAS 4300 Aerospace Propulsion
**Date:** **Mon 7 Dec 2026, 10:00 AM – 12:00 PM** (note: *not* the usual class time or period)
**Weight:** **30% of final grade** — the single largest component · 100 points
**Review sessions:** Mon 30 Nov and Wed 2 Dec (in class)
**Tags:** #exam #final #cumulative #review

⏱️ **2 hours** — twice a midterm. Expect **longer, multi-part problems** rather than more of them: a
full cycle analysis that then asks for a component design, or a matching problem that starts from a
map reading.

📚 **Cumulative** — all 26 topics. *(Confirm with the instructor whether it is weighted toward the
post-Midterm-2 material or genuinely uniform.)*

---

## Scope

**Everything, L01–L26.** The post-Midterm-2 material is new and untested, so it's disproportionately
likely to appear:

| Block | Lectures | Status |
|---|---|---|
| Fundamentals | [L01](L01-introduction.md)–[L05](L05-gas-dynamics.md) | Tested on M1 |
| Cycle analysis | [L06](L06-thermodynamics-of-jet-engines.md)–[L09](L09-engine-aircraft-performance.md) | Tested on M1 |
| Non-rotating components | [L10](L10-inlets.md)–[L13](L13-nozzles.md) | L10–12 on M1, L13 on M2 |
| Turbomachinery | [L14](L14-compressors-1.md)–[L22](L22-centrifugal-compressors.md) | Tested on M2 |
| **Rockets** | [L23](L23-rocket-engines-1.md)–[L24](L24-rocket-engines-2.md) | **Never tested — high probability** |
| **Testing** | [L25](L25-testing-performance-characteristics.md) | **Never tested — high probability** |
| Synthesis | [L26](L26-course-takeaways.md) | Study guide, not new material |

🎯 **Highest-value target: [L23](L23-rocket-engines-1.md) and [L24](L24-rocket-engines-2.md).**
Two full lectures plus HW9, never examined, and they come at the end of the semester when most of the
class is fading. The material is also self-contained — you can master it in a day. Best marks-per-hour
on the whole exam.

**[L25](L25-testing-performance-characteristics.md) is the second-best target** for the same reason:
small, distinctive, and likely underprepared.

**Homework:** HW1–HW9, all of it. **HW9 (out 16 Nov, rockets) is especially worth reworking.**

---

## Study strategy

**Start from [L26 — Course Takeaways](L26-course-takeaways.md).** It contains the six unifying ideas,
the master equation sheet, the numbers table, and a suggested study sequence. If you can reconstruct
the course from those six ideas, you can derive most of what you'd otherwise memorize.

### The six ideas (from L26)

1. **Thrust is a momentum balance on a control volume**
2. **Stagnation properties carry the energy bookkeeping** — $T_0$ tracks energy, $p_0$ tracks quality
3. **Compressible flow reverses intuition** — $dA/A = (M^2-1)dV/V$
4. **Euler's turbomachinery equation is exact and universal** — $w = U\Delta C_w$
5. **The pressure gradient decides what's achievable** — adverse vs. favorable explains almost everything
6. **Everything is a trade, and components can't be designed alone**

### Suggested sequence

| Priority | Focus | Why |
|---|---|---|
| **1** | [L23](L23-rocket-engines-1.md) + [L24](L24-rocket-engines-2.md) + HW9 | Untested, self-contained, high yield |
| **2** | [L25](L25-testing-performance-characteristics.md) | Untested, small, distinctive |
| **3** | [L06](L06-thermodynamics-of-jet-engines.md) + cycle march ([L07](L07-ramjets.md)–[L08b](L08b-turbofans.md)) | The most likely long problem |
| **4** | [L14](L14-compressors-1.md) + [L19](L19-turbines-1.md) triangles | Second most likely long problem |
| **5** | [L05](L05-gas-dynamics.md) | Most-reused toolkit; redo the summary table blind |
| **6** | [L16](L16-compressors-3.md) + [L21](L21-turbines-3.md) matching | One topic, high concept density |
| **7** | Components ([L10](L10-inlets.md)–[L13](L13-nozzles.md)), cooling ([L20](L20-turbines-2.md)) | Conceptual short-answer marks |
| **8** | Everything else, skim | |

---

## Derivations to have at your fingertips

These are short, standard, and recur across exams:

| Derivation | Lecture |
|---|---|
| Thrust equation from CV momentum balance | [L02](L02-basic-concepts.md) |
| $p_{02}\le p_{01}$ for adiabatic work-free flow | [L02](L02-basic-concepts.md) |
| $dA/A = (M^2-1)dV/V$ | [L05](L05-gas-dynamics.md) |
| Froude efficiency $\eta_p = 2/(1+u_e/u_a)$ | [L06](L06-thermodynamics-of-jet-engines.md) |
| Turbine work balance ⇒ $\tau_t$ | [L08a](L08a-turbojets.md) |
| Breguet range equation | [L09](L09-engine-aircraft-performance.md) |
| Euler's turbomachinery equation | [L14](L14-compressors-1.md) |
| Degree of reaction $R = (W_{w1}+W_{w2})/2U$ | [L15](L15-compressors-2.md) |
| Polytropic efficiency relation | [L15](L15-compressors-2.md) |
| Free vortex ⇒ uniform $C_a$ and uniform work | [L17](L17-compressors-4.md) |
| **Tsiolkovsky rocket equation** | [L23](L23-rocket-engines-1.md) |
| Solid motor stability, $n<1$ | [L24](L24-rocket-engines-2.md) |

---

## Cross-cutting questions the final is likely to ask

A cumulative exam favors questions that **span lectures**. Prepare these explicitly:

- **Trace one design decision through the engine.** E.g. "the afterburner lights — walk through every
  component that must respond and why." ([L12](L12-afterburners-ramjet-combustors.md) →
  [L13](L13-nozzles.md) → [L16](L16-compressors-3.md) → [L21](L21-turbines-3.md))
- **Compare engine types across the Mach range** and justify the ordering
  ([L26](L26-course-takeaways.md) family tree)
- **Explain why a component's ideal efficiency assumption breaks down** and where the loss goes
- **Given a symptom, diagnose the component.** ([L25](L25-testing-performance-characteristics.md) gas
  path analysis table)
- **Compare an air-breather and a rocket on a stated basis** — thrust vs. speed, thrust vs. altitude,
  $I_{sp}$, propulsive efficiency ([L01](L01-introduction.md), [L23](L23-rocket-engines-1.md))
- **Explain the adverse/favorable pressure gradient consequence** for any pair of components

---

## Formula sheet

**Use the [L26 master equation sheet](L26-course-takeaways.md#master-equation-sheet)** — it consolidates
thrust/performance, cycle parameters, gas dynamics, turbomachinery, and rockets in one place, and the
[numbers table](L26-course-takeaways.md#numbers-worth-carrying-into-the-exam) alongside it.

**Rocket additions not on the midterm sheets:**

$$
F = \dot m_p c, \qquad c = c^* C_F, \qquad I_{sp}=\frac{c}{g_0}, \qquad c \propto \sqrt{\frac{T_c}{\mathcal M}}
$$
$$
c^* = \frac{p_c A_t}{\dot m_p} = \frac{1}{\Gamma}\sqrt{\frac{R_u T_c}{\mathcal M}}, \qquad
\Gamma = \sqrt\gamma\left(\frac{2}{\gamma+1}\right)^{\frac{\gamma+1}{2(\gamma-1)}}
$$
$$
C_F = \Gamma\sqrt{\frac{2\gamma}{\gamma-1}\left[1-\left(\frac{p_e}{p_c}\right)^{\frac{\gamma-1}{\gamma}}\right]}+\frac{(p_e-p_a)A_e}{p_cA_t}
$$
$$
\Delta V = c\ln\frac{m_0}{m_f}, \qquad \lambda = \frac{\frac{1}{R}-\epsilon}{1-\epsilon}, \qquad r = a\,p_c^{\,n}
$$

**Rocket numbers:** LEO $\Delta V$ ≈ 9,400 m/s · $I_{sp}$: solid 250–280, RP-1/LOX 330–360,
LH₂/LOX 440–465 s · $\gamma_{\text{rocket}}$ ≈ 1.15–1.25 · Summerfield separation: $p_e \ge 0.4p_a$ ·
$\epsilon$: sea level 10–25, vacuum 80–285.

---

## Exam-day checklist

- [ ] Confirm the room — final exam locations are often **not** the regular classroom
- [ ] 10:00 AM start, **not** period 8
- [ ] Calculator, straightedge (for velocity triangles), formula sheet if permitted
- [ ] **Read the whole exam first**, then start with the problem you're most confident on
- [ ] **Draw a labeled diagram for every problem** — stations for cycle problems, triangles for
      turbomachinery. Most partial credit lives here.
- [ ] **Write units on every line.** Unit errors are the most common avoidable loss.
- [ ] **State your assumptions explicitly** (ideal components, perfectly expanded, $f\ll1$) — this earns
      credit and protects you if a number goes wrong
- [ ] **Sanity check every answer.** Is $I_{sp}$ in the right range? Is $\eta_p$ under 1? Is the exit
      Mach plausible? A flagged wrong answer scores better than an unflagged one.
- [ ] Budget ~28 min per question on a 4-question exam; leave 10 minutes to review

---

## Links

- **Study guide: [L26 — Course Takeaways](L26-course-takeaways.md)**
- Course hub: [EAS4300](../EAS4300.md)
- Earlier exams: [exam-midterm-1](exam-midterm-1.md) · [exam-midterm-2](exam-midterm-2.md)
- Concepts: [station-numbering](../../concepts/station-numbering.md) ·
  [stagnation-properties](../../concepts/stagnation-properties.md) ·
  [propulsion-efficiencies](../../concepts/propulsion-efficiencies.md) ·
  [velocity-triangles](../../concepts/velocity-triangles.md) ·
  [corrected-parameters](../../concepts/corrected-parameters.md)
