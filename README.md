# Reinforcement Learning for Battery Management in Electricity Markets

## Project Overview
This project explores reinforcement learning (RL) techniques for optimizing decision-making in an electricity market environment. Our agent represents a market player equipped with battery storage, aiming to maximize profit by strategically managing charging, discharging, and electricity selling based on fluctuating market conditions.

We implemented a custom Gymnasium environment called `ElectricityMarketEnv`, modeling realistic market dynamics, including stochastic electricity pricing and energy demand patterns. Various RL algorithms were evaluated, with PPO emerging as the most effective, especially when combined with ensemble learning.

## Features
- Custom RL Environment Models an electricity market with battery storage.
- Realistic Market Dynamics Uses real-world electricity demand patterns and pricing trends.
- Reinforcement Learning Algorithms Implements and compares PPO, DDPG, TD3, and A2C.
- Fast-Learning Method Early termination when the battery reaches zero state of charge.
- Ensemble Learning Improves policy robustness and generalization.

## Environment Design
### State Space
The agent observes six state variables
- Battery State of Charge (SoC) Current stored energy.
- Battery Capacity Maximum energy storage, which degrades over time.
- Electricity Price Fluctuates based on the time of day and season.
- Electricity Demand Modeled using a seasonal duck curve.
- Hour of the Day Affects both demand and price patterns.
- Season Impacts energy consumption and market trends.

### Action Space
- Continuous values
  - Positive values Charging the battery.
  - Negative values Discharging to meet demand or sell to the grid.
- Actions are constrained by battery capacity and efficiency.

### Reward Function
- Negative reward for charging (cost).
- Positive reward for selling electricity (profit).
- Battery degradation acts as an implicit constraint.

## Data Sources
- Electricity Demand Modeled using the duck curve (different for each season).
- Electricity Prices Analyzed from real-world hourly trends.
- Market Noise Incorporated to introduce variability.

## Reinforcement Learning Experiments
### Algorithms Implemented
- Proximal Policy Optimization (PPO)
- Deep Deterministic Policy Gradient (DDPG)
- Twin Delayed DDPG (TD3)
- Advantage Actor-Critic (A2C)

### Key Findings
- PPO outperforms DDPG and TD3 in this stochastic environment.
- Fast-learning method enables quicker training by terminating episodes early.
- Transfer learning failed due to differences in state and action spaces.
- Seasonal models performed worse than a single model trained on all seasons.
- Ensemble learning significantly improved performance, reducing variance and increasing profitability.

## Repository Structure
- code Contains the main reinforcement learning algorithms and model training scripts.
- env Implements the custom Gymnasium environment used for training.
- presentation Includes presentation materials summarizing the project.
- simulation Contains simulation scripts for testing trained models in different scenarios.
- trained_models Stores saved models after training.
- training_logs Logs and TensorBoard files for monitoring training progress.
- notebooks Jupyter notebooks used for analysis and experimentation.

## Jupyter Notebooks
- A2C_different_advantages.ipynb Investigates the effects of different advantage functions in A2C.
- comparison_between_known_algorithms.ipynb Compares various RL algorithms in our environment.
- Comparison_between_separate_model_for_each_season.ipynb Evaluates whether training a separate model for each season improves performance.
- investigating_results_with_reliable.ipynb Analyzes the reliability and consistency of the trained models.
- PPO_Ensemble.ipynb Implements and evaluates ensemble learning with PPO.
- transfer_learning.ipynb Examines the feasibility of transfer learning between different environments.

## Installation
1. Clone this repository
   ```bash
   git clone httpsgithub.comyour-repo-name.git
   cd your-repo-name
   ```
2. Install dependencies
   ```bash
   pip install -r requirements.txt
   ```
3. Run training
   ```bash
   python train.py
   ```

## Usage
- Modify `config.json` to change hyperparameters and environment settings.
- Use `evaluate.py` to test trained models.
- Visualize results using TensorBoard
  ```bash
  tensorboard --logdir=runs
  ```

## Future Work
- Introduce multi-agent RL for competitive market dynamics.
- Implement sudden market crashes to increase complexity.
- Explore meta-learning to enhance adaptability.

## Authors
- Hussein Rayan (323116319)
- Alina Sudakov

## License
This project is licensed under the MIT License.
