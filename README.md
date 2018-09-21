# Self-learning tic-tac-toe game agent 

This is an unbeatable self-learning Tic-Tac-Toe AI game written in python based on **MENACE** (*for Matchbox Educable Naughts and Crosses Engine*) proposed by  Donald Michie in 1961 and 1963. Follwoing is an exerpt about MENACE from the book "Reinforcement Leaning an Introduction" by Sutton and Barto:

*"MENACE consisted of a matchbox for each possible game position, each matchbox containing a number of colored beads, a different color for each possible move from that position. By drawing a bead at random from the matchbox corresponding to the current game position, one could determine MENACE’s move. When a game was over, beads were added to or removed from the boxes used during play to reinforce or punish MENACE’s decisions."*

Here is a detailed blog post about it: [How to train matchboxes to play human level tic-tac-toe](https://riturajkaushik.github.io/2018/09/19/self-learning-tictactoe.html)

The AI agent in this program learns to play tic-tac-toe from thousands of games *played by it with itself*.

Basic steps:

1. First generate all the possible states of the game and possible moves for each of the states. This step generates a huge number of states (more than 300000 states)
2. Since tic-tac-toe game board is symmetric, so many of the states are actually similar states if rotated or taken mirror image of the board. So we remove all the duplicate states that we generated. After this we are left with only around 900 states.
3. Now, the AI agent start playing games (initially with random moves and then with different strategies) with itself. After every game, it updates all the moves corresponding to the visited states as follows:
    * If it wins the game then it adds the corresponding move in the possible moves for that states. This increases the possibility of selecting that move again if we uniformly sample the moves for that state. Shorter the games more will be the addition of the moves. Also, closer the the step to the winning step of the game more will be the adding of the winning moves to the state.
    * If it loses the game, it deletes the corresponding moves that it has played from the states. Shorter the games more will be the deleting of the moves. Also, closer the the step to the winning step of the game more will be the deletion of the winning moves to the state.
4. Now, after thousands of self games, the states have more of the winning moves than the losing moves.
5. The system saves all the states and corresponding moves in a *experience.dat* file

Before playing with human player, the system reads the *experience.dat* file and loads the staes and corresponding moves. Now for every state in the game, the agent plays the maximum occurring moves for that state.

**Self-play screenshot:**

![self play screenshot: ](./screenshots/SelfLearning.png?raw=true "Self Play")

**Playing with human screenshot:**

![Human Play: ](./screenshots/HumanPlay.png?raw=true "Human Play")
