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
    
### Why is this more efficient? 

Suppose the agent experienced: 

    (2, Right, +1, 3)

It is a very useful experience because reaching state 3 gives a reward.

Without replay:

    Experience
        ↓
    Learn once
        ↓
    Throw away ❌ 

With replay: 

    Experience
        ↓
    Store in memory
        ↓
    Learn
        ↓
    Keep it
        ↓
    Maybe sample it again
        ↓
    Learn again
        ↓
    Maybe sample it again
        ↓
    Learn again

So one experience can help train the network multiple times.

### second problem: catastrophic forgetting/interference 

Imagine the agent has learned: 

    State A → Action RIGHT 

So the neural network has learned:

    A → RIGHT is good 

Then the agent moves to another part of the environment and experiences lots of new things:

    B → LEFT
    C → RIGHT
    D → LEFT
    E → LEFT
    F → RIGHT
    ... 

If we continuously train only on these new experiences, the neural network's weights keep changing.

Eventually it might become:

A → RIGHT ❌ not as good as before.

The network has partially forgotten what it learned about A.

This is the basic idea of catastrophic forgetting/interference. 

### How does Replay Buffer help?

The buffer keeps both old and new experiences.

For example:

Replay Buffer

    OLD experiences
    ────────────────
    A → RIGHT
    B → LEFT
    C → RIGHT

    NEW experiences
    ────────────────
    D → LEFT
    E → RIGHT
    F → LEFT 

Now, instead of training only on: 

    D
    E
    F 
we randomly sample from everything:

    A
    D
    C
    F
    B 

So the neural network keeps seeing a mixture of:

    OLD + NEW experiences

Therefore it is less likely to completely forget the old ones.

#### What happens when the buffer becomes full?

if Capacity = 5 

Suppose we already have: 

    1
    2
    3
    4
    5 
Then a new experience 6 arrives.

The oldest experience is removed:

    Before:

    1  2  3  4  5

    New experience = 6

    After:

    2  3  4  5  6 

So the replay buffer usually works like a fixed-size memory.





  
