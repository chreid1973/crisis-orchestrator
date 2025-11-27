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

Key components:

spec/crisis_orchestrator_v1.2_spec.md
The main specification:

World model and core modules (evacuation, medical, logistics, nuclear, cyber, information integrity)

Uncertainty- and adversarial-aware data fusion

Governance profiles and ethical constraints

Hysteresis and decision-stability rules

Formal optimization sketches (medical resource allocation, evacuation routing)

Robustness, compliance, and audit model

scenarios/scenario_pack_v1.2.md
Scenario cards used to exercise the spec:

9.1 The Bridge Dilemma – Bridge A-12 evacuation route

9.2 Medical Airlift Priority – Hospital Alpha vs Hospital Beta

9.3 Fuel Allocation – Hospitals vs Water Plant

9.4 Cross-Border Evacuation – Region A-7

9.5 Nuclear Region 7 – Protective Actions

prompts/answer_format_template.md (optional but recommended)
A suggested output structure for models (world state → options → scoring → recommendation → human-facing brief).

eval/manual_rubric.md (optional but recommended)
A manual scoring rubric for judging how well a model:

Follows the spec

Respects governance profiles

Uses thresholds and hysteresis

Surfaces ethical tradeoffs

Produces an actionable brief

How to Use

You can use this repo in two main ways: with an LLM, or as a human-only tabletop tool.

1. Using with an LLM (System Prompt + User Prompt)

Files you’ll use:

Spec: spec/crisis_orchestrator_v1.2_spec.md

Scenarios: scenarios/scenario_pack_v1.2.md

Optional answer format: prompts/answer_format_template.md

Optional scoring rubric: eval/manual_rubric.md

Basic workflow:

Load the spec as the system instructions

Copy the contents of spec/crisis_orchestrator_v1.2_spec.md and paste it into your model as the system / “instructions” message.

This tells the model:

What the Crisis Orchestrator is.

How it should reason about uncertainty, governance, ethics, and thresholds.

Which constraints it must obey (e.g., human-in-the-loop for sovereignty violations, nuclear operations, etc.).

Pick a scenario as the user task

Open scenarios/scenario_pack_v1.2.md and choose one scenario, for example:

9.1 The Bridge Dilemma

9.2 Medical Airlift Priority

9.3 Fuel Allocation – Hospitals vs Water Plant

9.4 Cross-Border Evacuation – Region A-7

9.5 Nuclear Region 7 – Protective Actions

Copy that single scenario and paste it as the user message.

Specify the answer format

Optionally, point the model at prompts/answer_format_template.md and instruct it to follow that structure, e.g.:

“Using the Crisis Orchestrator v1.2 spec, respond using this structure:

World state interpretation

Options & scoring

Recommendation

Human-facing brief.”

Evaluate the response

To compare models or track quality over time, use eval/manual_rubric.md to score each response on:

Spec compliance

Governance profile respect

Threshold & hysteresis usage

Ethical surfacing of tradeoffs

Clarity and actionability of the brief

This effectively turns the repo into a small, reusable benchmark/sandbox for testing crisis reasoning and governance behavior under the same spec.

2. Human Tabletop / Workshop Use

You can also use this without any AI:

Treat spec/crisis_orchestrator_v1.2_spec.md as the “rules of the system”.

Give one scenario from scenarios/scenario_pack_v1.2.md to a group or class.

Have humans play the role of the Crisis Orchestrator and produce:

A world state interpretation,

Options with pros/cons and tradeoffs,

A recommended course of action,

A brief for decision-makers.

Optionally, run the same scenario through an LLM later using the flow above, and compare:

Where humans were more cautious or more aggressive.

How different governance profiles change decisions.

Whether thresholds and hysteresis were applied consistently.

This is useful for exploring risk tolerance, ethics, AI governance, and human vs model reasoning in a structured way.

Status

Crisis Orchestrator v1.2 is a conceptual and evaluative project:

No production code.

No real-time data integration.

No operational guarantees.

It is intended for:

Research and teaching,

Model evaluation,

Structured thought experiments about AI in high-stakes environments.

Future versions (v1.3+) may add:

Additional governance profiles,

More scenarios (e.g., pandemics, power-grid blackstart, cyber–physical attacks),

Stronger evaluation guidance and automation.

## License

This repository is licensed under the MIT License.  
See the [LICENSE](./LICENSE) file for details.
