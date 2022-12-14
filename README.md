# DeepLearningFinal
UW Deep Learning Final Project

Video: https://youtu.be/9lMMUyqHQi4

Abstract: 
The idea was to create a chess AI based on evaluations from existing chess engines. If successful this would be much easier than trying to teach the AI how to play chess from the very beginning. The AI just tries to find the correct evaluation for a given position and makes the move that leads to the best highest evaluation.

The first step was to find a good dataset that contains chess positions and the corresponding evaluations by the best modern chess engines. The best one I found was from this source: https://colab.research.google.com/drive/1smI2B7kiwzkr43TqnCYOpxocZlI0kPUh, it contains a large number of games played on the open source chess platform lichess.org. The dataset had a lot of information about the chess positions like usernames, rating and so on. But the only thing interesting to us was the FEN and evaluation of the position. FEN´s are a kind of encoding for a chess position. Using pythons library python-chess it was possible to extract the positions from the FEN´s. 

The idea was now to create some kind of representation of these positions that a neural network can understand. Then it would be possible to feed the positions and the evaluations to the neural network and to train it on them. This would then hopefully lead to the neural network beeing able to predict the evaluations for positions it has not seen before. The problem with this might be that a chess positions is very complex and small changes can influece the evaluation by a lot. 

For the task I chose a Convolutional Neural Network. A chessboard would then be looked at as if it was an image with 8x8 pixels. To add more information to the "images" I chose to represent the chessboard as a 8x8x12 image, with every layer containing the information about one specific piece of one color. For example the first layer has a 1 everywhere where a white pawn stands and the rest of the pixels is 0. I also tried different representations like having only the 8x8 image or giving black pieces the value 0, empty squares the value 0.5 and white pieces the value 1.

This data is then given to the neural network. I tested many different configurations for the neural network, having 2-5 convolutional layers, 1-3 fully connected layers in the end, padding and no padding, stride 1 or 2 and so on. For the prediction I tried different ways to represent the score. Having negarive and positive scores, only positive scores and even changing the whole network to predict classes instead of scores. That means there is a class for "White is winning", "White is better", "Equal", "Black is better" and "Black is winning". 

The issue with all there approaches was that the network returned the same result for any input I gave to it. Also some of the layers of the network always return tensors with only zeroes. That means the network doesn´t save any information about the input and just returns the average of all the evaluation scores from the training data. The reason for that is probably that the task is too complex for the network to solve. A chess position is very complex and is hard to generalize. Small changes can completely flip the evaluation which makes it hard for the network to find a way to evaluate the position. It is not like in an image, if for example the image contains a car there are almost always wheels and windows in the car. This is something the network can "remember" and the use to find cars in other images. With a chess position there are very few things that are similar about positions. One thing that comes to mind is the material count, who has more pawns, queens, ... but even that doesn´t represent the position as piece activity also plays a big role in the evaluation. 

I then implemented a simple way to let the AI play against itself. It uses an opening database for the first moves. Opening databases check if the current position is a position they know. If yes they return the best move for the current position. These were created by professional chess players and other chess AI´s and help the AI to play better in the first moves. But when my AI reaches the end of the opening book it just starts to make random moves. This makes total sense given that the neural network evaluates all positions equally leading to a random selection of a move. 

I did not think that creating a chess AI in this way would be so hard. The positions are way more complex than I thought, at least I was hoping for the Network to find some sort of similarity between "good" and "bad" positions. This kind of approach is rarely used in the creation of competitive engines and now I understand why. The common way to do it is to let the AI play against itself, rewarding it for winning and punishing it for loosing. But this requires a huge amount of computing power and takes a long time. I wanted to try some of the alternatives which in the end did not work out too well. 

This is the jupyter notebook I used for the project: https://colab.research.google.com/drive/1ScKOzKAngA1HoU_pfJbp58ujIdrxA6Sb

It has been changed a lot during the process of the project.

![Chess01](https://user-images.githubusercontent.com/91910483/207732119-4814826f-dca6-45c5-ba53-85813c925fec.PNG)
![chess02](https://user-images.githubusercontent.com/91910483/207732137-7dcc8768-075f-4ba4-ab0c-888f07f55207.PNG)

These are some examples for the network making random moves. In the first image black just moves the knight in from of the pawn where it can be captured. And on the next move white does not take the knight but moves its own knight without any reason for it. 
