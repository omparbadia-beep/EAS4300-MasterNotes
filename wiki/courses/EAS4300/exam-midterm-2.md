# Midterm 2 — Scope and Prep

**Course:** EAS 4300 Aerospace Propulsion
**Date:** **Mon 9 Nov 2026**, in class, 3:00–3:50 PM, Matherly 0018
**Weight:** 25% of final grade · 100 points
**Review session:** Fri 6 Nov (in class)
**Tags:** #exam #midterm-2 #review #turbomachinery

⏱️ **50 minutes.** Same pacing constraint as Midterm 1.

📐 **This is the turbomachinery exam.** Velocity triangles dominate. Bring a straightedge and *draw
the triangles* — most partial credit on this exam comes from a correctly labeled diagram.

---

## Scope

**L13 through L22** (last new material 4 Nov). Note that L13 (Nozzles) came *after* Midterm 1 and is
therefore in scope here.

| # | Lecture | Book § | Weight guess |
|---|---|---|---|
| 13 | [Nozzles](L13-nozzles.md) | 6.7 | Medium |
| 14 | [Compressors 1](L14-compressors-1.md) | 7.1–7.3 | **Highest** — the foundation |
| 15 | [Compressors 2](L15-compressors-2.md) | 7.4–7.5 *(maps)* ⚠️ | **High** |
| 16 | [Compressors 3](L16-compressors-3.md) | 7.6 *(BL limits)* ⚠️ | **High** |
| 17 | [Compressors 4](L17-compressors-4.md) | 7.7–7.8 *(efficiency, reaction)* ⚠️ | Medium |
| 18 | [Transonic Fan Stage](L18-transonic-fan-stage.md) | 7.11 | Medium |
| 19 | [Turbines 1](L19-turbines-1.md) | 8.1–8.3 | **High** |
| 20 | [Turbines 2](L20-turbines-2.md) | 8.4 *(stresses)* + 8.5 ⚠️ | **High** |
| 21 | [Turbines 3](L21-turbines-3.md) | 8.6 | Medium–High |
| 22 | [Centrifugal Compressors](L22-centrifugal-compressors.md) | ~~8.7~~ → **9.1–9.2** ⚠️ | Medium |

⚠️ **Section references corrected 2026-08-25** after ingesting the textbook — see
[textbook-section-map](textbook-section-map.md). Three things this changes for your revision:

- **§7.4–7.5 (L15) is compressor *maps*; §7.6 (L16) is *boundary layer limitations*** (de Haller,
  diffusion factor). The notes were organized the other way round. Both pages now carry banners, and
  **[L16 §0](L16-compressors-3.md) is new** — read it, it's the section the syllabus actually assigns.
- **§8.4 (L20) is "Rotor Blade and Disc Stresses"**, not aerodynamic losses. **[L20 §0](L20-turbines-2.md)
  is new** — centrifugal stress, the $AN^2$ parameter, Larson–Miller creep, disc design. Expect it.
- **§7.9 Radial Equilibrium (most of L17) is *not assigned*.** Confirm before spending revision time
  on free-vortex blade twist.

🎓 **2026-09-05 — real test evidence changes the priority order above.** Cross-referenced against a
parallel offering's actual "Test 3: Compressors" exam (Section 5041, Spring 2026): it devotes a **40 of
70 points to a stability-audit problem** (given a basic stall PR, an operating PR, and a smaller
turbine flow parameter, compute stall margin and determine whether a deteriorated engine passes) and
several multiple-choice items specifically on the stability audit, basic stall line, and destabilizing
influences. **[L17 §0](L17-compressors-4.md) — added 2026-09-05 — covers exactly this**, and on this
evidence it deserves to be **at least as high-priority as items 1–4 below**, possibly higher than
radial equilibrium ever was. Radial equilibrium did **not** appear on that test at all. This doesn't
prove your Fall 2026 exam matches, but it's real evidence about what a course built around this
material actually tests. Also tested there: the 3 key compressor performance metrics (**flow capacity,
efficiency, stall margin** — memorize that exact triple), and a numeric velocity-triangle pressure-ratio
problem in the same style as item 1 below.

