# Wiki Index

Catalog of every page in this wiki. Update whenever a page is added, removed, or its scope changes.
See [CLAUDE.md](../CLAUDE.md) for the ingest/query/lint workflow.

## Courses

| Page | Course | Summary |
|---|---|---|
| [COP2274](courses/COP2274.md) | COP2274 | TBD — not yet ingested |
| [EAS4200](courses/EAS4200.md) | EAS4200 | TBD — not yet ingested |
| **[EAS4300](courses/EAS4300.md)** | **EAS4300 — Aerospace Propulsion** | **Fall 2026, Mannem. Air-breathing and rocket engines: cycles, gas dynamics, combustion, inlets/combustors/nozzles, axial and centrifugal turbomachinery, rockets, testing. Syllabus fully ingested; 27 lecture pages + 3 exam pages.** |
| [EAS4700](courses/EAS4700.md) | EAS4700 | TBD — not yet ingested |
| [EML4140](courses/EML4140.md) | EML4140 | TBD — not yet ingested |

## EAS4300 — lecture notes

Detailed per-lecture notes with concepts explained, equations typeset as Obsidian math, worked
examples, pitfalls, and exam checklists. Numbered by the syllabus's own topic number.

**Book sections verified against the textbook 2026-08-25** — see
[textbook-section-map](courses/EAS4300/textbook-section-map.md), which also lists the four places the
syllabus's section numbers are wrong. ⚠️ marks a lecture affected by one.

| # | Page | Topic | Book § |
|---|---|---|---|
| 1 | [L01](courses/EAS4300/L01-introduction.md) | Introduction — thrust, engine taxonomy, $I_{sp}$/TSFC | 1.1–1.2, 1.4 |
| 2 | [L02](courses/EAS4300/L02-basic-concepts.md) | Control volumes, conservation laws, perfect gases | 2.1–2.3 |
| 3 | [L03](courses/EAS4300/L03-combustion-thermodynamics-1.md) | Stoichiometry, fuel-air ratio, heating values | 2.4 |
| 4 | [L04](courses/EAS4300/L04-combustion-thermodynamics-2.md) | Adiabatic flame temp, dissociation, equilibrium, TIT | 2.4 |
| 5 | [L05](courses/EAS4300/L05-gas-dynamics.md) | Isentropic flow, choking, shocks, Fanno/Rayleigh | 3.1–3.6 |
| 6 | [L06](courses/EAS4300/L06-thermodynamics-of-jet-engines.md) | Stations, thrust equation, the three efficiencies | 5.1–5.2 |
| 7 | [L07](courses/EAS4300/L07-ramjets.md) | Ramjets — ram compression, no static thrust, Mach limits | 5.3 |
| 8a | [L08a](courses/EAS4300/L08a-turbojets.md) | Turbojets — full cycle march, optimum $\pi_c$, spools | 5.4 |
| 8b | [L08b](courses/EAS4300/L08b-turbofans.md) | Turbofans — bypass ratio, the propulsive efficiency win | **5.5** ⚠️ |
| 9 | [L09](courses/EAS4300/L09-engine-aircraft-performance.md) | Thrust lapse, matching, Breguet range | 5.7–**5.8** ⚠️ |
| 10 | [L10](courses/EAS4300/L10-inlets.md) | Inlets — recovery, spillage, multi-shock, unstart | 6.1–6.3 |
| 11 | [L11](courses/EAS4300/L11-combustors.md) | Combustors — zones, stabilization, pattern factor, NOₓ | 6.4 |
| 12 | [L12](courses/EAS4300/L12-afterburners-ramjet-combustors.md) | Afterburners — augmentation, thermal choking, variable nozzle | 6.5 |
| 13 | [L13](courses/EAS4300/L13-nozzles.md) | Nozzles — C-D, expansion regimes, $C_F$, variable geometry | 6.7 |
| 14 | [L14](courses/EAS4300/L14-compressors-1.md) | Velocity triangles, Euler's equation, de Haller | 7.1–7.3 |
| 15 | [L15](courses/EAS4300/L15-compressors-2.md) | Reaction, polytropic efficiency, loss mechanisms | 7.4–7.5 |
| 16 | [L16](courses/EAS4300/L16-compressors-3.md) | Maps, surge vs. rotating stall, stage matching | 7.6 |
| 17 | [L17](courses/EAS4300/L17-compressors-4.md) | Radial equilibrium, free vortex, twist, work-done factor | 7.7–7.8 |
| 18 | [L18](courses/EAS4300/L18-transonic-fan-stage.md) | Transonic fans — relative Mach, unique incidence, sweep | 7.11 |
| 19 | [L19](courses/EAS4300/L19-turbines-1.md) | Turbine triangles, impulse vs. reaction, Smith chart | 8.1–8.3 |
| 20 | [L20](courses/EAS4300/L20-turbines-2.md) | Reheat effect, losses, blade cooling, creep | 8.4–8.5 |
| 21 | [L21](courses/EAS4300/L21-turbines-3.md) | Choked NGV, component matching, operating line | 8.6 |
| 22 | [L22](courses/EAS4300/L22-centrifugal-compressors.md) | Centrifugal — slip factor, diffusers, specific speed | **9.1–9.2** ⚠️ |
| 23 | [L23](courses/EAS4300/L23-rocket-engines-1.md) | Rockets — $I_{sp}$, $c^*$/$C_F$, Tsiolkovsky, staging | 10 |
| 24 | [L24](courses/EAS4300/L24-rocket-engines-2.md) | Thrust chambers, cooling, power cycles, solid motors | 10 |
| 25 | [L25](courses/EAS4300/L25-testing-performance-characteristics.md) | Test facilities, instrumentation, EGT margin, health monitoring | 9.5 |
| 26 | [L26](courses/EAS4300/L26-course-takeaways.md) | Synthesis — six unifying ideas, master equation sheet | 9.1–9.2 |


