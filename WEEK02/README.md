# MLP for Deciphering

Last week we stumbled upon the Caesar cipher and frequency analysis. But is there a way to make a model which can give the rotation index when we pass on a crypted text.
Well, yes since caesar cipher is the easiest and faily straight-forwarded cipher a general MLP would do the work easily. How to do it?

# Preparation of a Dataset.
Since this is a word manipultion game, you can make your own dataset.    
1. Collect random text from any source, make sure you get good amount of text. The more the text, the better will be the model. (make a string of the total text)
2. Decide what all symbols (!,@,# even the space,etc) and letters you are going to use, let the total number of characters be N. (I would prefer to NOT use both the uppercase and lower case letters since it becomes difficult for the MLP to take care of the Casing of the letters aswell. I haven't tried it, but you want to test, you can test that case.)
3. Using the python libraries first transform the text and remove any unnecessary symbols/letters which you decided to remove in the second step. Then make the text uniform i.e. all lower cased words
4. Now divide the text into equal segments of N, ignore the fact that there might be some words that might split in this case.
5. Now make new copy of there segments and for each segment of text use the cipher, i.e. increment each character by the segmnet number, Say for the 4th segment the text is "hello", it turns to->"kipps",(note you need to take care that you have symbols here so Z will not map to D rather to some symbol, and the last symbol would map to D in this 4th segment case)
6. Yo cannot pass the Alphabets into the MLP, so you need to encode it. In all the ciphered segments, replace a->0,b->1.....
8. divide each segment into train and test data.(80-20)
9. split each train segment and test segment into smaller pieces i will call it subsegment of M character each, you can decide what this M is, (M is the input layer size of the MLP, I kept 20) -
10. Finally make labels for each M character set which represents its position. ex: the first subsegment of 20 characters of the 4th segment-[12,13,27,13.....] and its label would be 4.
11. Atlast grp all the train subsegments together train arr and all test together in test arr, <- data. similarly in the same order grp the train labels and test labels.
12. Now, make a dataset class as before which gives you torch.tensor of the subsegment and torch.tensor of the corresponding label

# Training
Finally you are done with the dataset, It might feel humongous task initially, but do it step by step, you will slowly do it.
Now use the same model as done bofore in the last week, just you need to kee the input as M nodes and output would be 1 node- obv it gives you the shift/rotation index. 
Ensure you keep shuffle = True in dataloader.
Tune your parameters-learning rate, batch size, etc to get better results.

Test your model yourself by giving it some ciphered text.


