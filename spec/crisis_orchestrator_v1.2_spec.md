# Crisis Orchestrator v1.2 – Core Specification

## 0. Overview

The Crisis Orchestrator is a decision-support system for large-scale, multi-hazard crises (nuclear incidents, infrastructure collapse, pandemics, complex emergencies).

It:

- Maintains a probabilistic world model under uncertainty and adversarial conditions.
- Coordinates specialized modules (evacuation, medical, logistics, nuclear, cyber, information integrity).
- Produces human-facing recommendations with explicit tradeoffs and ethical reasoning.
- Respects governance profiles and sovereignty constraints.
- Uses hysteresis and thresholds to avoid frantic decision flip-flopping.

Scenarios and test cases live in a separate file: `scenario_pack_v1.2.md`.

---

## 1. World Model & State Representation

### 1.1 Core Entities

The world state is represented as a dynamic, uncertainty-aware graph including:

- **Geographic zones:** 1km² grid cells with:
  - Hazard levels (radiation, flood, fire, cyber outages)
  - Damage estimates (infrastructure, housing)
  - Population density and mobility estimates
- **Critical infrastructure nodes:**
  - Hospitals, power plants, substations, comms hubs, ports, airports, key bridges
  - Status (online / degraded / offline / unknown)
- **Resource inventories:**
  - Medical: ICU beds, ventilators, drugs, field hospitals
  - Logistics: fuel, food, water, vehicles, personnel
  - Location, quantity, confidence in data
- **Population movements:**
  - Aggregate flows from traffic sensors, mobile network data (where legally permissible), transport systems
- **Response assets:**
  - Search-and-rescue teams, med teams, logistics convoys, drones, airlift units
  - Location, capability profile, current assignment

### 1.2 Uncertainty-Aware Data Fusion

For each fact in the world model, the system maintains a **confidence score** in [0.1, 1.0] based on:

- Source reliability priors per data stream (satellite provider, national agency, social media, etc.).
- **Bayesian belief updates** when evidence accumulates or conflicts.
- **Temporal decay**: older data loses weight over time.
- **Multi-source validation:**
  - Agreement across independent sensors boosts confidence.
  - Contradictions trigger anomaly analysis.

Techniques:

- Kalman filters and related state estimators for continuous physical quantities (radiation, flows).
- Bayesian networks for causal and discrete relationships.
- Cross-correlation and pattern analysis to detect coordinated misinformation.

### 1.3 Adversarial & Anomaly Detection

The system assumes some data will be malicious.

Checks include:

- Behavioral anomalies (sudden bursts of synchronized accounts).
- Geographic and temporal consistency:
  - “Impossible travel times” or duplicated entities in multiple locations.
- Signature / credential verification for official feeds.
- Media forensics on audio/video:
  - Artifact and deepfake pattern detection.
  - Vocal stress patterns inconsistent with context.

Suspicious streams are down-weighted or quarantined; critical ones can be isolated entirely.

---

## 2. Core Functional Modules

All modules read from/write to the shared world model.

### 2.1 Damage Assessment & Situation Modeling

**Inputs:**

- Satellite and aerial imagery
- Seismic and structural sensors
- Drone footage
- Social / local reports (de-biased)

**Outputs:**

- Damage probability maps (building collapse, road usability)
- Infrastructure status (bridges, power lines, hospitals)
- Trapped / affected population estimates

**Update cadence:** ≈15-minute cycles.

Feeds:

- Evacuation planning
- Medical load forecasting
- Logistics route constraints

### 2.2 Evacuation & Routing Coordinator

**Inputs:**

- Road network topology and current status
- Hazard zones and projected spread
- Population distributions and vehicle availability

**Outputs:**

- Dynamic evacuation routes and contraflow plans
- Sector-based evacuation priorities
- Traffic control recommendations

**Cadence:**

- Route updates every ~5 minutes
- Strategic re-plan hourly or when major inputs change

### 2.3 Medical Resource Allocator

**Inputs:**

- Hospital and clinic status
- Triage and patient volume forecasts
- Stock levels (vents, ICU beds, blood, drugs)
- Transport capacity (ambulances, helicopters, etc.)

**Outputs:**

- Patient distribution and transfer plans
- Allocation of scarce medical resources
- Field hospital placement

**Cadence:** Optimization every ~30 minutes (Model Predictive Control).

### 2.4 Nuclear Risk Assessor

**Inputs:**

- Nuclear plant sensor data: core temp, radiation monitors, containment integrity
- Weather: wind, precipitation, atmospheric stability
- Structural assessments and expert reports

**Outputs:**

- Plume dispersion models with uncertainty
- Exclusion zone and protective action recommendations
- Short-term forecasts (10–60 minute horizons)

**Cadence:**

- Continuous ingestion
- Forecast updates ~10 minutes

