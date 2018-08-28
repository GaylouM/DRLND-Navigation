# Navigation Bananas
1.0 8/28/2018

INTRO
-----------

Navigation is an agent built to navigate through bananas trying to avoid blue bananas and to catch yellow ones.
This agent must maximize its reward and earns 1 when it grabs yellow bananas and loses 1 when it catch blue bananas.
The algorithm using the simple Deep-Q learning algorithm. This algorithms is made of two interleaved processes. One is where we sample the environment by performing actions and we store experience tuple (S, A, R, S') in replay memory D and one who learns from that batch using gradient descent update step

1. First player create a game in createTwoplayersGame endpoint
2. Second Player get the webSafeGameKey in getGamesCreated endpoint
3. Second Player register with the webSafeGameKey in registerForGame endpoint,
an active player is randomly picked
4. The active player must guess a row and column on the board to find a boat in
guess endpoint
5. If a boat is hit the player continue else active player changes.
6. The game continues until one of the two players get rid of all the adversary ship

## DESCRIPTION STEP BY STEP

![image0](https://github.com/GaylouM/DRLND-Navigation/tree/master/misc/image0.JPG)

Our code is running in a loop with a finite number of episode which is limited by the n_episodes parameter

![image1](https://github.com/GaylouM/DRLND-Navigation/tree/master/misc/image1.JPG)

We start by resetting the environment with the 'env.reset' method setting train_mode to True to accelerate the training.
Then we are getting the first state with the env_info.vector_observations method

![image2](https://github.com/GaylouM/DRLND-Navigation/tree/master/misc/image2.JPG)

We are then entering the timestep loop which is constrained by both the maximum number of timestep per episode parameter max_t and the possible end of the episode.

![image3](https://github.com/GaylouM/DRLND-Navigation/tree/master/misc/image3.JPG)

We are calling the agent.act method which take as parameters the current state and epsilon and returns an action inferencing the Torch model.

![image4](https://github.com/GaylouM/DRLND-Navigation/tree/master/misc/image4.JPG)

This action is used as parameter to take a step forward in the environment by passing it to the step method of the environment object, and return a set of new observation

![image5](https://github.com/GaylouM/DRLND-Navigation/tree/master/misc/image5.JPG)

from those we are extracting the next state 'env_info.vector_observations[0]' and reward 'env_info.rewards[0]' and status of the environment.

Eventually the step method of agent is called which take as parameters state, action, reward, next_state and done, save experience in replay memory and call the learn method of the agent passing experience and gamma as parameters. The learn agent is computing the loss and is passing qnetwork_local and qnetwork_local as parameters to the soft_update method which in return update the model.

Then the loop is running for an other timestep until it reaches the conditions to break and start a new episode again.

![image6](https://github.com/GaylouM/DRLND-Navigation/tree/master/misc/image6.JPG)
