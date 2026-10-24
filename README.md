# Lunz-ARC
# Multi-Agent Reinforcement Learning with Centralized Training and Decentralized Execution (CTDE)

## LUNZ-ARC: A Multi-Agent AI Architecture for Plasma Stabilization

## 1. Overview

The **LUNZ-ARC project** proposes a multi-agent artificial intelligence architecture designed to learn stable, coordinated control policies for a future nuclear fusion reactor.

The central idea is to combine a foundation model, six specialized AI agents, twelve functional control areas, a shared representation of the plasma state, and **Multi-Agent Reinforcement Learning (MARL)** using **Centralized Training and Decentralized Execution (CTDE)**.

The objective is to develop a system capable of observing plasma behavior, predicting instabilities, coordinating control decisions, and adapting its learned policies to changing plasma conditions.

The architecture is a research proposal. Its effectiveness must be demonstrated through simulation, experimental data, and controlled validation before any connection to a physical fusion device.

## 2. Core Concept

The proposed system consists of four main components:

1. **Astra-6 Foundation Model** — supports research, model development, data analysis, and the improvement of specialized agents.
2. **Six Specialized AI Agents** — address twelve functional areas related to plasma observation, control, stability, and performance.
3. **Multi-Agent Reinforcement Learning** — trains the agents to develop coordinated policies based on feedback from a plasma simulator and, eventually, validated experimental data.
4. **Independent Safety Supervisor** — verifies proposed actions against predefined operational constraints before they can reach physical control systems.

The foundation model is not intended to make every real-time control decision. Fast operational decisions should be executed by specialized policies with predictable latency and measurable behavior.

## 3. System Architecture

```text
                  ASTRA-6 FOUNDATION MODEL
              Research, analysis, and development
                            |
                            v
                SHARED PLASMA-STATE MODEL
             State estimation, prediction, uncertainty
                            |
                            v
                SIX SPECIALIZED AI AGENTS
                            |
                 12 Functional Control Areas
                            |
                            v
                 COORDINATION MECHANISM
             Joint policy and action arbitration
                            |
                            v
               INDEPENDENT SAFETY SUPERVISOR
             Constraints, validation, fallback
                            |
                            v
                 PHYSICAL CONTROL SYSTEMS
                            |
                            v
                    FUSION PLASMA
                            |
                            v
                  SENSORS AND FEEDBACK
                            |
                            +----> Next control cycle
```

During training, a centralized learning component can access global state information and the joint actions of all agents. During deployment, each operational policy acts using the observations and shared information available to it, without relying on the training-only centralized critic.

The coordination mechanism must be designed so that its inputs, communication requirements, and latency are compatible with decentralized execution.

## 4. The Six Specialized Agents

Each agent is assigned two primary functional areas. The twelve-area division is an initial engineering proposal and may be revised after examining the available sensors, actuators, and plasma-control requirements.

| Agent | Primary Area | Secondary Area |
|---|---|---|
| **Agent 1 — Perception** | Sensor-data fusion | Plasma-state estimation and uncertainty |
| **Agent 2 — Equilibrium** | Plasma-shape control | Position and magnetic-equilibrium coordination |
| **Agent 3 — Stability** | Instability detection | Perturbation forecasting and disruption-risk estimation |
| **Agent 4 — Actuator Management** | Heating-system management | Plasma-current profile control |
| **Agent 5 — Fuel and Exhaust** | Fuel supply and density regulation | Impurity monitoring, divertor behavior, and exhaust heat-load management |
| **Agent 6 — Coordination** | Action arbitration | Joint performance optimization under operational constraints |

### Agent 1: Perception

Processes diagnostic signals and constructs a consistent estimate of the current plasma state.

It must account for sensor noise, missing measurements, uncertainty, and differences in sampling rates.

### Agent 2: Equilibrium

Evaluates the plasma's shape, position, and magnetic configuration. Its policy aims to reduce control error while remaining within the constraints imposed by the physical control system.

### Agent 3: Stability

Identifies potentially unstable behavior and estimates the likelihood and severity of future disturbances. Predictions must include uncertainty rather than treating every model output as certain.

