# Assignment 2

# Q1. Fisher Iris's Flowers
This is a very famous dataset collected by Fisher Iris way back in 1930s, it has the Petal,sepal widths and lengths corresponding to 4 different flower species. Make a MLP using NN such that it 
classifies these 4 flower species.  
 use this code snippet to get the dataset: 
 
import kagglehub    
path = kagglehub.dataset_download("uciml/iris")    
print("Path to dataset files:", path)

Change the learning rate, since the dataset is small I wont expect you to be using batches, but still you can try and observe its effect. Also change the number of layers and observe effect if any.

# Q2 Caeser Cipher
Lets time-travel back to the year 1586, England. At the time, Mary was imprisoned by her cousin, Queen Elizabeth I of England. While under house arrest, Mary secretly communicated with a young Catholic gentleman named Anthony Babington, who had devised a plot to assassinate Elizabeth, free Mary, and place her on the English throne
On July 17, 1586, Mary wrote a long logistical response to Babington's assassination proposal. The text that proved her treason was encrypted using caeser cipher, which was decrypted by Thomas Phelippes is: 

dyvkrwwrzbcksvz:xkdyeck@bv@rbvukr:ukw/btvckz:kbvruz:vccks/dykgzdy/edkr:ukgzdyz:kdyvkbvr,;mkdyv:kcyr,,kzdksvkdz;vkd/kcvdkdyvkczhkxv:d,v;v:kd/kg/b.nkdr.z:xk/buvbmke@/:kdyvkrtt/;@,zcyz:xk/wkdyvzbkuvczx:mkzk;riksvkceuuv:,ikdbr:c@/bdvuk/edk/wkdyzck@,rtvmkr:ukdyrdkr,,ki/ebkw/btvckz:kdyvkcr;vkdz;vksvk/:kdyvkwzv,ukd/k;vvdk;vl

To make matters worse for the conspirators, Thomas Phelippes didn't just decrypt the letter—he forged a postscript at the very end of it using Mary's own cipher to entrap the specific assassins. He added:

zkg/e,uksvkx,rukd/k.:/gkdyvk:r;vckr:ukaer,zdzvck/wkdyvkczhkxv:d,v;v:kgyztykrbvkd/krtt/;@,zcykdyvkuvczx:;v:dnkw/bkdyrdkzdk;riksvkzkcyr,,ksvkrs,vmke@/:k.:/g,vuxvk/wkdyvk@rbdzvcmkd/kxzfvki/ekc/;vkwebdyvbkrufztvk:vtvccrbikd/ksvkw/,,/gvukdyvbvz:

Use frequency analysis to find out, what the msg was.    

(Assume the cipher works on the letters and symbols- ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', ' ', '.', ',', ';', ':', '/', '@'], so no other letter/symbol has been used. the cipher rotates the elements of the array as in the case of general caeser cipher. rotaion by 1 means the last becomes the first,first->second,etc.. Caeser cipher does the nth rotation 1<=n<=len(letters))    
NOTE : symbols are also encoded, not just the letters.    

OPTIONAL: If you are comfortable with the NN and have time, you can do this - make a neural network which can figure out n (rotation index) from any given text, This would be the next week's assignment but anyways, you can give it a shot :)
