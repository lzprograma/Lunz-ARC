
<img width="2220" height="1170" alt="fig4_benchmark" src="https://github.com/user-attachments/assets/300ac2f3-522c-47e7-966b-91e78cd0dbe4" />


LUNZ-ARC: Trustworthy AI for Tokamak Plasma Control
Learning Unified Neural Zone - Autonomous Reactor Control
A Multi-Agent Reinforcement Learning Architecture with Centralized Training and Decentralized Execution (CTDE) for Robust Plasma Stabilization.

📖 1. Overview
Controlling magnetically confined plasmas in tokamak fusion reactors is one of the most formidable engineering challenges of our era. Maintaining stability requires sub-millisecond reactions to magnetohydrodynamic (MHD) instabilities while strictly respecting operational safety boundaries.

While pure Reinforcement Learning (RL) offers powerful data-driven optimization, it suffers from two fatal flaws for nuclear applications:

Sample Inefficiency: It requires millions of episodes to converge.

Unconstrained Behavior: "Black-box" exploratory actions can drive the system into irreversible high-risk regimes (plasma termination or wall damage).

LUNZ-ARC is a proposed architecture that bridges this gap. It decomposes the plasma control problem into six specialized functional agents, coordinated centrally during training, and supervised by an independent safety fallback during execution.

🧠 2. The Architecture & Theoretical Formulation
The LUNZ-ARC framework is structured around four foundational pillars designed to reconcile high-performance AI optimization with ironclad safety guarantees.

2.1 State-Space and Dynamic Model
The synthetic plasma environment tracks normalized macroscopic state variables, encapsulating:

Horizontal displacement: 
x
∈
[
−
1
,
1
]
x∈[−1,1]

Plasma velocity: 
v
∈
[
−
1
,
1
]
v∈[−1,1]

Instability index: 
i
∈
[
0
,
1.25
]
i∈[0,1.25]

Instantaneous risk metric: 
R
(
x
,
v
,
i
,
d
)
∈
[
0
,
1
]
R(x,v,i,d)∈[0,1], where 
d
d represents external loading and forcing factors.

2.2 Multi-Agent Decomposition
Instead of a single monolithic neural network, LUNZ-ARC divides control responsibilities among six specialized agents, each targeting distinct physical domains (Perception, Equilibrium, Stability, Actuators, Fuel/Escape, Coordination).

Analogy: Just like an elite pit crew in Formula 1 does not rely on a single mechanic to refuel, change tires, and adjust wings simultaneously, LUNZ-ARC assigns specialized "agents" to specific tasks, coordinated by a "chief engineer".

2.3 Centralized Training with Decentralized Execution (CTDE)
Training: Utilizes the Multi-Agent Proximal Policy Optimization (MAPPO) algorithm. A centralized critic evaluates global plasma states and joint actions across 12,000 episodes (with 12 paired seeds). This allows agents to learn cooperative, non-competitive strategies.

Execution: The centralized critic is stripped away. The six agents operate in a fully decentralized manner with minimal latency.

2.4 Independent Safety Supervisor (Fallback Mechanism)
During execution, an independent safety supervisor continuously monitors the system. If the instantaneous risk metric exceeds the critical safety threshold (
R
>
0.55
R>0.55), the system immediately overrides the RL policy and engages a deterministic classical feedback controller. The AI does not replace the engineer; it acts as a high-speed co-pilot with an infallible mechanical safety net.

🔬 3. Experimental Protocol
To evaluate the architecture under rigorous scientific standards, the system was subjected to a synthetic low-order plasma model across six distinct stress profiles:

Double Pulses: Rapid sequential disturbances.

Sustained Forcing: Continuous high-amplitude external loading.

Rising Ramp: Gradually escalating perturbation loads.

Clustered Pulses: Grouped bursts of instability-triggering events.

Altered Parameters: Shifts in internal plant dynamics.

Increased Sensor Noise: High-variance stochastic noise injected into diagnostic sensors.

Performance was benchmarked against four configurations: Pure RL, RL + Fallback (LUNZ-ARC), Classical Feedback, and No Control.

📊 4. Key Results
<img width="2220" height="1170" alt="fig4_benchmark" src="https://github.com/user-attachments/assets/e70d8bb2-3e52-48ff-81de-d8c9dcd07841" />
<img width="666" height="315" alt="frame_40" src="https://github.com/user-attachments/assets/e737359f-80a6-431b-9b80-ad3a5ee52267" />
<img width="2220" height="1350" alt="fig5_sobrevivencia" src="https://github.com/user-attachments/assets/c10feccd-e0cc-4203-b298-ce0ed05adb4c" />
<img width="2220" height="1200" alt="fig2_fases" src="https://github.com/user-attachments/assets/fad18bf8-bc01-4c31-b21f-3362bcb5d56f" />
<img width="2220" height="1470" alt="fig3_camara" src="https://github.com/user-attachments/assets/7701678c-365a-43f2-aa56-5d0169fbf828" />
<img width="2160" height="2790" alt="fig1_episodio" src="https://github.com/user-attachments/assets/bcd4df43-3b3a-4492-aed0-a1362aa7ec2f" />


Q-Table Policy Analysis: Under nominal conditions, 62% of the 6,435 visited state-space cells converged to Action 0 (
u
m
=
−
1
,
u
a
=
0
u 
m
​
 =−1,u 
a
​
 =0), demonstrating a learned energy-conservation strategy to minimize unnecessary actuator wear.

Phase-Space Dynamics: Pure RL and No Control frequently spiral out of the safe operational bounding box (crossing 
R
>
0.55
R>0.55). LUNZ-ARC tightly bounds all trajectories within the stable core of the phase space.

Survival Analysis (Kaplan-Meier): Under Clustered Pulses and Sensor Noise, pure RL survival degrades to ~60%. LUNZ-ARC achieves a flat survival probability of 
S
^
(
t
)
=
1.0
S
^
 (t)=1.0 across all tested stress regimes.

Poloidal Cross-Section: While unmanaged plasmas deform and collapse into the chamber wall, LUNZ-ARC maintains symmetric, well-centered flux surfaces throughout the entire 25-second discharge window.

🚀 5. Future Work
This study validates the LUNZ-ARC architecture on a synthetic model. The next phases of the project involve:

Migrating from synthetic low-order models to high-fidelity magnetohydrodynamic (MHD) simulation codes (e.g., JOREK, M3D-C1).

Preparing for Hardware-in-the-Loop (HIL) validation with representative control hardware.

Publishing the full methodology and results in a peer-reviewed journal (Nuclear Fusion).

📝 6. Citation
If you reference this architecture in your research, please cite the project whitepaper:

bibtex
@article{lunz2026arc,
  title={LUNZ-ARC: A Multi-Agent Reinforcement Learning Architecture with Centralized Training and Decentralized Execution for Robust Tokamak Plasma Stabilization},
  author={Lunz, Luiz Guilherme},
  journal={Lunz Research Group (Pre-print)},
  year={2026}
}
⚠️ Disclaimer
This is a research framework. LUNZ-ARC is currently evaluated on a synthetic low-order model. It is not a validated control system for a physical nuclear reactor. Any physical deployment requires high-fidelity MHD simulation, HIL testing, and independent safety certification.

Developed by Luiz Guilherme | Lunz Research Group
