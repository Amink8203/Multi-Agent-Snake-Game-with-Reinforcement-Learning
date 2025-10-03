# Multi-Agent Snake Game with Reinforcement Learning

## 🎯 Project Overview

This project implements a competitive two-player Snake game where two AI agents learn to play against each other using **Q-Learning** reinforcement learning algorithm. The project explores different agent architectures and reward systems to create intelligent Snake agents capable of strategic gameplay.

## 🎮 Game Description

The game features:
- **Two AI-controlled snakes** competing on a 20x20 grid
- **Dynamic food spawning** that both snakes compete for
- **Collision detection** with walls, self, and other snake
- **Real-time visualization** using Pygame
- **Persistent learning** with Q-table saving/loading

## 🧠 Reinforcement Learning Implementation

### Core Algorithm: Q-Learning
- **Temporal Difference Learning** for value function approximation
- **Epsilon-greedy exploration** with decay
- **Experience-based learning** from state-action-reward transitions

### Key Parameters:
- **Learning Rate (α):** 0.1 - 0.2
- **Discount Factor (γ):** 0.9
- **Epsilon Decay:** 0.998
- **Grid Size:** 20x20

## 🏗️ Project Architecture

### Three Model Implementations

#### **Model 1: Basic Q-Learning Agent**
- **State Space:** 12-dimensional binary features
  - Direction indicators (4): left, right, up, down
  - Food location relative to head (4): up, down, left, right  
  - Wall proximity (4): up, down, left, right
- **Q-Table Size:** (2,2,2,2,2,2,2,2,2,2,2,2,4)
- **Learning Rate:** 0.1

#### **Model 2: Enhanced Collision-Aware Agent**
- **State Space:** 16-dimensional binary features
  - All Model 1 features plus:
  - Snake collision detection (4): left, right, up, down positions
- **Q-Table Size:** (2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,4)
- **Learning Rate:** 0.2
- **Enhanced Policy:** Avoids predicted collisions with opponent

#### **Model 3: Optimized Strategic Agent**
- **State Space:** Same as Model 2 (16-dimensional)
- **Refined Reward System:** Balanced penalties and rewards
- **Strategic Improvements:** 
  - Enhanced self-preservation
  - Better opponent prediction
  - Optimized epsilon starting value (1.0)

## 🎯 Reward System Design

### Positive Rewards
- **+6000:** Eating food (Model 2&3) / +5000 (Model 1)
- **+400:** Moving directly toward food (within 3 cells)
- **+20:** General movement toward food
- **+500:** Safe movement (avoiding collisions)
- **+4000-7000:** Winning head-to-head collision

### Negative Penalties
- **-5000 to -8000:** Death (collision, out of bounds)
- **-1000:** Moving toward walls
- **-500:** Moving toward collision danger
- **-20 to -50:** Moving away from food

## 📊 State Representation

Each agent observes:
```python
state = (
    dir_left, dir_right, dir_up, dir_down,      # Current direction
    snack_up, snack_down, snack_right, snack_left,  # Food location
    wall_up, wall_down, wall_left, wall_right,     # Wall proximity
    snake_left, snake_right, snake_up, snake_down  # Collision detection (Models 2&3)
)
```

## 🔧 Technical Implementation

### Dependencies
```python
import pygame      # Game visualization and control
import numpy as np # Q-table management and array operations
import random      # Action exploration and environment randomness
import matplotlib.pyplot as plt  # Performance visualization
from tkinter import messagebox   # User interaction dialogs
```

### Key Classes

#### `Cube`
- Represents individual snake segments and food
- Handles position, movement, and rendering

#### `Snake_1/Snake_2/Snake_3`
- Implements Q-Learning agents with different capabilities
- Manages state observation, action selection, and learning
- Handles collision detection and reward calculation

### Game Loop Architecture
1. **State Observation:** Each agent observes current environment
2. **Action Selection:** Epsilon-greedy policy with learned Q-values
3. **Environment Update:** Move snakes, check collisions, update food
4. **Reward Calculation:** Compute rewards based on actions and outcomes
5. **Q-Table Update:** Apply Q-Learning update rule
6. **Policy Update:** Decay exploration (epsilon)

## 📈 Performance Analysis

The project includes comprehensive performance tracking:

- **Episode-wise reward plotting** for both agents
- **Convergence analysis** showing learning progression  
- **Competitive dynamics** between co-evolving agents

### Observed Behaviors:
- **Zig-zag reward patterns** due to competitive nature
- **Strategic emergence** as agents learn opponent patterns
- **Balanced gameplay** with neither agent dominating consistently

## 🚀 Getting Started

### Prerequisites
```bash
pip install pygame numpy matplotlib
```

### Running the Models

#### Model 1 (Basic):
```python
# Load and run the first model section in the notebook
# Q-tables saved as: model_1_s1.npy, model_1_s2.npy
```

#### Model 2 (Collision-Aware):
```python
# Load and run the second model section
# Q-tables saved as: model_2_s1.npy, model_2_s2.npy
```

#### Model 3 (Optimized):
```python
# Load and run the third model section
# Q-tables saved as: model_3_s1.npy, model_3_s2.npy
# Includes performance visualization
```

### Controls
- **ESC:** Save Q-tables during training
- **Close Window:** Option to save Q-tables before exit

## 📁 Project Structure

```
proj/
├── CA6.ipynb              # Main project notebook with all implementations
├── README.md              # This documentation
├── Description/           # Project requirements and documentation
│   └── AI-CA6-Description.pdf
├── model_1_s1.npy        # Model 1 Snake 1 Q-table
├── model_1_s2.npy        # Model 1 Snake 2 Q-table
├── model_2_s1.npy        # Model 2 Snake 1 Q-table
├── model_2_s2.npy        # Model 2 Snake 2 Q-table
├── model_3_s1.npy        # Model 3 Snake 1 Q-table
└── model_3_s2.npy        # Model 3 Snake 2 Q-table
```

## 🔬 Research Insights

### Multi-Agent Learning Challenges
- **Non-stationary environment** due to opponent learning
- **Credit assignment** in competitive scenarios
- **Exploration vs exploitation** balance in adversarial settings

### Model Progression
1. **Model 1:** Established basic Q-Learning foundation
2. **Model 2:** Added collision awareness and strategic depth  
3. **Model 3:** Refined reward balance and strategic optimization

### Key Findings
- **Collision detection** significantly improves performance
- **Reward engineering** critical for desired behaviors
- **Co-evolution** leads to emergent strategic behaviors

## 🎓 Educational Value

This project demonstrates:
- **Reinforcement Learning** fundamentals with Q-Learning
- **Multi-agent systems** and competitive learning
- **State space design** for complex environments
- **Reward engineering** for behavior shaping
- **Game AI development** with real-time visualization

## 🔧 Future Enhancements

Potential improvements:
- **Deep Q-Networks (DQN)** for larger state spaces
- **Multi-agent reinforcement learning** algorithms (MADDPG, QMIX)
- **Opponent modeling** for strategic prediction
- **Hierarchical reinforcement learning** for complex strategies
- **Tournament-based evaluation** across multiple agents

## 📝 Notes

- **Training Time:** Agents require substantial training for convergence
- **Visualization:** Can be disabled for faster training
- **Hyperparameters:** Tuned for balanced competitive gameplay
- **Reproducibility:** Random seeds can be set for consistent results
