LUNZ-ARC: Trustworthy AI for Tokamak Plasma Control
<img width="2220" height="1170" alt="fig4_benchmark" src="https://github.com/user-attachments/assets/300ac2f3-522c-47e7-966b-91e78cd0dbe4" />


📖 Overview
LUNZ-ARC is a Multi-Agent Reinforcement Learning (MARL) architecture designed for the safe, robust stabilization of magnetically confined plasmas in tokamak fusion reactors.

Traditional pure Reinforcement Learning (RL) approaches suffer from sample inefficiency and unpredictable behavior under extreme perturbations, making them unsafe for direct deployment in nuclear systems. LUNZ-ARC solves this by combining Centralized Training with Decentralized Execution (CTDE) and an Independent Safety Supervisor (Fallback).

Key features include:

Multi-Agent Decomposition: 6 specialized agents (Perception, Equilibrium, Stability, Actuators, Fuel/Escape, Coordination) managing 12 functional control areas.

Sample Efficiency: Achieves stable policies with only 12,000 training episodes (utilizing MAPPO).

100% Survival Rate: Maintains plasma stability under severe operational stresses (clustered pulses, sensor noise, sustained forcing) where pure RL fails.

Safety-First Design: A deterministic fallback mechanism overrides the RL policy when the instantaneous risk metric exceeds the safety threshold (
R
>
0.55
R>0.55).

📂 Repository Structure
text
lunz-arc/
├── agents/             # Multi-agent RL definitions (MAPPO implementation)
├── envs/               # Synthetic low-order plasma simulation environment
├── safety/             # Independent Safety Supervisor & Fallback controller
├── training/           # Scripts for Centralized Training
├── evaluation/         # Scripts for generating Kaplan-Meier and Phase-space plots
├── figures/            # Output directory for publication-ready plots
├── data/               # Paired seeds and trained model weights (checkpoints)
├── requirements.txt    # Python dependencies
└── README.md
🚀 Getting Started
Prerequisites
Ensure you have Python 3.10+ installed. It is highly recommended to use a virtual environment:

bash
python -m venv lunz-env
source lunz-env/bin/activate  # On Windows use `lunz-env\Scripts\activate`
Installation
Clone the repository and install the required dependencies:

bash
git clone https://github.com/yourusername/lunz-arc.git
cd lunz-arc
pip install -r requirements.txt
Training the Agents
To run the Centralized Training using MAPPO (12,000 episodes):

bash
python training/train_mappo.py --episodes 12000 --seeds 12 --env synthetic_plasma
Note: Trained model checkpoints will be saved in the /data/checkpoints directory.

Evaluation & Plot Generation
To evaluate the LUNZ-ARC architecture (RL + Fallback) against baselines (Pure RL, Classical Feedback, No Control) under stress profiles (e.g., Clustered Pulses, Sensor Noise):

bash
python evaluation/run_survival_analysis.py --profile clustered_pulses --seed 5000
This script will generate the Kaplan-Meier survival curves and phase-space trajectory plots (exported as PDF/PNG in the /figures folder).

📊 Simulation & Results (Paper Figures)
The architecture was tested on a synthetic low-order plasma model (without actual tokamak experimental data) to isolate the control logic.

Figure 1 & 2 (Phase Space & Time Series): Shows the RL + Fallback (green) successfully bounding the plasma trajectory within the safe envelope (dashed red lines), while pure RL (orange) terminates early.

Figure 3 (Kaplan-Meier): Demonstrates a flat survival probability 
S
^
(
t
)
=
1.0
S
^
 (t)=1.0 for LUNZ-ARC across all six stress profiles.

Figure 4 (Q-Table): Illustrates the learned actuator conservation strategy (62% of states converge to Action 0 under nominal conditions).

(Insert your published plots here in the README later)

📝 Citation
If you use this code or architecture in your research, please cite our paper (currently under review at Nuclear Fusion):

bibtex
@article{lunz2026arc,
  title={LUNZ-ARC: A Multi-Agent Reinforcement Learning Architecture with Centralized Training and Decentralized Execution for Robust Tokamak Plasma Stabilization},
  author={Lunz, Luiz Guilherme},
  journal={Nuclear Fusion (Under Review)},
  year={2026}
}
⚠️ Disclaimer
This is a research framework. LUNZ-ARC is currently evaluated on a synthetic low-order model. It is not a validated control system for a physical nuclear reactor. Any physical deployment requires high-fidelity MHD simulation (e.g., JOREK), Hardware-in-the-Loop (HIL) testing, and independent safety certification.

🤝 Contributing & Contact
Contributions from the fusion and RL communities are welcome!

Author: Luiz Guilherme (Lunz Research Group)

Contact: [Seu e-mail institucional ou LinkedIn]
