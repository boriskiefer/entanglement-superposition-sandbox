# Entanglement Swapping Sandbox

A compact technical artifact for **scenario screening**, **tradeoff exploration**, and **technical specification support** in a minimal quantum-networking model.

This repository centers on a simple but meaningful architecture:

* **two entanglement sources**
* **one hub performing a Bell-state measurement (BSM)**
* **adjustable source states**
* **misaligned BSM modeling**
* **simple loss**
* **branch-resolved remote-state metrics**

The purpose is not to replace full network simulators. The purpose is to provide a transparent, inspectable sandbox that helps technical users understand how source mismatch, hub measurement quality, and loss affect whether entanglement swapping is merely detected or actually useful.

---

## Why this artifact exists

Entanglement swapping is a foundational primitive for repeater-style quantum networking. It is often discussed at a high level, but many architecture-facing questions require a more explicit and compact model:

* How sensitive is swapping to source imbalance?
* How much does BSM misalignment degrade remote-state quality?
* How should one distinguish branch success from useful swapped entanglement?
* Which parameters matter most for scenario screening and downstream specification work?

This sandbox was built to make those questions visible in a simple, technical, and user-facing form.

---

## Core insight

**Bell-state measurement success and useful entanglement swapping are not the same thing.**

A branch can occur with nonzero probability while still producing a degraded remote state. The sandbox makes that distinction explicit by separating:

* **branch probability**
* **valid probability after loss**
* **conditional swapped-state quality**
* **yield-style metrics that combine occurrence and usefulness**

---

## What the sandbox models

The simulator uses a four-qubit abstraction:

* source A prepares qubits **1,2**
* source B prepares qubits **3,4**
* the hub acts on qubits **2,3**
* the remote swapped state is analyzed on qubits **1,4**

### Adjustable source states

Each source is parameterized as

[
|\psi\rangle = \cos(\alpha),|00\rangle + e^{i\phi}\sin(\alpha),|11\rangle
]

This supports direct exploration of source mismatch and phase sensitivity.

### Misaligned Bell-state measurement

The hub BSM can be rotated away from the ideal Bell basis using separate even/odd sector parameters. This provides a compact way to study nonideal hub behavior without introducing a full optical-circuit model.

### Simple loss model

The current implementation applies a link-level loss factor to valid branch probability:

[
p_{\mathrm{valid}} = \eta_2 \eta_3 \xi_{\mathrm{BSM}} , p_{\mathrm{cond}}
]

This separates state quality from valid-event rate in a way that is useful for architecture-facing scenario screening.

---

## Reported metrics

The sandbox reports branch-resolved and summary metrics including:

* branch probability
* valid probability after loss
* concurrence
* negativity
* best Bell-state fidelity
* entanglement yield
* fidelity yield

These metrics are intentionally complementary:

* **probability metrics** tell you how often something happens
* **entanglement metrics** tell you how nonclassical the remote state remains
* **yield metrics** tell you how much useful performance survives after loss and nonidealities

---

## Repository structure

```text
README.md
entanglement_swapping_technical_brief.pdf
entanglement_swapping_implementation_brief.pdf
entanglement_swapping_sandbox.ipynb
```

---

## Notebook structure

The notebook is organized into three cells:

### Cell 1 — Tools / Engine

Contains:

* source-state construction
* Bell-state basis and rotated BSM basis
* branch projection logic
* partial trace
* entanglement and fidelity metrics
* helper utilities
* shared display labels

### Cell 2 — UI

Contains:

* sliders and controls for source parameters
* BSM misalignment controls
* loss controls
* branch focus selection
* snapshot table and conditional remote-state display

### Cell 3 — Figures

Contains:

* branch probability bar plots
* conditional quality bar plots
* (\alpha_A)-(\alpha_B) heatmaps
* inherited parameter summary panel

---

## Companion documents

This repository is designed as a matched artifact set.

### Technical Brief

**Purpose:** explain what the sandbox is for.

Focus:

* problem addressed
* scenario-screening value
* representative metrics
* use cases
* positioning and technical relevance

### Implementation Brief

**Purpose:** document theory and rigor behind the sandbox.

Focus:

* physical model
* Bell-state measurement construction
* misaligned BSM basis
* loss treatment
* metrics
* software structure
* validation and testing strategy
* limitations and extension paths

Together, these documents separate:

* **artifact value**
  from
* **theory and implementation trustworthiness**

---

## Intended use cases

This artifact is aimed at technical audiences, including:

* solutions architects
* partner engineers
* applied research leads
* technically literate collaborators
* technical hiring managers
* ecosystem and developer-relations stakeholders

Typical use cases include:

* technical stakeholder communication
* architecture exploration
* scenario screening
* technical specification support
* GitHub / portfolio demonstration
* partner-facing technical discussion

---

## What this artifact is not

This sandbox is **not**:

* a claim of new physics
* a replacement for full quantum-network simulators
* a detailed optical hardware model
* a business-value or ROI calculator

Its value is different: it is a compact and inspectable artifact that helps users evaluate how source quality, hub measurement quality, and loss jointly affect swapped entanglement performance.

---

## Validation philosophy

The sandbox is intentionally small enough that validation can stay explicit and interpretable.

Representative checks include:

* branch probabilities sum correctly in the ideal no-loss case
* ideal Bell-point behavior is recovered for symmetric maximally entangled inputs
* valid probabilities scale correctly with (\eta_2 \eta_3 \xi_{\mathrm{BSM}})
* concurrence, negativity, and fidelity remain within physical bounds
* conditional remote density matrices remain Hermitian and trace-normalized

The goal is not just to produce plots, but to maintain clear theory-to-code traceability.

---

## Near-term extension paths

Natural next steps include:

* interference-visibility / path-mismatch dial at the hub
* more physical quantum loss channels
* branch acceptance policies
* linear repeater-chain extension
* exportable scenario-screening summaries

---

## Strategic positioning

This repository is intended to show more than the ability to code a simulator.

It is meant to demonstrate the ability to turn a current technical concept into a **stakeholder-facing technical artifact** that supports:

* clear reasoning
* parameter screening
* architecture communication
* implementation trust

That is the main purpose of the sandbox.

---

## Acknowledgements

This material was developed and/or adapted with support from the National
Science Foundation through the QCAP-NQVL-Pilot and QCAP-NQVL-Design efforts
under NSF Award Nos. OSI-2410813 and OSI-2531569.
Any opinions, findings, conclusions, or recommendations expressed in this
material are those of the author(s) and do not necessarily reflect the views
of the National Science Foundation.

---

## Contact

**Boris Kiefer**
New Mexico State University
[bkiefer@nmsu.edu](mailto:bkiefer@nmsu.edu)

* **GitHub:** [boriskiefer](https://github.com/boriskiefer)
* **LinkedIn:** [Boris Kiefer](https://www.linkedin.com/in/boris-kiefer-85089831/)

---

## Suggested top-of-repo companion items

A strong presentation package for this repository is:

1. this `README.md`
2. the notebook
3. a screenshot or heatmap in `figures/`
4. the **Technical Brief**
5. the **Implementation Brief**

That set creates a compact but credible technical artifact package.
