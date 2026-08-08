# Q Learning with simple example

Imagine a robot moving on 5 positions:

        START                      GOAL

         0      1      2     3      4
         🤖    ⬜    ⬜    ⬜    🏆

The robot has two possible actions:

    Left
    Right 

Rewards:
    
    Reaching goal → +10

    Every normal move → -1 

At first we make a Q table :

Q-learning stores:

"How good is taking action A when I am in state S?"

Q table:

| State | Left | Right |
| ----- | ---: | ----: |
| 0     |    0 |     0 |
| 1     |    0 |     0 |
| 2     |    0 |     0 |
| 3     |    0 |     0 |
| 4     |    0 |     0 |

### Episode 1 

#### Robot starts at state 0 

Suppose it chooses:

    State = 0
    Action = Right

It moves to state 1.

    0 --Right--> 1

Reward: 

    R = -1

Now Q-learning updates: 

$$Q(s,a) \leftarrow Q(s,a) + \alpha[r + \gamma\max_{a'}Q(s',a') - Q(s,a)]$$

Suppose:

    α = 0.5
    γ = 0.9

Before update: 

    Q(0, Right) = 0 

Next state is 1

Currently: 

    Q(1, Left)  = 0
    Q(1, Right) = 0 

Therefore: 

    maxQ(1,a)=0

So: 

    Q(0,Right)=0+0.5[−1+0.9(0)−0] 

    Q(0,Right)=−0.5 

Our table becomes: 

| State | Left |    Right |
| ----- | ---: | -------: |
| 0     |    0 | **-0.5** |
| 1     |    0 |        0 |
| 2     |    0 |        0 |
| 3     |    0 |        0 |
| 4     |    0 |        0 |

What did it learn?

It learned:

"Going right from state 0 resulted in a cost of -1."

But it doesn't yet know that going right eventually leads to the goal.

#### Continue from state 1

The robot is now here: 

    0     1     2     3      4
         🤖                 🏆

Suppose it chooses Right again.

    1 --Right--> 2

Reward: - 1

Before update:

    Q(1,Right) = 0 

And currently: 

    Q(2,Left)  = 0
    Q(2,Right) = 0

Therefore: 

    Q(1,Right)=0+0.5[−1+0.9(0)−0]
    Q(1,Right)=−0.5

Now: 

| State | Left |    Right |
| ----- | ---: | -------: |
| 0     |    0 |     -0.5 |
| 1     |    0 | **-0.5** |
| 2     |    0 |        0 |
| 3     |    0 |        0 |
| 4     |    0 |        0 |

#### Continue 2 --Right--> 3

Again reward: - 1

So: 

   Q(2,Right) = -0.5 

#### Then: 

    3 --Right--> 4 

Now The robot reaches the goal.

    Reward = +10

Before the update: 

    Q(3,Right) = 0 

Since 4 is the terminal goal, we don't need future Q-value. 

So:

    Q(3,Right)=0+0.5[10−0] 
    Q(3,Right)=5 

Now: 

| State | Left | Right |
| ----- | ---: | ----: |
| 0     |    0 |  -0.5 |
| 1     |    0 |  -0.5 |
| 2     |    0 |  -0.5 |
| 3     |    0 | **5** |
| 4     |    0 |     0 |

The robot has finished its first episode.

But look at what happened: 3 → 4

gave: +10 

So Q-learning learned:

Right from 3 is VERY good.

But what about state 2?

It currently thinks: 

    Q(2,Right) = -0.5 

It doesn't yet understand that: 

    2 → 3 → 4

eventually gives a big reward.

That's where future Q-values come in.

### Episode 2

The robot starts again: 

    🤖
    0 → 1 → 2 → 3 → 🏆

Suppose it reaches:

2 --Right--> 3

Reward: - 1

Now look at the Q-values at state 3. 

We already learned: Q(3,Right) = 5

Therefore: maxQ(3,a)=5

Now update: 

    Q(2,Right)=−0.5+0.5[−1+0.9(5)−(−0.5)]

Result: 

    Q(2,Right)=1.7

🔥 Notice what happened.

Before:

    Q(2,Right) = -0.5 
    
After learning about the good future:

    Q(2,Right) = 1.7

Eventually the reward propagates backward

After many episodes, you'll get something roughly like:

| State | Left |         Right |
| ----- | ---: | ------------: |
| 0     |  bad |      **good** |
| 1     |  bad |      **good** |
| 2     |  bad |      **good** |
| 3     |  bad | **very good** |
| 4     |    — |             — |

Eventually the robot understands:

0
 ↓ Right
1
 ↓ Right
2
 ↓ Right
3
 ↓ Right
4
🏆

Every time action is chosen on basis of exploration formula like epsilon greedy


