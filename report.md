### Learning Algorithm

In this project, I have used DDPG algorithm to train the agent.
- Basically, this algorithm follows Actor-Critic model thus I created total of 4 networks: actor and critic networks, both with different target networks too.
- During the training phase, traget network of actor is used to obtain the targeted Q-values for critic while local critic network is used to get expected Q-values.
- Then, critic loss is calculated using MSE loss fuction.
- After that, backpropagation and optimization steps are performed for the critic network.
- As for the actor network, we used the critic network, which is essentially an action-value network, to find the loss for actor network.
- Once loss is calculated, backpropagation(via gradient ascent) and optimization steps are performed for the actor network as well.
- And finally, traget networks'(of both actor and critic) model parameters are changed using soft update method.
- Experience tuples necessary for training these networks are obtained from Replay memory in which newly generated experience tuple is added during the training episodes.

### Hyperparameters

Following hyperparameters are used in the project:
* BUFFER_SIZE = int(1e5) : replay buffer size
* BATCH_SIZE = 64 : minibatch size
* GAMMA = 0.99 : discount factor
* TAU = 1e-3 : for soft update of target parameters
* LR_ACTOR = 1e-4 : learning rate of the actor 
* LR_CRITIC = 1e-3 : learning rate of the critic
* WEIGHT_DECAY = 0 : L2 weight decay
* EPSILON = 1.0 : epsilon for the noise process added to the actions
* EPSILON_DECAY = 1e-6 : decay for epsilon above
* UPDATE_EVERY = 20 : how often to update the network
* UPDATE_TIMES = 10 : how many times to update the network each time

### Network Architecture

3 Fully connected linear layers are used in both local and target networks of both actor and critic. Relu activation fuctions are used in the outputs of input and hidden layers. Batch normalization is also performed to the output of first input layer before it is passed through relu fuction. Final output of actor networks is also passed through tahn activation function as we need the output to be in range of -1 and 1.
As for actor networks, first input layer is of size 33 x 64. Likewise hidden layer is of size 64 x 64 and finally output layer is of size 64 x 4. Here 33 is the number of states and 4 is number of actions. 
As for critic networks, first input layer is of size 33 x 64. Likewise hidden layer is of size 68 x 64 and finally output layer is of size 64 x 1. Here 33 is the number of states and 4 is number of actions. We have 68 as size of hidden layer as the output of first input layer is concatinated with the action values (which is of size 4).

### Plot of Rewards

#### Training Phase

Environment solved in 210 episodes with	average Score of 35.127.

![Scores during training](https://raw.githubusercontent.com/SRatna/DeepRL-Reacher/master/plots/train.png)

#### Training Phase

The average score over 100 epsoides is 36.72 during testing phase.

![Scores during testing](https://raw.githubusercontent.com/SRatna/DeepRL-Reacher/master/plots/test.png)

### Future Work

Some of advanced algorithms can be used to obtain great performance. A few of them are:

* PPO: proximal Policy Optimization algorithm
* A2C: Advatage Actor Critic algorithm
* GAE: Generalized Advantage Estimation algorithm

Moreover, hyperparemeters like buffer size, learning rate and discouting rate can be changed and we can hope more improvement through it. Also, the depth of neural networks can be increase although it might increase the training time. We can also try different optimizers and see its effect in the overall performance of the agent. 

Ofcourse trying out more complex environment like Crawler would be a part of future work too.