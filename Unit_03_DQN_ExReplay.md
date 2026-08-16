# EXPERIENCE REPLAY

## Instead of throwing experiences away, we create a Replay Buffer.

Think of it as a memory box. 

             REPLAY BUFFER
        ┌─────────────────────┐
        │                     │
        │  Experiences stored │
        │  here               │
        │                     │
        └─────────────────────┘
Every time the agent experiences something, we put it inside.

For example:

    (0, Right, 0, 1)
    (1, Right, 0, 2)
    (2, Right,+1, 3) 

So now:

    Replay Buffer

    ┌────────────────────────┐
    │ (0,R,0,1)              │
    │ (1,R,0,2)              │
    │ (2,R,+1,3)             │
    └────────────────────────┘ 

We don't immediately forget these experiences.

## What does the neural network do with them?

Suppose the buffer contains 6 experiences:
        
Replay Buffer

    1. (0, Right, 0, 1)
    2. (1, Right, 0, 2)
    3. (2, Right, +1, 3)
    4. (1, Left, 0, 0)
    5. (2, Left, 0, 1)
    6. (0, Right, 0, 1) 

Instead of always training on the latest experience, we randomly pick a small group.

Suppose: 

    Batch size = 3

We randomly select: 

    (1, Left, 0, 0)
    (2, Right, +1, 3)
    (0, Right, 0, 1) 

These 3 experiences are given to the neural network for training.

    Replay Buffer
         ↓
    randomly select
         ↓
    ┌──────────────────────┐
    │ (1,L,0,0)            │
    │ (2,R,+1,3)           │
    │ (0,R,0,1)            │
    └──────────────────────┘
         ↓
    Neural Network
         ↓
    Update weights 

  That's the core idea. 






  