### Agent 4: Actuator Management

Evaluates control options involving heating and plasma-current-profile regulation. It must consider actuator limits, response delays, and interactions with other control objectives.

### Agent 5: Fuel and Exhaust

Monitors fuel-related variables, plasma density, impurities, and exhaust conditions. Its decisions must respect the limits of the relevant physical systems.

### Agent 6: Coordination

Combines the objectives and recommendations of the other agents into a coherent control policy. It is responsible for managing conflicting objectives and prioritizing stability and constraint compliance over performance improvements.

The coordination design must not assume that six agents are inherently better than one. Its value must be demonstrated experimentally against simpler alternatives.

## 5. Reinforcement Learning Strategy

The proposed training methodology is **Multi-Agent Reinforcement Learning with Centralized Training and Decentralized Execution (CTDE)**.

CTDE separates the information available during training from the information required during deployment.

### 5.1 Centralized Training

During training, the learning system may use:

- Global plasma-state estimates.
- Observations collected by all agents.
- The joint actions proposed by the agents.
- Simulator dynamics and predicted future states.
- Outcomes, performance metrics, and safety-constraint violations.
- Historical trajectories and validated experimental datasets.

A centralized critic can estimate the long-term value of joint actions. This helps the learning process evaluate how the combined behavior of the agents affects the system.

A suitable initial algorithm to investigate is **Multi-Agent Proximal Policy Optimization (MAPPO)**. Other methods should be evaluated against it rather than excluded in advance.

### 5.2 Decentralized Execution

During deployment, the centralized critic is removed from the operational decision loop.

Each specialized policy acts using its available observations and permitted shared state information. The coordination mechanism combines or reconciles their recommendations where necessary.

The operational system must maintain predictable execution times, defined communication interfaces, explicit actuator constraints, and independent safety checks.

### 5.3 Reward Design

The learning objective should reflect measurable physical and operational goals.

Potential reward components include:

- Plasma-stability performance.
- Tracking accuracy for the desired plasma state.
- Recovery from disturbances.
- Robustness to uncertainty and changes in operating conditions.
- Efficient use of available actuators.
- Avoidance of unsafe states and constraint violations.

A single unconstrained reward is insufficient. Safety requirements must be represented by explicit constraints and independently enforced safeguards, not merely by penalties that a learned policy might trade against other rewards.

The reward function and its weights must be established through domain-specific analysis and tested for undesirable behavior.

## 6. Shared Plasma-State Model

The agents require a consistent representation of the plasma state.

The proposed state model may combine:

- Magnetic diagnostic measurements.
- Plasma position and shape estimates.
- Density and temperature estimates.
- Current-profile information.
- Indicators of instability and disruption risk.
- Actuator status and operating limits.
- Time-series history.
- Predictions and uncertainty estimates.

A physics-informed, data-driven predictive model may help estimate how the plasma could evolve under candidate actions.

Its predictions must be calibrated and validated against suitable reference data. Model uncertainty, extrapolation beyond the training domain, and discrepancies between simulation and experiment must be explicitly considered.

## 7. Learning and Validation Pipeline

The project should progress through the following stages.

### Stage 1 — Research and Formalization

Define the control objectives, observation spaces, action spaces, agent responsibilities, safety constraints, and evaluation metrics.

Identify available plasma simulators, diagnostic datasets, existing control strategies, and relevant research results.

### Stage 2 — Environment Development

Build or configure a simulation environment capable of representing the plasma behaviors relevant to the selected control tasks.

Validate the environment against reference data before relying on it for policy training.

### Stage 3 — Initial Policy Training

Train baseline controllers and individual specialized agents. Establish a reproducible training pipeline and compare candidate reinforcement-learning algorithms.

### Stage 4 — Multi-Agent Coordination

Train the agents under CTDE. Evaluate whether shared learning and coordinated policies improve stability, robustness, and performance relative to independent policies.

### Stage 5 — Robustness Testing

Evaluate the system under:

- Sensor noise and missing data.
- Changes in model parameters.
- Disturbances and uncertain initial conditions.
- Actuator limitations and communication delays.
- Operating conditions not encountered during training.
- Agent disagreements and coordination failures.

