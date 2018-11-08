# Continuous Control - Report


The aim of this project is to train an agent to manipulate a double-jointed robotic arm so that it can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of the agent is to maintain its position at the target location for as many time steps as possible. The task is episodic (fixed number of timesteps), and in order to solve the environment, the agent must get an average score of +30 over 100 consecutive episodes.



## Learning Algorithms

The algorithm of choice to solve the environment was Deep Deterministic Policy Gradients (DDPG, Lillicrap et al. (2015)).
DDPG is an off-policy actor-critic algorithm, applicable to continuous action spaces. 



### Overview of learning algorithms and network architecture

Below is a short summary of the components and neural network architectures used as part of the DDPG algorithm and what the learning process is.


#### Actor Network 

The Actor takes the State as input and outputs the what the agent believes to be the best action (here a set of continues values of the torque for each joint) to maximise long term reward.

<img align=center src="images/actor.png" width="300" height="250" />

Two separate networks with identical architectures of the Actor are instansiated; one local and one target. The target network's weights are updated less often than the local network. Without fixed targets, we would encounter a harmful form of correlation, whereby we shift the parameters of the network based on a constantly moving target.

#### Critic Network

<img align=center src="images/critic.png" width="300" height="250" />

The Deep Q-Learning algorithm represents the optimal action-value function as a neural network instead of a table. The DQN takes the state as input and returns the predicted action values for each possible action.

For the reasons stated above, two separate networks with identical architectures of the Critic are instansiated (local and target).


#### Experience Replay


When the agent interacts with the environment, the sequence of experience tuples can be highly correlated. The naive learning algorithm that learns from each of these experience tuples in sequential order runs the risk of getting swayed by the effects of this correlation. By instead keeping track of a replay buffer and using experience replay to sample from the buffer at random, we can prevent action values from oscillating or diverging catastrophically.


#### OU Noise

In this implememntation the DDPG algorithm uses a correlated stochastic policy of the form:
w ∼ OU(0, σ2)

The exploration is realized through action space noise only. Note that training without noise was also found to have good performance, possibly due to the well defined reward function.


#### Learning Process - DDPG algorithm

The learning process can be broken into 3 steps:

* Update of the local Critic network
* Update of the local Actor network
* Update of both Actor and Critic target networks 

<img align=center src="images/ddpg.png" width="600" />

**Updating the Critic**

Similar to DQN, the critic estimates the Q-value function using off-policy
data and the recursive Bellman equation:
Q(st, at) = r(st, at) + γQ (st+1, πθ(st+1)),
where πθ is the actor or policy. 

**Updating the Critic**

The actor is trained to maximize the critic’s estimated Q-values by
back-propagating through both networks. 

**Updating target networks**






### Chosen Hyperparameters

The following hyperparameters were chosen following a trial and error approach

* Replay buffer size: 300000
* Minibatch size for training: 256
* Discount factor: 0.99
* Interpolation parameter for soft update of target parameters: 0.0009
* Optimizer: Adam
* Learning rate (Actor): 0.0001
* Learning rate (Critic): 0.0005
* Steps between netwok update: 2 updates every 4 timesteps


## Plot of Rewards

The following plots of the rewards per episode illustrate that the agent is able to receive an average reward (over 100 episodes) of at least +15. The table also shows how many episodes were needed to solve the environment.

<table style="width:500%" border=1>
  <tr>
    <th align=center>Agent: DDPG, Solved in: 91 episodes</th>
  </tr>
  <tr>
    <td align=center><img src="images/scores.png" width="400" height="300" /></td>
  </tr>
</table>


## Ideas for Future Work

One key improvement to make would be to use a prioritised replay buffer. It has been shown that experience replay allows online reinforcement learning agents to reuse experiences that are not sequencial and from different times. The algorithm used here uniformly samples experience transitions from a replay memory. Although this approach is effective, it only replays transitions at the same frequency that they were originally experienced, regardless of their significance. As shown in this [paper](https://arxiv.org/abs/1511.05952 "arXiv:1511.05952") prioritising experience, so as to replay important transitions more frequently, leads to more efficient learning. 

