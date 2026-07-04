🤖 Reinforcement Learning from Scratch

A beginner-friendly series of 7 Jupyter notebooks that build up Reinforcement Learning
concepts step by step — from the basic Markov Decision Process to comparing SARSA vs
Q-Learning on the Cliff Walking problem.

Every notebook has: simple theory in plain language → working Python code → graphs →
a short takeaway.


📚 Notebooks

01️⃣ Markov Decision Process (MDP)

What it is: The basic framework used to describe any RL problem — States, Actions,
Rewards, Transition Probabilities, and a Discount Factor.

What's inside:


A simple 4x4 grid world (16 states)
4 actions: UP, DOWN, LEFT, RIGHT
A reward matrix (-1 per step, +10 at the goal)
Agent moves randomly to show how states change
Heatmap of which cells the agent visited


Takeaway: No learning happens here — it's just to understand what an MDP looks like.


02️⃣ Dynamic Programming

What it is: When we already know the environment's rewards and transitions, we can
directly calculate the best possible values using the Bellman Equation — no trial and error.

What's inside:


Value Iteration — repeatedly updates values until they stop changing
Policy Iteration — alternates between evaluating a policy and improving it
Both methods extract a final optimal policy from the grid world


Takeaway: Fast and exact, but only works if we know the environment's full model —
which is rarely true in real life.


03️⃣ Monte Carlo

What it is: Now we don't know the model — we learn only from full episodes of
experience by averaging the returns (total rewards) we observe.

What's inside:


generate_episode() — runs the agent randomly until it reaches the goal
First-Visit MC — counts a state only the first time it appears in an episode
Every-Visit MC — counts a state every time it appears
Side-by-side heatmap comparing both methods


Takeaway: No model needed, but we must wait for a whole episode to finish before
learning anything.


04️⃣ Temporal Difference (TD) Learning

What it is: A mix of Monte Carlo and Dynamic Programming — no model needed, but we can
update our estimates after every single step, not just at the end of an episode.

What's inside:


TD(0) prediction using the update rule: V(s) = V(s) + α[R + γV(s') - V(s)]
The term R + γV(s') - V(s) is called the TD Error
A graph showing TD error decreasing over episodes (proof that learning is happening)


Takeaway: The most practical approach — learns online, one step at a time.


05️⃣ SARSA

What it is: An on-policy control algorithm — the agent learns the value of the
policy it is actually following, including its random exploration steps.

Environment: CliffWalking-v1 — a 4x12 grid where falling off the cliff gives -100 reward.

What's inside:


Epsilon-greedy action selection (mostly best action, sometimes random)
Update rule uses the next action actually taken: Q(s,a) += α[R + γQ(s',a') - Q(s,a)]
Reward graph + final learned policy


Takeaway: Because it accounts for its own exploration risk, SARSA learns a safer path
that stays away from the cliff edge.


06️⃣ Q-Learning

What it is: An off-policy control algorithm — the agent always learns assuming it
will take the best possible next action, even if it doesn't actually take it.

Environment: FrozenLake-v1 — a slippery 4x4 grid where the agent must reach the goal
without falling into a hole.

What's inside:


Epsilon-greedy with decay (explores a lot early, less later)
Update rule uses the best possible next action: Q(s,a) += α[R + γ·max(Q(s',:)) - Q(s,a)]
Q-table heatmap + success rate evaluation (~77%)


Takeaway: Learns the shortest/optimal path, but ignores the risk of its own exploration.


07️⃣ Cliff Walking — SARSA vs Q-Learning

What it is: Training both algorithms on the same environment to directly compare
on-policy vs off-policy behavior.

What's inside:


Both SARSA and Q-Learning trained side by side
Reward comparison graph (moving average)
Final greedy paths plotted on the grid for both algorithms


Takeaway: SARSA takes the long, safe route; Q-Learning takes the short, risky route
right along the cliff edge — a clear, visual proof of the on-policy vs off-policy trade-off.


🧠 How the Concepts Build Up

MDP → Dynamic Programming → Monte Carlo → Temporal Difference → SARSA → Q-Learning → Cliff Walking
(setup)   (model-based)      (model-free)    (model-free, TD)   (on-policy) (off-policy)  (comparison)

🛠️ Setup

bashpip install numpy matplotlib seaborn "gymnasium[toy-text]"

Run any notebook with:

bashjupyter notebook

📦 Requirements


Python 3.10+
numpy, matplotlib, seaborn
gymnasium[toy-text] (for FrozenLake-v1 and CliffWalking-v1 in notebooks 05-07)