**Likely also fair game:** foundational material from L02/L05/L06 that the turbomachinery builds on
(stagnation properties, choking, efficiency definitions). **Ask the instructor whether Midterm 2 is
cumulative.**

**Homework covered:** HW5 (12 Oct), HW6 (19 Oct), HW7 (26 Oct), HW8 (2 Nov). **Rework all four.**

---

## The six things most likely to appear

### 1. Design a compressor or turbine stage from velocity triangles
**The highest-probability problem, by a wide margin.** Given $U$, $C_a$, and either a target
$\Delta T_0$ or a reaction/angle specification: find all four angles, all velocities, $\Delta T_0$,
$\psi$, $R$, and $\pi_{\text{stage}}$.

**Practice:** [L14 worked example](L14-compressors-1.md#worked-logic--designing-one-compressor-stage),
[L15 worked example](L15-compressors-2.md#worked-logic--a-50-reaction-stage),
[L19 worked example](L19-turbines-1.md#worked-logic--a-single-stage-hp-turbine).

**Always check de Haller ($W_2/W_1 \ge 0.72$) for compressor rows.** A triangle can be geometrically
fine and aerodynamically impossible — and the exam may well hand you exactly that case.

### 2. Reaction and the 50% symmetry
Derive $R$, apply it to find the triangles, verify $\beta_1 = \alpha_2$ and $\beta_2 = \alpha_1$.
Explain why 50% is standard and what goes wrong at the hub.

### 3. Maps, surge, and matching
- Distinguish **rotating stall** from **surge** (mechanism, direction, frequency, consequence)
- Compute **surge margin**, including distortion and transient penalties
- Explain why a **choked turbine NGV** fixes the compressor operating line
- Explain why raising $T_{04}$ at fixed speed moves **toward** surge
- Explain why opening $A_8$ moves **away** from surge

**Practice:** [L16 worked example](L16-compressors-3.md#worked-logic--surge-margin-during-acceleration),
[L21 worked example](L21-turbines-3.md#worked-logic--operating-line-shift-during-acceleration).

### 4. Polytropic vs. isentropic efficiency
Convert between them; explain **preheat** (compressor, $\eta_c<\eta_p$) and **reheat** (turbine,
$\eta_t>\eta_p$). **The sign flip is the point** — expect to be asked which way it goes and why.

### 6. The stability audit (validated as high-weight by a parallel offering's real test)

Given a basic stall PR, an operating PR, and one or more destabilizing influences (tip-gap growth,
deterioration, a smaller turbine flow parameter $FP_4$), compute the **basic stall margin**, apply the
losses, and determine whether the audited result is positive (stall-free) or negative (surge risk) at
a stated confidence level (2σ/3σ). Know the difference between influences on the **operating line**
(deterioration, transients, extractions — all *raise* PR) versus the **stall line** (deterioration,
transient tip gaps, inlet distortion — all *lower* PR). Full method and a worked example:
[L17 §0](L17-compressors-4.md#0-the-compressor-stability-audit-cross-referenced-content--likely-this-lectures-real-subject).

### 5. Conceptual short-answer
Very likely, and cheap marks if prepared:
- **Why do compressors need 15 stages and turbines only 2?** (favorable vs. adverse pressure gradient —
  *not* "because it's hot")
- Why are compressor blades twisted?
- Why does a fan run supersonic in the relative frame but not the absolute?
- How can TIT exceed the blade melting point, and what does it cost?
- Why do centrifugal compressors get such high pressure ratio per stage?
- Why can't a turbine surge?

---

## Formula sheet (assemble your own)

### Euler and triangles
$$
w = U\Delta C_w = c_p\Delta T_0, \qquad C_w = C_a\tan\alpha, \qquad W_w = C_a\tan\beta
$$
$$
w = \frac{C_2^2-C_1^2}{2}+\frac{U_2^2-U_1^2}{2}+\frac{W_1^2-W_2^2}{2}
$$

### Stage parameters
$$
\phi = \frac{C_a}{U}, \qquad \psi = \frac{\Delta C_w}{U}
$$
$$
R_{\text{comp}}=\frac{W_{w1}+W_{w2}}{2U}=1-\frac{C_{w1}+C_{w2}}{2U}
$$
$$
R_{\text{turb}}=\frac{C_a}{2U}\left(\tan\beta_2-\tan\beta_1\right)
$$

### Efficiency
$$
\tau_c = \pi_c^{\frac{\gamma-1}{\gamma\eta_{p,c}}}, \qquad
\tau_t = \pi_t^{\frac{(\gamma-1)\eta_{p,t}}{\gamma}}
$$
$$
\eta_c = \frac{\pi_c^{\frac{\gamma-1}{\gamma}}-1}{\tau_c-1}, \qquad
\pi_{\text{stage}}=\left[1+\frac{\eta_{\text{stage}}\Delta T_0}{T_{01}}\right]^{\frac{\gamma}{\gamma-1}}
$$

### Limits and corrections
$$
\mathrm{DH}=\frac{W_2}{W_1}\ge0.72, \qquad D = 1-\frac{W_2}{W_1}+\frac{\Delta W_w}{2\sigma W_1}\le0.6
$$
$$
\Delta T_0 = \frac{\lambda U\Delta C_w}{c_p} \quad (\lambda: 0.98,\,0.93,\,0.88,\,0.85,\,0.83\ldots)
$$
$$
M_{\text{rel}}=\frac{\sqrt{C_a^2+U^2}}{\sqrt{\gamma R T}}, \qquad M_n = M_{\text{rel}}\cos\Lambda
$$

### Radial equilibrium
$$
\frac{dh_0}{dr}=T\frac{ds}{dr}+C_a\frac{dC_a}{dr}+\frac{C_w}{r}\frac{d(rC_w)}{dr}
$$
$$
\text{Free vortex: } C_w r = \text{const} \ \Rightarrow\ C_a \text{ uniform},\ w \text{ uniform},\ R = 1-\frac{k}{r^2}
$$

### Maps and matching
$$
\dot m_{\text{corr}}=\frac{\dot m\sqrt\theta}{\delta}, \qquad N_{\text{corr}}=\frac{N}{\sqrt\theta}
$$
$$
\mathrm{SM}=\frac{\pi_{\text{surge}}-\pi_{\text{op}}}{\pi_{\text{op}}}\times100\%
$$
$$
\frac{\dot m\sqrt{T_{04}}}{p_{04}}=\text{const (choked NGV)}, \qquad
\dot m_{\text{corr},2}\propto \pi_c\sqrt{\frac{T_{02}}{T_{04}}}
$$

### Centrifugal
$$
\sigma = 1-\frac{0.63\pi}{Z} \ \text{(Stanitz)}, \qquad w = \psi_{\text{pf}}\,\sigma\,U_2^2
$$

### Stability audit
$$
\mathrm{SM}_{\text{basic}}=\frac{\pi_{\text{stall,basic}}-\pi_{\text{op,basic}}}{\pi_{\text{op,basic}}}\times100\%
$$
$$
\mathrm{SM}_{\text{remaining}} = \mathrm{SM}_{\text{basic}}
- \Delta\mathrm{SM}_{\text{operating-line losses}} - \Delta\mathrm{SM}_{\text{stall-line losses}}
- \text{variability} - \text{uncertainty}
$$
$$
\Delta\mathrm{SM}_{\text{tip gap}} = (\text{ratio, \%/0.010in}) \times \text{tip gap opening (0.001in units)}
$$
$$
FP_4 = \frac{\dot m\sqrt{T_4}}{P_4 A_4} \ (\text{const, choked}) \quad\Rightarrow\quad
P_4 = \frac{\dot m\sqrt{T_4}}{FP_4}, \qquad P_3 = \frac{P_4}{1-\text{burner loss}}
$$

### Nozzles
$$
u_9 = \sqrt{2c_pT_{07}\left[1-\left(\frac{p_9}{p_{07}}\right)^{\frac{\gamma-1}{\gamma}}\right]},
\qquad C_F = \frac{F}{p_{07}A_8}, \qquad \lambda = \frac{1+\cos\alpha}{2}
$$

---

## Typical values to have in mind

| Quantity | Compressor | Turbine |
|---|---|---|
| $\Delta T_0$ per stage | 25–35 K | 150–300 K |
| Stage pressure ratio | 1.3–1.4 | ~2 (expansion) |
| $\psi$ | 0.3–0.5 | 1–2.5 |
| $\phi$ | 0.4–0.7 | 0.5–1.0 |
| $R$ (typical) | 0.5 | 0.2–0.5 |
| Turning per row | 20–45° | 70–120° |
| Polytropic efficiency | 0.90–0.92 | 0.90–0.93 |
| Stages in a gas generator | 10–15 | 1–2 |

**Others:** centrifugal stage $\pi$ = 3–8, slip factor 0.85–0.92; fan $M_{rel,tip}$ = 1.3–1.5;
tip speed 350–500 m/s; TIT 1,700–2,000 K; cooling bleed 15–25%; surge margin 15–25%; tip clearance
sensitivity 1.5–3% efficiency per 1% of span.

---

## Top 10 pitfalls

1. **Mixing absolute and relative frames.** Draw and label the triangle first, every time.
2. **Sign errors in $\Delta C_w$.** Compressor: $C_{w2}-C_{w1}$. Turbine: $C_{w1}-C_{w2}$.
3. **Skipping the de Haller check.**
4. **Applying de Haller to a turbine rotor.** Irrelevant — flow accelerates.
5. **Using the compressor stage order for a turbine.** Turbine is **NGV first**.
6. **Getting the polytropic inequality backwards.** $\eta_c<\eta_p$; $\eta_t>\eta_p$.
7. **Omitting the work-done factor** in multistage compressor estimates.
8. **Confusing rotating stall with surge.**
9. **Treating slip factor as an efficiency.** It's kinematic — apply it *and* efficiency separately.
10. **Cold $\gamma$, $c_p$ in the turbine.** Use 1.33 / 1150.

---

## Suggested 5-day plan

| Day | Focus |
|---|---|
| **5 days out** | [L14](L14-compressors-1.md) cold — derive Euler, draw triangles from a blank page. |
| **4 days out** | [L15](L15-compressors-2.md) + [L19](L19-turbines-1.md). Reaction both ways. Do both worked examples blind. |
| **3 days out** | Rework HW5–HW8 without solutions. |
| **2 days out** | [L16](L16-compressors-3.md) + [L21](L21-turbines-3.md) — treat as one topic. Surge margin and matching problems. |
| **1 day out** | [L13](L13-nozzles.md), [L17](L17-compressors-4.md), [L18](L18-transonic-fan-stage.md), [L20](L20-turbines-2.md), [L22](L22-centrifugal-compressors.md) — mostly conceptual. Write your formula sheet. Attend the 6 Nov review. |

---

## Links

- Course hub: [EAS4300](../EAS4300.md)
- Previous exam: [exam-midterm-1](exam-midterm-1.md)
- [exam-final](exam-final.md)
- Concepts: [velocity-triangles](../../concepts/velocity-triangles.md) ·
  [corrected-parameters](../../concepts/corrected-parameters.md) ·
  [propulsion-efficiencies](../../concepts/propulsion-efficiencies.md)
