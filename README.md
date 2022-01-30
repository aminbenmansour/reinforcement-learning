# reinforcement-learning

# Theory behind RL

How agent maximizes long-term rewards in an environment with uncertainties.

**Q-learning** is a powerful solution because it makes agent learns from thr environment in real time and quickly learn novel strategies from mastering the task at hand.


*   q-learning works by mapping **pairs of states and actions** to expected future rewards

  *   decides which action to take based on epsilon greedy action selection
      *   if random number > epsilon then apply a random action else take actions that lead to the highest known expected feature rewards
      *   storing values in a table of state action pairs
      *   update estimate of Q, not memory

When dealing with an environment which has a huge number of states or a state space which is continuous we can't use a tabl, in that case we use **deep Q-learning** to take interpretations of the environment and turn them into discrete outputs that corresponds to the values of each action.

Neural networks are universal function approximators, they can approximate any continuous function. In our case we are looking for the relation between states, actions and rewards that the agent wants to learn so he can maximiwes his future rewards.

Deep Q learning agents have a **memory of <S, A, R, S'>** they stands for the states they saw, the action they took and the rewards they receive.

During each subset step the agent samples a subset of this memory to feed this states through its neural network, thus the agent could compute the value of the action he took then his loss (Q(actual) - Q(maximal)) in order to update the weightd of the neural network.
