# How Actions (random or greedy ) are selected in DQN ? Experience Replay ?
## In Deep Q-Learning with experience replay, there is no Q-table. Instead, the Neural Network acts as the Q-function.

When epsilon-greedy decides to choose the greedy action: 

    1. Take the current state S
    2. Input S into the neural network.
    3. The NN outputs estimated Q-values for all actions:
    4. Choose the action with the highest output Q-value 
       
   $$
   a = \arg\max_a Q(s,a)
   $$

     Every time epsilon-greedy chooses the greedy option, the current state is fed into the neural network, 
     and the action with the highest predicted Q-value is selected.

  #### Very simply 

  Random case: 
         
    With probability ϵ→choose random action

  Greedy case:

    With probability 1−ϵ
    Current State → Neural Network → [Q1,Q2,Q3,Q4]

  Choose:

    action corresponding to maximum Q-value
	​
### In very beginning, the NN weights are random, so its predicted Q-values are also basically meaningless/random.

Suppose:

    s → NN → [2.1,−0.7,0.3,1.5] 

These Q-values are coming from randomly initialized weights, not from learning. 

If epsilon-greedy says greedy, it will still choose the highest:

    max=2.1 → action

Even though action is not actually known to be good yet. It just happens to have the highest random output.

### What happens in the first episode?

At the start:

    NN weights → random
    Replay buffer → empty
    Q-value predictions → random/untrained

At each step:

    1 Current state goes into NN.
    2. Epsilon-greedy decides:

       * with probability ϵ → random action
       * with probability ϵ → feed state into NN and choose action with highest currently predicted Q-value. 

    3. Agent performs the action.
    4. It gets:   (s,a,r,s',done)
    5. This experience is stored in the replay buffer.
Initially, there may be not enough experiences to train. So the agent keeps collecting experiences.

For example: 

    Start:
    Replay Buffer = [ ]

    Step 1:
    experience → store
    Buffer = [E1]

    Step 2:
    experience → store
    Buffer = [E1, E2]

    Step 3:
    experience → store
    Buffer = [E1, E2, E3]

    ... 
Once the buffer has enough experiences for a minibatch, for example batch size = 32:

    Buffer size ≥ 32

then training can start by randomly sampling experiences from the buffer.
