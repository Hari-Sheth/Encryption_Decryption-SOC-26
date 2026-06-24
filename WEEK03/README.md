# Assignment 4

## Sentiment Analysis using RNN

RNN can learn the mapping between words in a sentence or relationship between elements in any sequence for that matter. One application of RNN is to find out the sentiment analysis of any sentence.
for any sentence your mode needs to output the- feelings of the author, as we call in english. So this is your dataset, make a rnn model, and take the outputs of that rnn and feed them to a NN (aka
Fully connected layer) and it should predict the sentiment.

import kagglehub

path = kagglehub.dataset_download("abhi8923shriv/sentiment-analysis-dataset")

print("Path to dataset files:", path)

NOTE: no need to make the RNN from scratch, it is really exhaustive, just get the maths behind it, it is enough. you can use the rnn from the library and connect it to a FC layer

## Substitution Cipher
Keeping expectations on the track, To be honest RNN is not that strong of a model to be able to crack substitution cipher (any substitution), but it can crack if the total permuations are small (some 5-10). so I would want in this exercise to also acknowledge the limitations of RNN since it is quite basic model.

So Make 2-3 permuations of the letters and make a dataset, in the same way as you did in the last week. Then pass it on to the model and check its accuracy.

NOTE: 
1. I tried using Bidirectional RNN for nearly 2k permuations of the data but at max it could just reach 40 percent, Atleast better than guessing (0.4>1/2k). You Dont need to use the bidirectional RNN, use the general unidirectional one only. (Expect accuracy to be on the lower side since this is not that strong model).
2. Use Bigger Datasets like a whole book by importing some libraries. And use the GPU for training, go to runtime settings ->change runtime type ->select GPU 
