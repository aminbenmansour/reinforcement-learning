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

# Implementation
In practice we have to deep neural networks


*   **Q(evaluation):** used to evaluate the cirrent state and decide which action to take.
*   **Q(target):** calculates the value of maximal action during the learning step.

We mainly use two networks so we can **reduce the bias**

The weights of the target networks are periodically updated with the weights of the evaluation network. so the estimates of the maximal actions could get more accurate overtime.


When dealing with an environment that uses pixel images we need to use the **Convolutional Neural Network (CNN)** to process images and perform feature extraction from the input.

The Output of the CNN is then **flattened** and then fed through **dense layers** to calculate action values.

If the environment have movement (and mostly will do), we will have additional problems to solve!


In this image even a human doesn not have a sense of motion to tell which direction the ball or the panel is moving.
![Screenshot_20220130_221257](https://user-images.githubusercontent.com/50111205/151719871-7fa614b3-db24-49e8-9e12-ee420e772afb.png)


So we need a way of stacking frames to give the agent a sense of motion. In other words our CNN will take a batch of stacked images as input rather than a single image.

Choosing an action is reasonably straightforward, generate a random number and then follows the simple condition.
*   if **rand < epsilon** then take a **random action**
*   if **rand > epsilon** then take a **greedy action** by feeding our set of stack frames through the evaluation network to get the values of all the actions in the current state. find the maximal action and take it. Once you get the new state back from the environment add it to the end of the stack frames and **finally store the stack frames, actions and rewards to the agent's memory**

Perform the learning operations by sampling the agent's memory. It is really important to get a non sequential random sampling of the memory so we avoid getting trapped in one little corner of parameter space.

As long as we keep track of the state transitions, action and rewards in the same way we should be pretty safe.


Feed the random batch of data to the evaluation and target networks, compute the loss function to perform your loss minimization step for the neural network.


In order to summarize, this what deep Q learning needs:


*   A couple of neural networks.
*   A memory to keep track of states.
*   Lots of GPU horsepower to handle the training.

# Frameworks

We should preferably use a framework that lets you use a GPU for the training. Both **tensorflow** and **pytorch** are great choices. and support [model checkpointing](https://www.analyticsvidhya.com/blog/2021/03/improving-your-deep-learning-model-using-model-checkpointing-implementation-part-2/) and we will take advantage of both of them in this repository.
