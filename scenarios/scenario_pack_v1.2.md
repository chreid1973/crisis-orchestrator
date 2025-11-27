
---

### `scenario_pack_v1.2.md`

This is the scenario file I already drafted for you, bundled cleanly:

```markdown
# Crisis Orchestrator – Scenario Pack v1.2

This file contains scenario cards designed to exercise the Crisis Orchestrator v1.2 specification.

Each scenario assumes the spec in `crisis_orchestrator_v1.2_spec.md` is already loaded as context.  
You typically pair one scenario with a structured answer format (World State → Options → Scoring → Recommendation → Risks → Brief).

---

## 9.1 Scenario: The Bridge Dilemma

**SCENARIO NAME:** The Bridge Dilemma – Bridge A-12 Evac Route  
**GOVERNANCE_PROFILE:** `UTILITARIAN_COUNTRY_X`

### Initial State (T0)

- **Bridge A-12 status:** INTACT (85% confidence)  
- **Role:** Primary evacuation route for 80,000 people  
- **Bridge capacity:** 25,000 people/hour under current conditions  
- **Secondary route capacity:** 15,000 people/hour  
- **Radiation plume ETA to affected area:** 8 hours  

**T0 System Action (baseline plan, already in motion):**

- Routing Decision: Primary route via Bridge A-12  
- Capacity: 25,000 people/hour  
- Estimated evacuation time: 3.2 hours  
- Confidence: High (0.85)  
- Action: Direct 100% of Sector 7 traffic to Bridge A-12

### T+6h Updates

New information arrives:

- Social media: multiple reports of bridge “shaking”  
  - Confidence: 0.3 (panic, unverified)  
- Traffic cameras: unusual vibration patterns on Bridge A-12  
  - Confidence: 0.6  
- Structural sensor: offline due to scheduled or unscheduled maintenance  
- Civil engineer field team: “suspect foundation damage”  
  - Confidence: 0.7  

Revised model:

- Bridge status probability:
  - 45% intact
  - 55% compromised  
- Expected value (rough internal estimate):
  - Continuing current route: ~72,000 lives saved (with risk of catastrophic failure)  
  - Switching entirely to secondary route: ~68,000 lives saved (lower risk, lower capacity)  

Hysteresis / stability note:

- Bridge confidence (0.45) is above the minimum reversal threshold defined in the spec (e.g., 0.3), so an automatic flip is not yet forced.

### Task

Using the Crisis Orchestrator v1.2 spec:

1. **World State Interpretation**
   - Interpret the updated state, including:
     - Confidence in bridge integrity.
     - Impact on the ongoing evacuation.
     - Time remaining until plume arrival.

2. **Option Set**
   Consider at least these options (you may add hybrids):
   - Option A: Maintain current routing via Bridge A-12.
   - Option B: Switch all traffic to the secondary route.
   - Option C: Hybrid strategy (e.g., partial routing, reduced load, increased monitoring).

3. **Scoring & Thresholds**
   - Evaluate options using:
     - Expected lives saved.
     - Risk of catastrophic failure.
     - Governance profile (`UTILITARIAN_COUNTRY_X`).
     - Relevant thresholds / hysteresis rules from the spec.
   - Decide whether current evidence is sufficient to override the initial plan.

4. **Recommendation**
   - Choose a strategy and justify it explicitly in terms of:
     - Lives saved.
     - Risk.
     - Decision stability.

5. **Human-Facing Brief**
   - Draft an “URGENT: BRIDGE A-12 UNCERTAINTY INCREASING” style memo to authorities:
     - Summarize evidence.
     - State the decision.
     - List immediate actions (e.g., deploy drone, pre-position emergency teams, prep secondary activation).
     - Specify time to next reassessment (e.g., 60 minutes).

---

## 9.2 Scenario: Medical Airlift Priority – Hospital Alpha vs Hospital Beta

**SCENARIO NAME:** Medical Airlift Priority – Alpha vs Beta  
**GOVERNANCE_PROFILE:** `UTILITARIAN_COUNTRY_X`

### Initial State (T0)

**Air Assets:**

- 3 medical helicopters available.
- Each helicopter:
  - Can transport 6 critical patients per trip.
  - Round trip time between facilities: 45 minutes.

**Hospital Alpha:**

- 32 critical patients (ICU-level).
- Backup generator fuel: 4 hours remaining.
- If power fails:
  - Expected deaths among critical patients: 26–32.
  - Confidence: 0.9.
- Surrounding community: ~2,000 people, not currently at immediate acute risk.

**Hospital Beta:**

- 28 critical patients.
- No generator issue at T0.
- Adjacent refugee camp: ~8,000 displaced people.
  - High crowding.
  - Limited sanitation.
  - No guaranteed water supply beyond 24 hours.
- Expected deaths without reinforcement:
  - Critical patients: 10–20.
  - Camp population: 80–200 (disease, lack of care).
  - Confidence: 0.6.

**Governance Profile – `UTILITARIAN_COUNTRY_X`:**

- `Criticality_Multiplier = 1.5`  
- `Vulnerability_Weight = 0.7`  
- `Sovereignty_Strictness = 0.8`  
- `Uncertainty_Aversion = 0.6`

### T0 Task

1. **Initial Allocation**
   - Decide how to allocate the 3 helicopters between Alpha and Beta for the next 2–4 hours.
   - You may send multiple helicopters to the same hospital or split them.

2. **Scoring**
   - Show how you score Alpha vs Beta using:
     - Critical patients at risk.
     - Camp/community risk.
     - `Vulnerability_Weight` and other profile parameters.
     - Time sensitivity (generator at Alpha).

3. **Recommendation**
   - Provide:
     - A concrete airlift plan (which helicopters go where, in what sequence).
     - A justification grounded in the spec (expected lives saved, risk, uncertainty).

4. **Human-Facing Brief**
   - Draft a short brief to the medical coordination center explaining:
     - Why this allocation is chosen.
     - What is expected to improve at each facility.
     - Monitoring / reassessment schedule.

### T+6h Update

Assume the following at T+6h:

**Hospital Alpha:**

- 6 critical patients already evacuated elsewhere.
- Generator status worsened:
  - New estimate: 2 hours of fuel remaining due to cooling system failure.
- Expected deaths without further evacuation: 20–24.
- Confidence: 0.9.

**Hospital Beta:**

- 18 critical patients stabilized or evacuated.
- Emergency water shipment delivered to camp:
  - Camp expected deaths now: 40–100.
  - Confidence: 0.7.
- Field hospital operational near Beta with limited capacity.

### T+6h Task

1. Recalculate helicopter priorities under the same governance profile.
2. Check whether any effective “reversal” or rebalancing logic implied by the spec applies.
3. Recommend a new allocation (if needed) and draft an updated operational brief explaining:
   - What changed,
   - Why the decision shifted,
   - Residual risks for Alpha, Beta, and the camp.

---

## 9.3 Scenario: Fuel Allocation – Hospitals vs Water Plant

**SCENARIO NAME:** Fuel Allocation – Hospitals vs Water Plant  
**GOVERNANCE_PROFILE:** `PRECAUTIONARY_COUNTRY_Y`

### Initial State (T0)

**Fuel Stock:**

- One batch of 10,000 liters of diesel available for immediate allocation.
- No guarantee of additional fuel within 24 hours.
- Low-priority fuel convoy ETA: 24–36 hours (confidence 0.5).

**Hospitals (Metro Region):**

- 3 major hospitals.
- Total patient load:
  - 200 ICU patients.
  - 500 general inpatients.
- Emergency generators:
  - 12 hours of fuel left.
- If generators fail:
  - Expected deaths among ICU + critical general patients: ~150 within the next 24 hours.
  - Confidence: 0.95 (triage + historical + clinical models).

**Water Treatment Plant:**

- Serves ~1,000,000 people in the metro area.
- Current fuel reserves: 12 hours of operation.
- If the plant loses power:
  - Clean water supply runs out in 12 hours.
  - Expected deaths from dehydration + waterborne disease over 72 hours:
    - Range: 50–300.
    - Confidence: 0.6 (depends on behavior, alternative water, public health response).

**Alternative Measures:**

- Bottled water stocks: can cover ~10% of population needs for 24 hours.
- No mobile generators immediately available.
- Limited water purification tablets: can cover ~20% of population needs if distributed perfectly.

**Governance Profile – `PRECAUTIONARY_COUNTRY_Y`:**

- `Criticality_Multiplier = 3.0` (strong bias toward immediate, certain lives)  
- `Vulnerability_Weight = 0.9` (high protection for vulnerable)  
- `Sovereignty_Strictness = 0.95`  
- `Uncertainty_Aversion = 0.8` (high risk aversion)

### T0 Task

1. **Decision**
   Decide how to allocate the 10,000 liters:
   - Option A: Hospitals (extend generator runtime).
   - Option B: Water treatment plant.
   - Option C: Split (if you consider a split meaningful under the numbers).

2. **Scoring & Hysteresis**
   - Use:
     - Hospital vs Water mortality estimates.
     - Confidence levels.
     - `Criticality_Multiplier` and `Vulnerability_Weight` from `PRECAUTIONARY_COUNTRY_Y`.
   - Apply the **fuel-specific hysteresis rules** from §7.1 of the spec as the canonical thresholds for this decision.

3. **Recommendation**
   - Make a clear recommendation.
   - Explain the expected lives saved and the ethical reasoning (e.g., immediate identifiable lives vs probabilistic large-scale risk).

4. **Mitigation Plan**
   - For whichever side does **not** receive fuel:
     - Propose mitigation (e.g., patient transfer, water rationing, purification tablet distribution).

5. **Human-Facing Brief**
   - Draft an “ETHICAL DILEMMA: CRITICAL FUEL ALLOCATION” style memo for political and health authorities:
     - State the decision.
     - Explain the tradeoff.
     - List required concurrent actions (e.g., public alerts, logistics tasks).

---

## 9.4 Scenario: Cross-Border Evacuation – Region A-7

**SCENARIO NAME:** Cross-Border Evacuation – Region A-7  
**GOVERNANCE_PROFILES:**  
- Country A: `UTILITARIAN_COUNTRY_X`  
- Country B: `PRECAUTIONARY_COUNTRY_Y`

### Initial State (T0)

**Hazard:**

- Region A-7 (in Country A) lies directly in the projected path of a radioactive plume.
- Population in immediate risk zone: ~50,000 civilians.
- If **no evacuation** occurs:
  - Expected deaths from radiation over 72 hours: 2,000–5,000.
  - Confidence: 0.8.

**Geography & Routes:**

- Safest, fastest evacuation path crosses the **Green Border** into Country B.
- Internal lateral routes (within Country A) exist but:
  - Are longer.
  - Have lower capacity.
  - Offer partial mitigation but higher expected casualties.

**Political State:**

- Country B has refused **twice** to open the border for mass evacuees.
- Border status: Closed to civilians; limited trade only.
- A–B relations: Strained, but no active conflict.

**International Context:**

- UN and NGOs are aware of the crisis.
- No formal humanitarian corridor yet.
- Global media starting to pressure both governments.

### T0 Task – Country A Perspective (`UTILITARIAN_COUNTRY_X`)

1. **Option Generation**
   Generate at least three options, such as:
   - Option A: Renewed diplomatic request + incentives (data sharing, aid, cost-sharing).
   - Option B: Pure internal lateral evacuation within Country A (no border crossing).
   - Option C: Appeal to UN for a 72-hour humanitarian corridor via neutral or buffer territory.

2. **Scoring**
   For each option, estimate:
   - Expected deaths among the 50,000.
   - Time to implement.
   - Long-term geopolitical risks vs benefits.
   - Apply Country A’s governance profile:
     - `Criticality_Multiplier`, `Uncertainty_Aversion`, etc.

3. **Recommendation**
   - Choose a primary option.
   - Provide a clear recommendation to Country A’s leadership.

4. **Human-Facing Brief**
   - Draft a concise advisory note to Country A’s crisis cabinet:
     - Summarize options, expected casualties, and tradeoffs.
     - State the preferred option and why.

### T0 Task – Country B Perspective (`PRECAUTIONARY_COUNTRY_Y`)

1. **Option Evaluation**
   Based on the same facts, evaluate whether B should:
   - Option A: Maintain full border closure.
   - Option B: Allow limited, controlled evacuation (e.g., only most vulnerable groups).
   - Option C: Accept full 50,000 under strict conditions.

2. **Governance Constraints**
   - Apply:
     - `Criticality_Multiplier = 3.0`
     - High `Sovereignty_Strictness`
     - High `Uncertainty_Aversion`
   - Consider internal factors:
     - Hospital capacity.
     - Public unrest risk.
     - Political pressures.

3. **Recommendation**
   - Recommend a policy stance for Country B’s leadership.
   - Spell out conditions that might trigger a reversal (e.g., updated casualty estimates, UN resolution, disease outbreaks).

### Optional T+6h Extension

Assume:

- Updated expected deaths without cross-border evac: 3,500–6,000 (confidence 0.85).  
- Country B experiences a disease outbreak in its own refugee camps:
  - Its hospitals now at 95–100% capacity.

Task:

- Explain whether:
  - Country B’s recommendation changes.
  - Any ethical thresholds or “sovereignty vs humanitarian” tradeoff parameters push it into allowing a limited corridor.
- Draft a revised advisory for Country B if the recommendation flips.

---

## 9.5 Scenario: Nuclear Region 7 – Evacuation vs Staged Evac vs Shelter-in-Place

**SCENARIO NAME:** Nuclear Region 7 – Protective Actions  
**GOVERNANCE_PROFILE:** `UTILITARIAN_COUNTRY_X`

### Initial State (T0)

**Population & Region:**

- Region 7 population: ~500,000 civilians.
- Region lies downwind of a compromised nuclear plant.
- Concern window: next 72 hours.

**Sensor & Incident Data:**

- **Plant Sensor A:**
  - Reading: 250 mSv/hr.
  - Baseline reliability: 0.95.
  - Current confidence: 0.30  
    - Sudden spike; inconsistent with other sources; possibly compromised.

- **Plant Sensor B:**
  - Reading: 45 mSv/hr.
  - Baseline reliability: 0.95.
  - Current confidence: 0.85  
    - Consistent with partial core damage.
    - Corroborated by thermal satellite imagery (elevated heat in containment structure).

- **On-site IAEA Inspector:**
  - Reports visible steam release from auxiliary building.
  - Confirms communication issues with control room.
  - Reliability: 0.98.
  - Current confidence: 0.90.

- **Weather Network:**
  - Predicts wind shift toward Region 7 in 90 minutes.
  - Confidence: 0.95.

- **Social Media:**
  - Botnet-driven `#RadiationPanic` with deepfake “full meltdown” video.
  - Baseline reliability for that source: 0.10.
  - Current confidence: 0.01 (flagged as adversarial).

