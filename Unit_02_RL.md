# ε (epsilon) Greedy: 


    For every action decision

    With probability ε, choose a random action (exploration).

    With probability 1 − ε, choose the action with the highest Q-value (exploitation).

  if ε = 0.8, then every time the agent needs to choose an action, it does:

Generate random number r

If r < 0.8:


    Explore
    
Else:

    Exploit

Suppose the random numbers generated are:

0.15 → Explore

0.91 → Exploit

0.42 → Explore

0.77 → Explore

0.95 → Exploit

0.31 → Explore

0.84 → Exploit

0.12 → Explore

0.65 → Explore

0.98 → Exploit

Out of these 10 actions:

Explore = 6
Exploit = 4

Even though ε = 0.8 (80%), we got only 60% exploration because 10 actions is a small sample.

If you repeat this for 10,000 actions, you'll likely get something like:

Explore = 7,984

Exploit = 2,016

which is very close to 80% and 20%.

So the important difference is:

Probability: "Each action has an 80% chance of exploration." ✅

Guarantee: "Exactly 80 out of 100 actions will be exploration." ❌

# Why Bellman Equation needed ?
To calculate Each value of a state or state-action pair , we need to sum all the rewards an agent can get if it starts at that state. 

this is Computationaly Expensive. 

a tiny example:

    Home ----> Shop ----> Treasure

Rewards:

    Home → Shop = +2

    Shop → Treasure = +10

 - Before Bellman Equation

       Value(Home) = Reward(Home→Shop) + Reward(Shop→Treasure) 

                = 2 + 10 = 12

If there were 100 more states after Treasure , agent would have to keep adding all of them. 

         Expensive for long paths. 
         Must look at the complete future. 

- Bellman Equation

Don't calculate the whole future at once. Break it into smaller pieces.

First calculate: 

     Value(Home) =  Reward(Home→Shop) + Value(Shop)
                 

Now calculate:

     Value(Shop) = Reward(Shop→Treasury) + Terminal / Treasure
                 

✅ Bellman update happens after every action (every step). 

✅ The updated Q-values are stored in the Q-table immediately.

✅ The next episode starts with this updated Q-table, so learning continues from where the previous episode left off. 

# Different forms of Bellman Equations: 

$$V(s) = R + \gamma V(s')$$

$$V(s) = R + \gamma \sum P(s' | s, a)V(s')$$

$$Q(s,a) = R + \gamma \max_{a'} Q(s',a')$$



- $$V(s) = R + \gamma V(s')$$ This assumes that after taking an action, there is only ONE next state.

Home -----> Shop -----> Treasure 

- Problem:

Real environments are rarely this simple.

Suppose now From Home, taking the same action can lead to

Shop (80%)

Park (20%)

Should we use

    V(Home)=R+γV(Shop) 

    or 

    V(Home)=R+γV(Park)

Neither!

Both can happen.

So we compute the expected (average) value.

That's why the equation becomes 
$$V(s) = R + \gamma \sum P(s' | s, a)V(s')$$

- But another problem appears

Even if you know

      V(Home)=50
      
you still don't know

which action to take.

Suppose

At Home

Action 1 → Walk

Action 2 → Bike

Action 3 → Stay

The value function only says

Home = 50

It doesn't tell you

Walk?

Bike?

Stay?

It evaluates states, not actions

So RL introduces Q-values

Instead of storing State ➡ Value , it stores (State, Action) ➡ Value
 
Example

| State | Action | Q-value |
|-------|--------|--------:|
| Home  | Walk   | 90      |
| Home  | Bike   | 70      |
| Home  | Stay   | 30      |

Now the best action is obvious.

Choose Walk

because 90 is maximum.

This gives $$Q(s,a) = R + \gamma \max_{a'} Q(s',a')$$





 
