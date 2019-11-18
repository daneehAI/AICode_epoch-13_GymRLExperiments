# FruitPunch AI Code epoch 13: OpenAI Gym Reinforcement Learning Experiments
Some OpenAI Gym Reinforcement Learning experiments for FruitPunch AI's AI Code session of 19-11-2019.
The notebooks contain implementations of a few different algorithms, for the Acrobot-v1 environment of OpenAI gym.
This environment has a continuous observation space of 6 values. These are 3 pairs of x and y coordinates, one per joint of the Acrobot arm. The action space is discrete, consisting of 3 possible actions. These are left, right and none, and apply a force in that direction on one of the joints. I did not bother to find out which one, because this does not matter.

# The Notebooks
Each notebook contains a few variations of a specific algorithm. A list of all algorithms and all the implementations of each:

1. Q-learning with a Q table. 3 different Q-tables are implemented. All of these contain Q values for the 3 possible actions for each state, but the amount of states differs. These states are expressed in terms of comparisons of values from the observation. These 6 values are labeled [x1, y1, x2, y2, x3, y3].
   a. The first table only takes into account the relations of the coordinates in the current observation. This means this
      implementation does not know in what direction it is moving, but only its current position.
      
      s1: x1 <= x2 <= x3 && y1 <= y2 <= y3
      
      s2: x2 <= x1 <= x3 && y1 <= y2 <= y3
      
      etc, covering every possibility. Every possible order of 3 elements is 3! = 6 possible orders for both the x side and
      the y side. Combining each possibility from both sides makes the number of possible states 6^2 = 36, which makes for a
      Q table of 108 elements.
   b. The second table contains only the relations of each value to its previous value. This means this implementation does
      not take into account the relations between the joints, but only the movement of each joint.
      
      s1: x1 <= x1' && x2 <= x2' && x3 <= x3' && y1 <= y1' && y2 <= y2' && y3 <= y3'
      
      s2: x1 > x1' && x2 <= x2' && x3 <= x3' && y1 <= y1' && y2 <= y2' && y3 <= y3'
      
      etc, again covering every possibility. Since every state contains 6 comparisons that can either be <= or >, the amount
      of states comes to 2^6 = 64, and the size of the Q-table comes to 192 elements.
   c. The third table contains a combination of the information contained in the previous two implementations. This means the
      table contains 36 * 192 = 6912 states, and 6912 * 3 = 20736 elements. I am only going to write out 1 example state from
      this table:
      
      s1: x1 <= x2 <= x3 && y1 <= y2 <= y3 && x1 <= x1' && x2 <= x2' && x3 <= x3' && y1 <= y1' && y2 <= y2' && y3 <= y3'
      
      Yeah, you get the idea. This means this implementation knows where its joints currently are, as well as the direction
      they moved in since the last step.

Results:

2. Deep Q Learning. This is Q-learning, but with a neural network instead of a Q-table. This neural network is then called a Deep Q Network. I also have three implementations of this technology, the first two of which I implemented using the paper "Deep Q-Learning with Recurrent Neural Networks" by Clare Chen, Vincent Ying and Dillon Laird of Stanford University.
   a. The first implementation is regular Deep Q-Learning, using regular dense layers. This means that the agent acts only on 
   its current state.
   b. The second implementation is Deep Recurrent Q-Learning
   c. The third implementation is a combination of the second
   
Results:

3. Random Forest/Evolutionary AI. This is a fairly simple AI technology. The forest is a collection of trees. These trees are decision trees. Each tree has a root node. That's where the decision making starts. This root node has 2 branches that each have another node with another 2 branches etc, etc. At each node a boolean expression is checked, and if it is True, you continue along the first branch, and if it's false, you continue along the second. The tree continues until all possibilities are covered, or until a certain specified depth is reached, and then an action is chosen. Check out the AI Code session on Random Forests by Alican Noyan for more info on that topic (https://github.com/fruitpunch-ai-code/epoch-5). Besides that, each of the again 3 implementations is unique.
   a. The first implementation is a basic random forest. 
   b. 




Questions and challenges:
(Note: I do not have answers to all of these questions. Many questions are pretty subjective or complicated. I recommend researching these questions for yourself using the web, books and papers.)
1. Q-Learning:
   a. How would you change the content of the Q-table to increase both the efficiency and the skill of the agent?
   b. In which kinds of environments does regular Q-learning perform best? You should change the notebook to try out different
   gym environments with different observation and action spaces!
2. Deep Q-Learning
   a. What advantages does Deep Q-learning have to offer over regular Q-learning? And what are its disadvantages?
   b. Try modifying one of the Deep Q Networks. Read all about the layers, activations, optimizers and losses that keras has to
   offer, and try out the ones you think can improve the DQN.
   c. Try training one of the DQN's on some different environments at the same time. If you modify and refine the DQN enough,
   you might end up with a gym AGI!
3. Random Forest (Besides the web, books and papers, you should definitely use Alican's AI Code session to find answers to these questions, https://github.com/fruitpunch-ai-code/epoch-5)
   a. How do these 3 random forest implementations compare to the Q- and Deep Q-Learning? For which types of environments is the
   random forest suitable?
   b. Try defining a decision tree to solve the Acrobot environment yourself! Can natural intelligence beat all of the AI
   technologies in this repository?
   c. Try solving 2 different environments with the same random forest! You can use the same code and train the algorithm on
   each environment separately. Maybe you can even train one random forest on both environments, if you figure out how to handle
   all of the inputs and outputs?
