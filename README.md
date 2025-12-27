# Reinforcement Learning: From SnakeFrog to Taxi-v3

This repository documents the transition from a custom-built heuristic environment to a standardized Reinforcement Learning (RL) framework using **OpenAI Gymnasium**.

## 🚀 Project Evolution

### 1. The Homegrown "SnakeFrog"
Originally, I developed a custom environment called **SnakeFrog**. This phase focused on establishing the **Agent-Environment loop** and building a custom OpenCV-based `VideoRecorder` to visualize the agent's behavior. The logic was primarily heuristic (hand-coded).

### 2. The Taxi-v3 Substitution
I swapped the custom engine for the **Gymnasium Taxi-v3** environment. This provided a standardized 5x5 grid challenge with 500 discrete states:
* **Goal:** Pick up a passenger (Blue) and deliver them to a destination (Magenta).
* **Rewards:** -1 per step, -10 for illegal actions, and +20 for success.



### 3. Implementing Q-Learning
I moved from "guessing" to "learning" by implementing a **Q-Table**. This "brain" stores the expected future rewards for every action in every state.

The core learning mechanism is the **Bellman Equation**:
$$Q(s, a) \leftarrow (1 - \alpha) Q(s, a) + \alpha [R + \gamma \max Q(s', a')]$$

---

## 📊 Sensitivity Analysis (Grid Search)

To understand the "personality" of different agents, I conducted a **Factorial Sensitivity Analysis**. I trained 9 different "brains" (3x3 grid) for 5,000 episodes each, varying the core hyperparameters.

### The Parameters
* **Alpha ($\alpha$):** The Learning Rate. Determines how much the agent values new information vs. old memory.
* **Gamma ($\gamma$):** The Discount Factor. Determines the "time horizon" (Short-sighted vs. Visionary).

### The Metrics
Each brain was tested over **20 independent trips** to measure:
1. **Avg_Success_Reward:** How efficiently the taxi navigates (higher is better).
2. **Truncated_Count:** Reliability (how many times the agent failed to finish within 200 steps).

| Alpha | Gamma | Avg_Success_Reward | Truncated_Count | Success Rate |
| :--- | :--- | :--- | :--- | :--- |
| 0.1 | 0.9 | +12.4 | 0 | 100% |
| 0.5 | 0.5 | +4.2 | 2 | 90% |
| 0.9 | 0.1 | -185.0 | 14 | 30% |



---

## 🛠️ Technical Implementation

### Custom HUD Video Recording
I modified the `VideoRecorder` class to act as a diagnostic tool. Using `cv2.putText`, the recorder overlays:
* **Current Step Count**
* **Cumulative Reward**
* **Trip Status (Success/Failure)**

This allowed for "Failure Analysis," where I captured videos of **Truncated runs (-200 reward)** to identify infinite loops or "Wall-Humping" behaviors in the agent's logic.

### Automated Data Pipeline
The project utilizes **Pandas** to store results from the sensitivity analysis, allowing for quick pivot-table generation and performance visualization.

```python
# Analysis Pivot Table Example
df.pivot(index='Alpha', columns='Gamma', values='Avg_Success_Reward')