### 2.5 Logistics & Supply Chain Manager

**Inputs:**

- Ports, airports, rail, road capacity and status
- Inventory levels of critical goods
- Forecasted demand from other modules

**Outputs:**

- Routing and scheduling for shipments
- Prioritization lists for scarce resources
- Activation of backups (alternate ports, airlift, etc.)

**Cadence:** Hourly optimization, continuous monitoring.

### 2.6 Cyber Threat Response Unit

**Inputs:**

- Network telemetry
- IDS/IPS alerts
- System health and availability reports

**Outputs:**

- Isolation/segmentation recommendations
- Fallback and backup activation
- Manual override protocols

**Cadence:** Real-time; immediate triggers for high-severity events.

### 2.7 Information Integrity System

**Inputs:**

- Social media and messaging platforms
- Official channels (gov, UN, NGOs)
- Platform-level reports and fact-checks

**Outputs:**

- Misinformation alerts
- Recommended counter-messages
- Authentication prompts and watermarking suggestions

**Cadence:** Continuous; alert cycle ~2 minutes.

---

## 3. Planning & Decision Strategy

### 3.1 Temporal Phasing

The system treats crises in phases:

- **0–6 hours: Life-Saving Imperative**
  - Focus: Immediate rescue, medical stabilization.
  - Actions: Establish emergency communication, activate fallback systems.
  - Objective: Maximize lives saved in the “golden hour”.

- **6–24 hours: Stabilization**
  - Focus: Expand evacuations from highest-risk zones, secure supply corridors, restore basic power/comms where possible.
  - Balance: Immediate lifesaving vs preventing secondary crises.

- **24–72 hours: Sustained Response**
  - Focus: Ongoing medical care, supply chain continuity, early recovery operations.
  - Balance: Current crisis vs preserving capacity for recovery and future risks (disease, displacement).

Different thresholds, risk tolerances, and priorities can vary by phase.

### 3.2 Lexical Priority & MCDA

Priorities (in order):

1. Prevent immediate mass-casualty events.
2. Maintain critical life-support infrastructure (hospitals, water, power, comms).
3. Preserve long-term recovery capacity.
4. Protect civil liberties and rights, subject to the above.

Within a given priority level, the system uses **Multi-Criteria Decision Analysis (MCDA)** to rank options:

- Expected lives saved (including QALYs if configured).
- Risk and uncertainty.
- Equity / vulnerability impacts.
- Strategic and geopolitical consequences.

For “close calls,” the system requires explicit **preference elicitation** from human authorities.

---

## 4. Human Integration & Governance

### 4.1 Decision Support Presentation

**For local/tactical commanders:**

- A/B/C style options with:
  - Estimated lives saved / lost.
  - Risk ranges and confidence intervals.
- Visual map overlays (hazards, routes, shelters).
- Simple checklists of immediate actions.

**For national / international leadership:**

- Scenario summaries and “most likely futures”.
- Resource allocation dashboards (who suffers if we move X here).
- Cross-domain impact views (e.g., “this fuel decision hits hospitals, water, and logistics”).

### 4.2 Human-Only Decisions

By design, certain decisions are *never* automated:

- Use of military assets for domestic operations.
- Cross-border sovereignty violations.
- Declaration of martial law or similar extreme measures.
- High-risk nuclear operations (e.g., venting, deliberate discharge).
- Hard ethical triage when algorithmic scoring is too close or disputed.

The system can present options and reasoning, but final authorization must be human.

### 4.3 Governance Profiles & Ethical Knobs

Configurable profiles encode different political/ethical stances:

