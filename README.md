# DeepLearningFinal
UW Deep Learning Final Project

Abstract: 
The idea was to create a chess AI based on evaluations from existing chess engines. If successful this would be much easier than trying to teach the AI how to play chess from the very beginning. The AI just tries to find the correct evaluation for a given position and makes the move that leads to the best highest evaluation.

The first step was to find a good dataset that contains chess positions and the corresponding evaluations by the best modern chess engines. The best one I found was from this source: https://colab.research.google.com/drive/1smI2B7kiwzkr43TqnCYOpxocZlI0kPUh, it contains a large number of games played on the open source chess platform lichess.org. The dataset had a lot of information about the chess positions like usernames, rating and so on. But the only thing interesting to us was the FEN and evaluation of the position. FEN´s are a kind of encoding for a chess position. Using pythons library python-chess it was possible to extract the positions from the FEN´s. 

The idea was now to create some kind of representation of these positions that a neural network can understand. Then it would be possible to feed the positions and the evaluations to the neural network and to train it on them. This would then hopefully lead to the neural network beeing able to predict the evaluations for positions it has not seen before. The problem with this might be that a chess positions is very complex and small changes can influece the evaluation by a lot. 

