# Policy: 
A policy is simply a rule or strategy that an agent learns from experience which tells it what action to take in a given situation.
                                                            or
A policy is a learned decision-making function that tells the agent what action to take in a particular state.

In simple words:
Situation (State)
        ↓
What should I do? (Action)

**Example:** Suppose a robot is learning navigation.
State: Robot is near wall,
Policy says: Turn Right,
Another state: Robot sees goal nearby,
Policy says: Move Forward,

**Mathematically: 
A policy is often written as:**
**π(s)=a**,

**1. Deterministic Policy**
In a deterministic policy, the agent always chooses the same action for a given state.
One State → One Fixed Action,
e.g.:
State: Robot sees a wall,
Policy: Always turn right,
Whenever the robot sees the wall, it will always turn right,
So the decision is fixed and predictable. 

**2. Stochastic Policy**
In a stochastic policy, the agent chooses actions based on probabilities.
One State → Multiple Possible Actions,
e.g.:
State: Robot sees a wall,
Policy: Turn Right → 70%,
Turn Left → 20%,
Move Back → 10%,

This means the robot usually turns right, but sometimes it may choose another action.

So the decision is random but controlled by probabilities.
# Value:
A value tells the agent how good or useful a state is.

It represents the amount of future reward the agent expects to get from that state.

In simple words:

State -> How good is this position?
**Example**

Suppose a robot wants to reach a goal.

S → A → B → G

The robot learns these values:

State S = 20

State A = 50

State B = 90

Goal G = 100

Higher value means a better state because it is closer to getting higher rewards.

If the robot is at State A and has two choices:

Left  → Value 30

Right → Value 90

The robot chooses:

Right

because higher value means better expected future reward.

# Discounted reward: 
Discounted reward means future rewards are given less importance than immediate rewards.

Example:

S → A → B → Goal

Rewards:

S → A = -1
A → B = -1
B → Goal = +100

Discount factor:

γ = 0.9
Future rewards after S are:

-1 , -1 , +100

Discounted return formula:


$-1 + 0.9(-1) + 0.9^2(100)$

Now add all:

-1 -0.9 +81
=79.1

So:

Value(S) ≈ 79.1

# Why do we discount?

Imagine two paths.

Path A
Immediately

+50
Path B
0
0
0
+60

Without discounting

Path A = 50

Path B = 60

The robot would choose Path B.

With discounting (γ=0.9):

Path A

50

Path B

0

0

0

0.9³ × 60

= 43.7

Now

50 > 43.7

So the robot prefers getting a good reward sooner rather than waiting a long time for a slightly larger reward.