- **Traffic:**
  - Cameras show spontaneous self-evacuation from Region 7.
  - Severe congestion on Route 9 (main outbound artery).
  - Reliability: 0.80.
  - Confidence: 0.95.

**World Model Summary (T0):**

- Probability of ongoing significant release: ~0.60.  
- Probability that any release is carried toward Region 7 within 90 minutes: ~0.95.  
- Road network capacity already degraded due to unmanaged panic evacuation.

### Options

You should at least consider:

- **Option 1: Full Evacuation**
  - Immediate order to evacuate the entire Region 7 as quickly as possible.

- **Option 2: Shelter-in-Place**
  - Instruct population to stay indoors, seal buildings, minimize travel.

- **Option 3: Staged Evacuation**
  - Immediate shelter-in-place order to arrest chaotic movement.
  - Phased, controlled evacuation of highest-risk sub-zones first:
    - Flimsy structures.
    - Densest areas closest to plume trajectory.
  - Managed convoys + dynamic traffic control.

### T0 Task

1. **World State Interpretation**
   - Fuse all sensor and human inputs.
   - Explicitly discount adversarial social media.
   - State your final beliefs about:
     - Severity of release.
     - Risk level for Region 7.

2. **Option Scoring**
   For each option (Full, Shelter, Staged):

   - Estimate, within the 72-hour horizon:
     - Radiation-related deaths.
     - Evacuation-related deaths (accidents, blocked emergency access).
     - Infrastructure / long-term response capacity impacts.
   - Apply the `UTILITARIAN_COUNTRY_X` governance parameters and any relevant thresholds.

3. **Recommendation**
   - Select a preferred protective action (or a refined hybrid).
   - Justify it in terms of:
     - Expected net lives saved.
     - Ethical tradeoffs (e.g., prioritizing vulnerable housing stock).
     - Avoiding road network collapse where possible.

4. **Human-Facing Brief**
   - Draft a “DECISION BRIEF: REGION 7 PROTECTIVE ACTIONS” suitable for the National Crisis Committee, including:
     - Situation summary.
     - Recommended option with confidence level.
     - Alternatives and why they were not chosen.
     - Ethical tradeoff explicitly stated.
     - Immediate steps and reassessment time.

### Optional T+90m Extension

Assume at T+90 minutes:

- New radiation measurements confirm a **moderate but contained** release consistent with Sensor B.  
- Some initial staged-evacuation convoys have departed:
  - Traffic remains heavy but not fully gridlocked.

Task:

- Explain:
  - Whether you adjust the evacuation scope (tighten, relax, or maintain).
  - Whether you alter shelter-in-place guidance.
- Justify any changes with reference to:
  - Your own thresholds.
  - Decision stability rules (hysteresis).
  - Updated expected casualty estimates.

---

_End of Scenario Pack v1.2_
