# MONTE CARLO

## Problem : A robot wants to reach the Goal.

    A → B → C → Goal

Rewards:

    Moving to another state = 0
    Reaching Goal = +10

Learning rate:

      α = 0.5

Initially,

    V(A)=0
    V(B)=0
    V(C)=0

Monte Carlo does NOT update while moving. It waits until the episode ends.

Monte Carlo Update Equation :  $V(S)=V(S)+α(G−V(S))$

### Episode 1
Robot moves: A → B → C → Goal

While moving... Visited states: A B C

No updates yet. Current values are still 

    V(A)=0
    V(B)=0
    V(C)=0 
Episode Ends, Now Goal is reached, Now calculate returns backwards.

Goal reward = + 10 , Return From C G(C) = 10 , Return From B G(B) = 10 , Return From A G(A) = 10 

Now Update

    V(C)=0+0.5(10−0) = 5 
    V(B)=0+0.5(10−0) = 5
    V(A)=0+0.5(10−0) = 5
#### After Episode 1

| State | Value |
| ----- | ----: |
| A     | 5     |
| B     | 5     |
| C     | 5     |

### Episode 2

This time the robot takes a different path. A → D → Goal 

Rewards

    A→0
    D→0
    Goal→6

Current values before learning

    V(A)=5
    V(B)=5
    V(C)=5
    V(D)=0
Robot reaches Goal. Only now does Monte Carlo learn.

Returns G(D)=6 , G(A)=6

Update 

    V(D)=0+0.5(6−0) = 3
    Old V(A)=5 New =5+0.5(6−5) = 5.5

B and C were not visited, so they are not updated.

#### After Episode 2

| State | Value |
| ----- | ----: |
| A     |   5.5 |
| B     |     5 |
| C     |     5 |
| D     |     3 |

### Episode 3

Robot goes A → B → E → Goal 

Goal reward = + 12

Episode finishes.

Returns G(E) = 12 , G(B) = 12 , G(B) = 12

Update 
             
    V(E) = 0+0.5(12−0) = 6
    V(A) = 5.5+0.5(12−5.5) = 8.75
    V(B) = 5+0.5(12−5) = 8.5 
#### After Episode 3
| State | Value |
| ----- | ----: |
| A     |  8.75 |
| B     |   8.5 |
| C     |     5 |
| D     |     3 |
| E     |     6 |

##### Monte Carlo only updates states that actually appeared in that episode.

In the example above, assumed γ (discount factor) = 1, so every state received the same return as the final reward.

In practice, Monte Carlo usually uses: 

$$
G_t = R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3}
$$
     
#### 📌First-Visit Monte Carlo : One update per state per episode.
- Update a state only the first time it is visited in an episode.
- At the start of every new episode, the "visited" list is reset.

Episode: A → B → A → Goal

Updates: 

✓ Update A (first visit)

✓ Update B

✗ Ignore second A

Next Episode

A → C → Goal

Updates: 

✓ Update A again

✓ Update C

#### 📌Every-Visit Monte Carlo: Every occurrence of a state is updated.

Episode: A → B → A → Goal

Updates: 

✓ Update A (first visit)

✓ Update B

✓ Update A (second visit)

# TEMPORAL DIFFERENCE LEARNING : Learn step-by-step while moving.

TD Update Equation : $V(S)=V(S)+α(R+γV(S')−V(S))$                                                            

Suppose : A → B → C → Goal

Rewards:

    A → B = 0
    B → C = 0 
    C → Goal = +10

Initially:

    V(A)=0

    V(B)=0

    V(C)=0 
    
Take α = 0.5 , γ = 1

### Episode 1:

Robot moves : A → B  , Reward = 0

Update    
          
    V(A) = 0+0.5(0+1×0−0) = 0 

Move B → C , Reward = 0 

Update 

    V(B) = 0+0.5(0+1×0−0) = 0


Move C → Goal , Reward = +10

Update

    V(C) = 0+0.5(10+0−0) = 5  
    
##### After Episode 1

| State | Value |
| ----- | ----: |
| A     |     0 |
| B     |     0 |
| C     |     5 |

### Episode 2 

A → B → C → Goal , V(C)=5 

A → B , Reward=0 , V(B)=0 

    V(A) = 0+0.5(0+0−0) = 0 

B → C , V(C)=5 

    V(B) = 0+0.5(0+5−0) = 2.5

C → Goal , Reward = +10 , 

    V(C) = 5+0.5(10−5) = 7.5

#### After Episode 2

| State | Value |
| ----- | ----: |
| A     |     0 |
| B     |   2.5 |
| C     |   7.5 |

#### And similarly Episode Continues....



 

 




 












 







