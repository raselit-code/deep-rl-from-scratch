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






 







