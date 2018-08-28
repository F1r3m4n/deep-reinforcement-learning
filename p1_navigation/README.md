# Deep Reinforcement Learning - Navigation


## Project Details

The aim of this project is to train an agent to navigate and collect yellow bananas in a large, square world. The task is episodic, and in order to solve the environment, the agent must get an average score of +15 over 100 consecutive episodes.


#### State 

The state space has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around the agent's forward direction. Given this information, the agent has to learn how to best select actions. 


#### Actions

Four discrete actions are available, corresponding to:

* 0 - move forward.
* 1 - move backward.
* 2 - turn left.
* 3 - turn right.


#### Rewards

A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting a blue banana. Thus, the goal of the agent is to collect as many yellow bananas as possible while avoiding blue bananas in a given time frame.


#### Expected Behaviour

<img src="images/NavigationProject_Medium.gif" width="800" height="500" />



## Getting Started


#### Step 1: Clone the DRLND Repository

If you haven't already, please follow the instructions in the DRLND GitHub repository to set up your Python environment. These instructions can be found in README.md at the root of the repository. By following these instructions, you will install PyTorch, the ML-Agents toolkit, and a few more Python packages required to complete the project.



#### Step 2: Download the Unity Environment

For this project, you will not need to install Unity - this is because we have already built the environment for you, and you can download it from one of the links below. You need only select the environment that matches your operating system:

Linux: 
Mac OSX: 
Windows (64-bit): 

Place the file in the p1_navigation/ folder in the DRLND GitHub repository, and unzip (or decompress) the file.


## Instructions