## EAS4300 — reference

| Page | Summary |
|---|---|
| [textbook-section-map](courses/EAS4300/textbook-section-map.md) | Verified section→title→page map for all 14 chapters of Hill & Peterson 2nd ed, plus a line-by-line reconciliation against the syllabus. Records the four syllabus errors and what the course skips. |

## EAS4300 — exam prep

| Page                                                | Exam                     | Date                        |
| --------------------------------------------------- | ------------------------ | --------------------------- |
| [exam-midterm-1](courses/EAS4300/exam-midterm-1.md) | Midterm 1 (L01–L12), 25% | Wed 7 Oct 2026              |
| [exam-midterm-2](courses/EAS4300/exam-midterm-2.md) | Midterm 2 (L13–L22), 25% | Mon 9 Nov 2026              |
| [exam-final](courses/EAS4300/exam-final.md)         | Final (cumulative), 30%  | Mon 7 Dec 2026, 10 AM–12 PM |

## Concepts

Cross-cutting pages. Currently all originate in EAS4300; link them from other courses as those are
ingested (several are general thermo/fluids ideas likely to recur).

| Page | Summary |
|---|---|
| [station-numbering](concepts/station-numbering.md) | The 0/2/3/4/5/8/9 gas turbine station convention and ratio notation |
| [stagnation-properties](concepts/stagnation-properties.md) | Total vs. static; $T_0$ tracks energy, $p_0$ tracks quality; why $p_0$ can only fall |
| [propulsion-efficiencies](concepts/propulsion-efficiencies.md) | Thermal, propulsive, overall; Froude efficiency; polytropic preheat/reheat |
| [velocity-triangles](concepts/velocity-triangles.md) | The two-frame method, Euler's equation, reaction, compressor vs. turbine |
| [corrected-parameters](concepts/corrected-parameters.md) | $\theta$, $\delta$, and why one map covers the whole flight envelope |
