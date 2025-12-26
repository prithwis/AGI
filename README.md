# AGI Training Ground: From Physics to Reinforcement Learning

This repository documents an academic journey into **Artificial General Intelligence (AGI)** and **Reinforcement Learning (RL)**. It begins with custom-built environments to understand physics and modular architecture, progressing toward industry-standard benchmarks like Gymnasium's Taxi and Lunar Lander.

## 🚀 Project Evolution

The project is structured as a series of evolving environments, each introducing a new layer of AGI complexity:

### 🟢 FrogSnakeWorldV1: The Base
- **Concept:** Simple coordinate-based tracking.
- **Logic:** "Teleportation" movement where snakes move directly toward the target.
- **Goal:** Establishing the core Pygame rendering and Video Capture pipeline.

### 🟡 FrogSnakeWorldV2: Physics & Momentum
- **Concept:** Introduction of **Control Theory**.
- **Logic:** Snakes use acceleration, velocity, and friction. They must manage momentum to avoid overshooting the target.
- **Senses:** Implements relative observations (the snake only "sees" the distance/angle to the prey).

### 🔴 FrogSnakeWorldV3 & V3R: The RL Framework
- **Concept:** Decoupling the "Brain" from the "Body."
- **Logic:** The snake no longer knows how to chase; it receives an **Action** (0-3) from an external `Agent` class.
- **Reward Shaping (V3A):** Implements a **Dense Reward Function** to provide the agent with a "success signal" based on spatial proximity and directional progress.

## 🛠️ Architecture

The code follows a strictly modular design to ensure scalability:
- **`World` Class:** Handles environment physics and state transitions.
- **`Agent` Class:** Decides on actions based on observations (currently utilizing `RandomAgentV3`).
- **`VideoRecorder`:** A robust OpenCV/FFmpeg pipeline for recording and embedding simulations in Google Colab.

## 📊 Objective Function
The agent's success is measured by a cumulative reward signal:
$$R = \sum_{t=0}^{T} r_t$$
Where $r_t$ is calculated based on minimizing the distance $d$ between the snake and the frog:
- $r = +1.0$ if $\Delta d < 0$ (progress)
- $r = -1.1$ if $\Delta d \geq 0$ (stagnation/regression)
- $r = +100$ for target capture.

## 🛠️ Requirements
- Python 3.x
- Pygame
- OpenCV
- Gymnasium
- FFmpeg (for video encoding)

## 🏁 Next Steps
- [ ] Integration with **Gymnasium Taxi-v3**.
- [ ] Implementation of **Q-Learning** and **Deep Q-Networks (DQN)**.
- [ ] Comparison of sparse vs. dense reward structures.

---
**License:** [Apache 2.0](LICENSE)