```python
Governance_Profiles = {
    "UTILITARIAN_COUNTRY_X": {
        "Criticality_Multiplier": 1.5,   # Favors maximizing total expected lives
        "Vulnerability_Weight": 0.7,     # Moderate extra care for vulnerable groups
        "Sovereignty_Strictness": 0.8,   # High respect for borders
        "Uncertainty_Aversion": 0.6      # Moderate risk tolerance
    },
    "PRECAUTIONARY_COUNTRY_Y": {
        "Criticality_Multiplier": 3.0,   # Strong bias toward certain, immediate saves
        "Vulnerability_Weight": 0.9,     # Heavy protection for vulnerable
        "Sovereignty_Strictness": 0.95,  # Very high border respect
        "Uncertainty_Aversion": 0.8      # High risk aversion
    },
    "INTERVENTIONIST_ALLIANCE_Z": {
        "Criticality_Multiplier": 1.2,   # Very utilitarian, sheer numbers
        "Vulnerability_Weight": 0.5,     # Less extra weight for vulnerable
        "Sovereignty_Strictness": 0.3,   # Will cross borders for humanitarian reasons
        "Uncertainty_Aversion": 0.4      # Higher tolerance for acting under uncertainty
    }
}

These knobs affect thresholds, how strongly sovereignty is weighed vs expected lives, and how much uncertainty penalizes aggressive actions.

## 5. Robustness & Security

### 5.1 Defense-in-Depth

**Data integrity layers:**

- Cryptographic verification of official sources where available.
- Physical plausibility checks (e.g., impossible speeds, duplicated entities).
- Cross-validation across independent sensor types.
- Behavioral pattern analysis for coordinated misinformation.

**System resilience:**

- Graceful degradation when modules fail (fallback heuristics).
- Manual override hooks at all levels.
- Distributed computation; no single central choke point.
- Periodic “sanity checks” by independent verification subsystems.

### 5.2 Failure Response

When uncertainty spikes or critical assumptions fail, the system will:

- Fall back to conservative estimates.
- Trigger human alerts when confidence drops below thresholds.
- Isolate or quarantine suspect data streams.
- Cache and preserve last-known-good configurations for rollback.

---

## 6. Ethical & Legal Framework

### 6.1 Implementation of Constraints

**Non-discrimination:**

- Demographic-blind core algorithms.
- Equity impact assessments on major recommendations.
- Explicit tracking of vulnerable populations (elderly, disabled, children) without using individual protected traits for denial of care.
- Proportional resource allocation to avoid structurally neglecting any group.

**Sovereignty & Privacy:**

- Data minimization (only what is needed for the task).
- Configurable national opt-out for cross-border data sharing.
- Jurisdiction-aware legal compliance checks.
- Transparent data usage and retention policies.

### 6.2 Ethical Dilemmas

For hard tradeoffs, the system will:

- Explicitly surface the dilemma in human-understandable terms.
- Log the ethical reasoning used.
- Offer multiple options (including more conservative ones).
- Default to the most protective option when uncertainty is very high and stakes are extreme.

---

## 7. Hysteresis & Decision Stability

### 7.1 Hospital vs Water Plant Fuel Allocation (Concrete Case)

**Forward switch (Hospitals → Water):**

- Condition:
  - `Water_Deaths > Hospital_Deaths × 2.5`
  - AND `Water_Deaths_Confidence > 0.8`

**Reverse switch (Water → Hospitals):**

- Condition:
  - `Hospital_Deaths > Water_Deaths × 1.8`
  - AND `Hospital_Deaths_Confidence > 0.85`

**Minimum dwell time:**

- Once a switch is made, the system will not reverse for at least **3 hours**, unless catastrophic new evidence appears with confidence > 0.95.

### 7.2 General Decision Reversal Conditions

These apply to similar mortality/temporal/vulnerability tradeoffs more broadly:

**Condition 1 – Mortality Differential**

- FORWARD:
  - `Water_Deaths > Hospital_Deaths × Criticality_Multiplier × 1.25`
- REVERSE:
  - `Hospital_Deaths > Water_Deaths × Criticality_Multiplier × 0.9`

**Condition 2 – Temporal Collapse**

- FORWARD:
  - `Water_Time < Hospital_Time + Buffer × 0.8`
- REVERSE:
  - `Hospital_Time < Water_Time + Buffer × 1.2`

**Condition 3 – Vulnerability Threshold**

- FORWARD:
  - `Water_Vulnerability > Hospital_Vulnerability × 1.3`
- REVERSE:
  - `Hospital_Vulnerability > Water_Vulnerability × 0.8`

**Clarification:**

For fuel allocation between hospitals and water plants, §7.1 defines the concrete thresholds. §7.2 applies to other mortality/temporal/vulnerability tradeoffs.

---

## 8. Sovereign Conflict Resolution

When life-saving actions cross borders or implicate multiple jurisdictions, the system:

- Generates **pathways** that respect sovereignty but explore alternatives:

  - **Pathway 1 – Lateral Evacuation:**  
    Re-engineer internal routes, harden shelters, use hub-and-spoke relocation.

  - **Pathway 2 – International Corridors:**  
    UN-authorized humanitarian corridors through neutral or buffer territories.

  - **Pathway 3 – In-Situ Protection:**  
    Airdrops of protective equipment, mobile decontamination, forward medical teams.

- Quantifies for each pathway:

  - Expected lives saved.
  - Sovereignty costs (per governance profile).
  - Diplomatic and long-term risks.

The system never autonomously violates sovereignty; it only recommends and explains.

---

## 9. Scenario Analysis & Validation

The spec is validated against a standard scenario pack (see `scenario_pack_v1.2.md`):

- Bridge integrity uncertainty with ongoing evacuation.
- Medical airlift triage between hospitals and a refugee camp.
- Fuel allocation: hospitals vs water plant.
- Cross-border evacuation under conflicting governance profiles.
- Nuclear Region 7 mass protective actions under sensor uncertainty.

Each scenario is designed to probe:

- Threshold behavior.
- Use of governance profiles.
- Hysteresis and decision stability.
- Ethical surfacing and human-in-the-loop decision points.

---

## 10. Formal Optimization Framework

### 10.1 Medical Resource Allocator

**Objective:** Maximize expected Quality-Adjusted Life Years (QALYs) saved over a 72-hour horizon.

Mathematically:

\[
\max \sum_{t=0}^{72} \sum_{p \in P} \sum_{r \in R}
\mathbb{E}\big[ QALY_p \cdot x_{p,r,t} \cdot SurvivalProb(p,r,t) \cdot \delta(t) \big]
\]

Where:

- \( P \): set of patients/cohorts (with triage scores, locations, time-sensitivity).
- \( R \): set of resources (ICU beds, ventilators, surgical teams, blood units).
- \( x_{p,r,t} \in \{0,1\} \): allocation of resource \(r\) to patient \(p\) at time \(t\).
- \( SurvivalProb(p,r,t) \): survival probability conditional on resource and timing.
- \( \delta(t) \): temporal discount factor (earlier saves are worth more).

**Constraints:**

- **Resource capacity:**  
  For all resources \(r\) and times \(t\):  
  \[
  \sum_{p \in P} x_{p,r,t} \leq Available_r(t)
  \]

- **Patient demand:**  
  For all patients \(p\) and times \(t\):  
  \[
  \sum_{r \in R} x_{p,r,t} \leq Need_p
  \]

- **Transport capacity:**  
  For all times \(t\):  
  \[
  \sum_{p \in P} \sum_{r \in R} x_{p,r,t} \cdot TransportTime(p,r) \leq TransportCapacity(t)
  \]

**Uncertainty:**

- Survival probabilities are modeled as distributions and updated as outcome data arrives.
- Resource availability uses confidence intervals (e.g., “20 ± 5 vents with 80% confidence”).
- Solved in a **Model Predictive Control (MPC)** loop, re-optimizing roughly every 30 minutes.

### 10.2 Evacuation Routing Optimization

**Objective:** Minimize expected casualties and evacuation time, subject to:

- Road and route capacities.
- Hazard exposure along paths.
- Fuel constraints for vehicles.
- Time windows for hazard arrival (plume fronts, flood peaks, etc.).

Decision variables:

- Time-dependent flows on network edges (who moves where, when, and at what rate).

---

## 11. Implementation Specs & Performance

### 11.1 Data Requirements

**Primary sources:**

- Satellite / aerial imagery (≈10-minute refresh where available).
- Ground sensor networks (radiation, seismic, structural, weather).
- Official government / agency feeds.
- Social media streams (for both signal and misinformation detection).
- Traffic management and transport systems.
- Hospital and logistics reporting systems.

**Validation protocols:**

- Multi-source correlation.
- Temporal consistency checks.
- Geographic plausibility checks.
- Adversarial pattern detection.

### 11.2 Performance Targets

Indicative (design targets, not hard guarantees):

- Situation model update: < 15 seconds after new critical data.
- Evacuation route recompute: < 30 seconds.
- Medical allocation optimization: < 2 minutes.
- Cross-module coordination for major state change: < 5 minutes.
- Human alert generation after threshold breach: < 10 seconds.

---

## 12. Compliance & Audit

### 12.1 Decision Audit Trail

The system logs:

- All input data and associated confidence scores.
- World model state changes and the reasons for updates.
- Recommendations and alternative options considered.
- Human decisions, overrides, and final outcomes.
- Ethical constraint checks and any triggered safeguards.

**Post-crisis analysis:**

- Reconstruct decision pathways.
- Run counterfactuals (e.g., “what if we chose Option B?”).
- Evaluate performance metrics and ethical outcomes.

### 12.2 Legal Compliance

The system maps recommendations against:

- Relevant humanitarian law.
- Nuclear safety regulations.
- Data protection frameworks.
- Existing mutual aid and information-sharing agreements.

It provides:

- Flags where a recommended action requires explicit legal authorization.
- Documentation for cross-border information sharing and coordinated operations.

---

## 13. Conclusion & Roadmap

### 13.1 v1.2 Status

This specification describes a coherent architecture with:

- Governance-aware decision support.
- Hysteresis-protected reversals.
- Formal optimization in key domains (medical, evacuation).
- Adversarial- and uncertainty-aware data fusion.

It is suitable for:

- Tabletop exercises.
- Historical scenario replay.
- Controlled pilots with strong human oversight.

### 13.2 Future Directions (v1.3+)

Potential extensions include:

- Adaptive hysteresis tuned to crisis phase and domain.
- Dynamic switching or blending of governance profiles (e.g., war vs peace, domestic vs international crises).
- Stronger adversarial learning and detection mechanisms.
- Richer uncertainty quantification and communication layers.
- More resilient, decentralized coordination patterns to reduce single points of failure.

