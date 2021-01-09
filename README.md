# Alpha Zero for maplestory reversi

Main code from [alpha-zero-general](https://github.com/suragnair/alpha-zero-general).
Modified the game logic to have 4 blocked blocks in the board.

```Coach.py``` contains the core training loop and ```MCTS.py``` performs the Monte Carlo Tree Search. The parameters for the self-play can be specified in ```main.py```. Additional neural network parameters are in ```othello/{pytorch,keras,tensorflow,chainer}/NNet.py``` (cuda flag, batch size, epochs, learning rate etc.). 

To start training a model for Othello:
```bash
python main.py
```
Choose your framework and game in ```main.py```.


### How to use?

Now in ```./temp```, there is a pre-trained model which I have trained for 4 hours.
I guess the whole training time requires about 3 days, so the model for testing now doesn't have ideal strategy for winning the game.

First install all required pip package including pytorch, by ```pip install -r requirements.txt```(python3).

To play game, you can pushc command ```python pit.py```(python3).
The ```pit.py``` loads the trained model(```best.pth.tar```) located in ```./temp```, and consists the AI enemy.

After starting the game, the console requires you to input 4 blocked blocks.
The board consists of 8x8 blocks, and to input the intended block you have to input the (y x) coordinate splitted with space, starting from y axis.
For example for the board below, you can type (1 1), (1 6), (6 2), (6 6) in order without brackets.
```
   0 1 2 3 4 5 6 7 
-----------------------
0 |- - - - - - - - |
1 |- B - - - - B - |
2 |- - - - - - - - |
3 |- - - X O - - - |
4 |- - - O O O - - |
5 |- - - - - - - - |
6 |- - B - - - B - |
7 |- - - - - - - - |
-----------------------
```

After you input the blocked blocks, it requires you to type who (ai/human) will start the game. Just type one of them.

Then the game starts, by typing the (y x) value for each turn, try to win the ai :)

### Experiments

(Experiment results are from the original code, not the maplestory-reversi.)

We trained a PyTorch model for 6x6 Othello (~80 iterations, 100 episodes per iteration and 25 MCTS simulations per turn). This took about 3 days on an NVIDIA Tesla K80. The pretrained model (PyTorch) can be found in ```pretrained_models/othello/pytorch/```. You can play a game against it using ```pit.py```. Below is the performance of the model against a random and a greedy baseline with the number of iterations.
![alt tag](https://github.com/suragnair/alpha-zero-general/raw/master/pretrained_models/6x6.png)

A concise description of our algorithm can be found [here](https://github.com/suragnair/alpha-zero-general/raw/master/pretrained_models/writeup.pdf).

### Contributing
While the current code is fairly functional, we could benefit from the following contributions:
* Game logic files for more games that follow the specifications in ```Game.py```, along with their neural networks
* Neural networks in other frameworks
* Pre-trained models for different game configurations
* An asynchronous version of the code- parallel processes for self-play, neural net training and model comparison. 
* Asynchronous MCTS as described in the paper

### Contributors and Credits
* [Shantanu Thakoor](https://github.com/ShantanuThakoor) and [Megha Jhunjhunwala](https://github.com/jjw-megha) helped with core design and implementation.
* [Shantanu Kumar](https://github.com/SourKream) contributed TensorFlow and Keras models for Othello.
* [Evgeny Tyurin](https://github.com/evg-tyurin) contributed rules and a trained model for TicTacToe.
* [MBoss](https://github.com/1424667164) contributed rules and a model for GoBang.
* [Jernej Habjan](https://github.com/JernejHabjan) contributed RTS game.
* [Adam Lawson](https://github.com/goshawk22) contributed rules and a trained model for 3D TicTacToe.
* [Carlos Aguayo](https://github.com/carlos-aguayo) contributed rules and a trained model for Dots and Boxes along with a [JavaScript implementation](https://github.com/carlos-aguayo/carlos-aguayo.github.io/tree/master/alphazero).