### Stage 6 — Hardware-in-the-Loop Validation

Test the learned policies with a simulated plant and representative control hardware, initially without authority over a live plasma.

Any later experimental deployment requires specialist review, appropriate authorization, and independently validated safety measures.

## 8. Safety and Reliability

The learned agents must never be the sole mechanism responsible for protecting the reactor.

The system should include:

- An independent safety supervisor.
- Validated operational limits for all commanded actuators.
- Monitoring for out-of-distribution states and model uncertainty.
- Defined behavior when an agent becomes unavailable or produces an invalid output.
- A tested fallback to an approved baseline controller.
- Complete logging of observations, proposed actions, accepted commands, and outcomes.

When agent recommendations conflict, the system must have a deterministic and auditable arbitration strategy. If the system cannot establish that an action is acceptable, it must reject the action or transition to an approved safe operating state.

## 9. Evaluation Metrics

The architecture must be evaluated against a conventional controller and simpler learning-based baselines.

| Category | Proposed Measurements |
|---|---|
| Stability | Instability frequency, severity, and duration |
| Control accuracy | Error relative to the desired plasma state |
| Disturbance response | Recovery rate and recovery time |
| Robustness | Performance across uncertain and unseen conditions |
| Actuator efficiency | Control effort and resource consumption |
| Reliability | Constraint violations, invalid actions, and fallback events |
| Coordination | Benefit or degradation attributable to multi-agent cooperation |
| Computational performance | Inference latency, communication overhead, and execution reliability |

The system should advance only when its performance improvements are statistically credible, reproducible, and achieved without compromising predefined safety constraints.

## 10. Role of the Astra-6 Foundation Model

Astra-6 is the proposed foundation-model component of the LUNZ-ARC architecture.

Its intended responsibilities include:

- Analyzing scientific literature and experimental datasets.
- Supporting the design of agent objectives and training environments.
- Generating candidate hypotheses and test scenarios.
- Assisting in failure analysis and evaluation.
- Supporting the development and refinement of specialized policies.
- Helping researchers interpret training results.

Astra-6 should not be assumed to have direct access to the physical plasma or to possess a validated plasma-control policy. Such capabilities would require explicit implementation and experimental validation.

The model's name represents the proposed role in this project; the architecture does not depend on any unverified capability of a specific commercial model.

## 11. Research Objectives

The primary objective is to determine whether a coordinated multi-agent architecture trained through CTDE can learn a more robust and effective plasma-stabilization policy than selected single-agent and conventional-control baselines.

Secondary objectives include:

1. Establishing a reliable shared plasma-state representation.
2. Developing specialized agents with clearly defined responsibilities.
3. Learning coordinated policies without sacrificing safety constraints.
4. Improving robustness to uncertainty and changing plasma conditions.
5. Establishing a reproducible, measurable validation framework.

## 12. Scope and Limitations

LUNZ-ARC is currently a research concept, not a validated reactor-control system.

The proposed architecture does not establish that fusion can be sustained commercially, that a 100 MW electric-output target is achievable, or that a multi-agent controller will outperform existing methods.

The design focuses on the AI control architecture. It does not resolve the reactor's independent engineering challenges, including plasma confinement, neutron-resistant materials, tritium breeding, heat extraction, maintenance, and net electrical power production.

Those issues remain separate requirements for any future commercial fusion plant.

## 13. Conclusion

The LUNZ-ARC proposal combines a foundation model, six specialized agents, twelve functional control areas, a shared predictive plasma-state model, and multi-agent reinforcement learning using CTDE.

The research strategy is to train centrally in a validated environment, deploy specialized policies under decentralized execution constraints, and enforce safety through an independent supervisory system.

The project's central hypothesis is that **coordinated, prediction-aware multi-agent learning can improve plasma-stabilization performance under uncertainty**.

That hypothesis must be tested, measured, and compared against existing approaches. The first milestone is a reproducible simulation prototype that shows whether the proposed architecture delivers meaningful improvement before we consider any physical integration.
