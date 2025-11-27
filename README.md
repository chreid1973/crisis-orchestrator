# Crisis Orchestrator v1.2

Crisis Orchestrator v1.2 is a **specification and scenario suite** for an AI-assisted crisis decision-support system.

It is not an implementation.  
It’s a structured “brain spec” plus test scenarios you can use to:

- Explore how an AI *should* reason in high-stakes emergencies.
- Benchmark different models on the same crisis problems.
- Run tabletop exercises and thought experiments about AI governance, ethics, and uncertainty.

---

## Goals

This project aims to:

- Define a **world model** and modular architecture for multi-hazard crises
  (nuclear incidents, infrastructure failure, medical overload, cross-border emergencies).
- Encode **governance profiles** and ethical “knobs” so behavior changes by jurisdiction and values.
- Use **hysteresis and thresholds** to avoid unstable, flip-flopping decisions.
- Provide **realistic scenario cards** that stress-test:
  - Uncertainty handling  
  - Conflicting objectives  
  - Sovereignty vs humanitarian imperatives  
  - Triage and resource allocation under pressure  

---

## Repository Structure

Suggested layout (you can adjust as needed):

```text
crisis-orchestrator/
  README.md
  spec/
    crisis_orchestrator_v1.2_spec.md
  scenarios/
    scenario_pack_v1.2.md
  prompts/
    answer_format_template.md        # (optional) A standard output format for models
  eval/
    manual_rubric.md                 # (optional) Notes on how you score responses
