# DQN training 

## Deep Q-Learning training might suffer from instability 

Suppose the agent is at State A and takes an action.

The neural network initially says: 

    Q(A, Right) = 5 

Now DQN wants to improve this value. 

To calculate the new target, it looks at the next state B and asks the same neural network: 

    Q(B, best action) = 8

So it creates a target using that 8.

The network learns and its weights change.

After the update, it might now say: 

    Q(B, best action) = 12 

So the next time it calculates a target, it uses 12 instead of 8. 

Then after another update: 

    Q(B, best action) = 15

So the target keeps changing: 

    8 → 12 → 15 → ...
    
The problem is: The network is using its own changing predictions to create the targets it is learning from.

To help us stabilize the training, we implement three different solutions:

1. Experience Replay to make more efficient use of experiences.

2. Fixed Q-Target to stabilize the training.

3. Double Deep Q-Learning, to handle the problem of the overestimation of Q-values.

## Without Experience Replay 

    [ A ] → [ B ] → [ C ] → [ Goal ] 

The agent starts at A and wants to reach the Goal.

Suppose the agent experiences: 

Step 1

Agent is at A.

It chooses:

    Action = Right ; Reward = 0
 
Moves to B. 

So experience is: 

    (A, Right, 0, B) 

The neural network trains on this experience. 

Step 2

Now agent is at B.

It chooses: 

    Action = Right ; Reward = 0 

Moves to C.

    Experience: (B, Right, 0, C) 

The neural network trains on this. 

 Step 3

Agent is at C.

It chooses:     

    Action = Right ; Reward = +10 

Moves to Goal.

Experience: 

    (C, Right, +10, Goal)

The neural network trains on this. 

The problem : 

Without Experience Replay, training happens like this:

    Experience 1
     ↓
    Train NN
     ↓
    Experience 2
     ↓
    Train NN
     ↓
    Experience 3
     ↓
    Train NN 

After training on Experience 3, the network's weights have been changed according to the most recent experience.

And Experience 1 is gone.

So the network doesn't get to repeatedly learn: 

    A → B
    B → C
    C → Goal 

It just sees each experience once, in sequence.

The bigger problem

The experiences are also very similar: 

    (A, Right, 0, B)
    (B, Right, 0, C)
    (C, Right, 10, Goal) 

They came one after another and are therefore correlated. 
