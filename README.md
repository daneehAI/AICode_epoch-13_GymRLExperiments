# FruitPunch AI Code epoch 13: OpenAI Gym Reinforcement Learning Experiments
Some OpenAI Gym Reinforcement Learning experiments for FruitPunch AI's AI Code session of 19-11-2019.
The notebooks contain implementations of a few different algorithms, for the Acrobot-v1 environment of OpenAI gym.
This environment has a continuous observation space of 6 values. These are 3 pairs of x and y coordinates, one per joint of the Acrobot arm. The action space is discrete, consisting of 3 possible actions. These are left, right and none, and apply a force in that direction on one of the joints. I did not bother to find out which one, because this does not matter.

# The Notebooks
Each notebook contains a few variations of a specific algorithm. A list of all algorithms and all the implementations of each:
1. Q Learning with a Q table. 3 different Q Tables are implemented. All of these contain Q values for the 3 possible actions for each state, but the amount of states differs. These states are expressed in terms of comparisons of values from the observation. These 6 values are labeled [x1, y1, x2, y2, x3, y3]
   a. 
