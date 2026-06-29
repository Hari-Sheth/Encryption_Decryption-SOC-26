# Vigenere Cipher

Vigenere cipher is a polyalphabetic cipher, unlike the monoalphabetic ones- substitution and ceiser (where the alphabet was mapped to a single alphabet- one to one function), but in vigenere cipher we do one to many mapping.
A key is used to create such one to many mapping, and main objective is to figureout the key while deciphering it.      

Vigenere cipher details:    
https://www.geeksforgeeks.org/dsa/vigenere-cipher/

# Deciphering Vigenere Cipher 
To decipher the vigenere cipher we need to find the key, but the key might be anything any word- hence for simplicity we assume the key might have a length less than or equal to 5, since the avg word length in English is 4.7 (approx. 5).
and then we have to find what the word is after deciphering its length. So for this we need to make two models- one, which can predict the len of the word, second, the word itself.

# Part 1
Making a model to find out the length of the Key

How to make it?
1. Make your dataset by importing text from any book, use this code to get one:         

import nltk        
nltk.download('gutenberg')        
from nltk.corpus import gutenberg               
text_net = (        
    gutenberg.raw('austen-emma.txt')+gutenberg.raw('austen-persuasion.txt')             
).lower()  

2. Choose your symbols set like done in ceiser cipher, all lower english letters +' '+ and other symbols. So make sure you remove other symbols and convert upper case to lower in the text.
3. Divide the data into 5 parts, and each part to some 100 letter wide blocks. Make a dataset function which generates random n length key and applies vigenere cipher to the text inputted, hence text,n are given as input it, ciphers it by using the Symbols set in step 2.
4. Now, pass on each part to the function and use the n= part number+1, i.e. 0th part->n=1, 1st part->n=2,etc. Also make a label set, it is simple- [0,0,0,..len(part[0])][1,1,1..len(part[1])].... [REMEMBER: we are not starting from 1 even if in the function we do part+1, because in cross entropy loss it expects us to start the labels from 0, dw we can add 1 at the end]
5. Make a LSTM class use nn.LSTM and make it bidirectional, (bidirectional=True) and since it is bidirectinal the input to fc is 2*hidden_size. The forward layer looks like this:  
   
    def forward(self, x):          
        h0 = torch.zeros(2, x.size(0), self.hidden_size).to(x.device)  # 2 for bidirectional      
        c0 = torch.zeros(2, x.size(0), self.hidden_size).to(x.device)      
        out, _ = self.lstm(x, (h0, c0))      
        out = self.fc(out[:, -1, :])        
        return out      
7. make a dataset, where it converts the cipher letters into one hot encoding np.array and its corresponding label. (each block is of 100 ciphered letters, hence the one hot would be= 100 x len(symbols))
8. now train the model and test it

# Finding the key using LSTM (OPTIONAL)
This segment is optional since it requires a Dual LSTM model, we can do this question using Transformers which would be more robust, so if you wat to do this using LSTM you can take this-

In the last part we found out the size of the key, This timw we will be finding the key itself, The LSTM now learns the repetition and the subsequennt repeating patter and would try to guess the key.     
You can follow these guidelines to make the LSTM:    
(We assume that the length of the key is 5 since, if it works for 5 it will work for the smaller lengths aswell)
1. Use the same dataset, the same class to cipher the text and the same dataloader
2. choose your symbols- A-Z,' ',...etc, and make a set ,say symbols. Now pre process the data in the same fashion as done in all the previous deciphering models. 
3. Instead of dividing the set into parts of different lengths, just divide the text into many segments of 100- 150 chr each, and now make the txt ciphered.
4. divide into test and train, and one hot encode the characters in each segment, so you would get a vector of size- 100xlen(symbols),Along with this also concatenate the Actual sentence so that your output becomes - 100x(len(symbols)*2).
5. Make a LSTM model- the model is a little bit different it has one encoder and a decoder branch, dw both are lstms only- th output of one will be fed to the other guy. A sample code is given:
```python
import torch
import torch.nn as nn
import torch.nn.functional as F

class Bidirectional_Encoder(nn.Module):
    def __init__(self, input_size, hidden_size):
        super().__init__()
        self.lstm = nn.LSTM(input_size, hidden_size, batch_first=True, bidirectional=True)

    def forward(self, x):
        outputs, (hn, cn) = self.lstm(x)
        
        hn_combined = torch.cat((hn[0, :, :], hn[1, :, :]), dim=1).unsqueeze(0)
        cn_combined = torch.cat((cn[0, :, :], cn[1, :, :]), dim=1).unsqueeze(0)
        
        return outputs, hn_combined, cn_combined

class Attention_Decoder(nn.Module):
    def __init__(self, input_size, hidden_size, output_size):
        super().__init__()
        self.lstm = nn.LSTM(input_size + hidden_size, hidden_size, batch_first=True)
        self.fc = nn.Linear(hidden_size, output_size)

    def forward(self, x, hidden_state, cell_state, encoder_outputs):
        hidden_reshaped = hidden_state.permute(1, 2, 0)
        
        raw_scores = torch.bmm(encoder_outputs, hidden_reshaped)
        attention_weights = F.softmax(raw_scores, dim=1)
        
        weights_flipped = attention_weights.permute(0, 2, 1)
        context = torch.bmm(weights_flipped, encoder_outputs)
        
        lstm_input = torch.cat((x, context), dim=2)
        
        out, (new_hidden, new_cell) = self.lstm(lstm_input, (hidden_state, cell_state))
        prediction = self.fc(out)
        
        return prediction, new_hidden, new_cell
```
6. Make the dataset and finally train the model and Test it

References:     
https://pradeep-dhote9.medium.com/seq2seq-encoder-decoder-lstm-model-1a1c9a43bbac        
https://www.geeksforgeeks.org/nlp/encoder-decoder-models/
