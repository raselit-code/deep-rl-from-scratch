# Deep Q Network  

In normal Q-Learning, we directly store Q-values in a table: 

    State → Action → Q-value

Example:

State = (0,0)

   Q-value:
   
↑              2.1

↓              0.5

←              1.2

→              3.7

DQN uses a neural network instead of the Q-table.

State

  ↓
  
Neural Network

  ↓
  
Q-values for all actions



suppose 4 x 4 Grid 

Our 4×4 grid has two values to represent the state:

- `x` = row
- `y` = column

So the neural network receives **2 inputs** and produces **4 outputs**, one for each possible action.

                 NEURAL NETWORK

     INPUT              HIDDEN              OUTPUT
   (2 neurons)        (some neurons)       (4 neurons)

      x ────────┐       ○ ───────────────→ Q(UP)
               ├──────→ ○ ───────────────→ Q(DOWN)
      y ────────┤       ○ ───────────────→ Q(LEFT)
               └──────→ ○ ───────────────→ Q(RIGHT)


     State                 Network              Q-values
    [x, y]                   ↓                    ↓
      │                 ┌─────────┐
      └────────────────→│   NN    │────────→ [Q1, Q2, Q3, Q4]  
                        └─────────┘
    

The 4 outputs represent:

- Output 1 → UP
- Output 2 → DOWN
- Output 3 → LEFT
- Output 4 → RIGHT

### What actually happens?

Suppose the agent is here: 

    (1,2) 

We convert it to: 

    [1,2] 

Then: 

     [1,2]
     
       ↓
  
    Neural Network
    
       ↓
  
    [2.1, 0.7, 1.3, 3.5] 

The output means: 

    UP     = 2.1
    DOWN   = 0.7
    LEFT   = 1.3
    RIGHT  = 3.5 

Now the DQN learning step

Suppose: 

    Current state = (0,0)
    Action = RIGHT
    Reward = 0
    Next state = (0,1) 

The network currently predicts: 

    Q((0,0), RIGHT) = 0.8 

Now look at the next state: 

    (0,1) 

Suppose the network predicts: 

    UP    = 0.2
    DOWN  = 0.4
    LEFT  = 0.1
    RIGHT = 0.9 

The maximum is: 

    max Q = 0.9 

Suppose: 

    γ = 0.9

Then: 

    Q-target = reward + γ × max Q(next state)

         = 0 + 0.9 × 0.9

         = 0.81

So: 

    Prediction = 0.8
    Target     = 0.81 

The network is pretty close.

We calculate the loss: 

    Loss = (0.81 - 0.8)²
    = 0.0001 
Then: 
          
    Loss
      ↓
    Gradient Descent
      ↓
    Change network weights
      ↓
    Network becomes slightly better

### The final Goal of DQN is : to learn a set of neural-network weights such that (a generalized NN works for all kind of state) :

    Any possible state
      ↓
    Neural Network
      ↓
     Q-values for
    all possible actions
    
