Initially, I took the professor's suggestion and I tried to train a simple neural network to learn how to play Connect 4. The idea was to use adversarial search agents playing against one another to generate the initial training data. I ran 1000 games (which surpisingly took quite a while as I hadn't made my code more efficient) with the agent playing against itself, and used this data to train the network.

(Done in file "connect4-nn.ipynb"
The neural network I used was built with PyTorch. It's a feed-forward network with four layers. It takes the state of the Connect 4 board as input, which is a 64-dimensional vector (8x8 board), and outputs an 8-dimensional vector, each element representing a column move.

I trained the model for 50 epochs, using batches of 32 examples from the game data. The model used the cross-entropy loss function to measure prediction errors and the Adam optimization algorithm to minimize these errors.

However, when I tested the trained model, it didn't perform as well as I'd hoped against the adversarial search. It was a bit disappointing, but it got me thinking about what I could do differently. I honestly didn't even attempt to keep trying with this approach, as I read more about better methods here:

https://codebox.net/pages/connect4

(Training done in "trying-deep-reinforcement.ipynb, and to see me play it check out "testing-deep-reinforcement.ipynb"
So, I decided to explore deep reinforcement learning, which is another approach to train AI models (except using adversarial search not the Monte Carlo search mentioned in the article). I set up a model to play 15000 games against an adversarial player. This model used a similar architecture to the first one but was trained using the REINFORCE algorithm which is a policy gradient method. This meant the model was updated after each game, based on the history of its moves, board states, and rewards. The reward function simply used the score of the board as reward which, as we all know, was given by the minMax algorithm from homework 4.

Sadly, even after implementing deep reinforcement learning, the model's performance didn't improve significantly. It didn't manage to consistently beat the adversarial search, which showed that the current approach wasn't working as expected. I ran it a few times with tweaks to the minMax algorithm and reward functions to no avail. I made sure that the games were printed so that I could see if there was any progress being made, and I noticed that in larger, longer games with so many different patterns of length 2 and length 3 with potential wins that the score almost got confused. I feel as though to move forward I need a more reliable minMax algorithm. Something that fully understands the consequences of not defending here or placing here if I am guranteed a win even after the next move. For some reason, even though adversarial search should look a few moves into the future and know these things, with larger games it just stopped blocking certain things and going on the attack. 

Going forward, there's a lot of room for improvement and further research. For one, I might try a more complex network architecture, maybe including convolutional layers to better process the spatial relationships on the board. I could also experiment with other reinforcement learning algorithms like Q-learning or actor-critic methods, which might be more efficient or stable.

Plus, I could look into using different training setups. Maybe pre-training the model on human-played games could teach it a wider range of strategies. Finally, evaluating the model's performance more comprehensively, like setting it up against other AI or human players, could also provide better insight into how well it's really learning the game.

Also, I definitely should have done this earlier, but I found a dataset with a bunch of human-played Connect4 games! Although the game is played on a different board, that might be a good next step. 

So, despite the setbacks, I learned a ton from this project. It's pretty clear that I've got more work to do, but I'm excited to see where it goes as I work on it some more over the summer.
