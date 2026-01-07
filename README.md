# Reinforcement Learning: The "City Expert" World Model (Taxi77)

This repository documents the evolution of a Reinforcement Learning agent, moving from a basic heuristic loop to a custom **7x7 World Model** featuring specialized drivers for distinct urban maps.

## 🚀 Project Evolution

### 1. SnakeFrog & Taxi-v3
* **SnakeFrog:** Established the basic Agent-Environment loop and custom OpenCV `VideoRecorder`.
* **Taxi-v3:** Transitioned to the Gymnasium standard 5x5 grid. Implemented **Q-Learning** using the Bellman Equation:
$$Q(s, a) \leftarrow (1 - \alpha) Q(s, a) + \alpha [R + \gamma \max Q(s', a')]$$

### 2. Sensitivity Analysis (Hyperparameter Tuning)
Conducted a grid search on **Alpha** (Learning Rate) and **Gamma** (Discount Factor) to identify the optimal "agent personality."
* **Result:** High-stability agents (100% success) were achieved with a low Alpha (0.1) and high Gamma (0.9).

---

## 🏙️ The "Taxi77" World Model
The final phase, **Taxi77**, moves beyond generic training to **Spatial Specialization**.

### Multi-City Parameterization
I developed four symbolic maps—**Arrah, Balia, Chappra, and Dhanbad**—and trained four expert drivers: **Arun, Bimal, Chitra, and Dilip**. 

* **Localized Intelligence:** Each driver is an "expert" in their own city map but fails in others. This demonstrates that the agent has encoded a **World Model** (a specific spatial reality) rather than just a general "driving" script.
* **Garage Start:** Every mission begins at a fixed "Garage" at (3, 3) to allow for consistent pathfinding comparison across different maps.
* **Occupancy HUD:** The taxi dynamically displays its status: **"V"** (Vacant) while searching and **"P"** (Passenger) once the passenger is secured.



### Technical Implementation
* **Environment:** Custom `MarsTaxi7x7` class supporting dynamic `wall_offsets`.
* **Visualization:** OpenCV (cv2) for real-time status overlays, wall rendering, and "Mission Success" frames.
* **Evaluation:** Used Pandas to track `Avg_Success_Reward` and `Truncated_Count` to identify where specific drivers "got lost" in foreign cities.

---

## 🛰️ Next Step: Lunar Lander
Having mastered discrete grids, the next mission is **Lunar Lander**. This marks the transition from spatial "Mental Maps" to **Continuous State Spaces**, where the agent must master the physics of gravity and velocity using Deep Q-Networks (DQN).
