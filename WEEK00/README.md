
# Q.1  Finding the Killer
You are a member of the great CID team of a city. On Monday night (24/5/2024) at around 11 PM, You receive a call from locals that a person has been murdered in a desolate place which was near a pond 
under a bridge in city east. You interrogate the locals, and you find one lady who had seen someone running away with a knife from the crime scene from her window at around 10:45 PM and she was the one who called you first when
she checked the area. 
You have a witness, whom you need to trust since there are no other lead and you dont find much from the crime scene. The following is the information you get :

+ The Suspect looked like a man in his thirties to mid forties   (You assume his age &ge; 30 and age &le; 45)
+ The Suspect was around 5'11 , so you take the height &ge; 160 cm and height &le; 190 cm.
+ She wasn's sure about weight but didn't look lean so you assume wide range and you take the weight &ge; 50 and weight &le; 100.

You also get information about the city- city was divided into 4 parts - city north, city south, city east, city west. There was one hospital and school for the entire city and it was in the city north.
Getting into the city north or city west was difficult because there was forest in between. The forst route was closed after 8PM and people have to take a longer route 
Appromimate time to reach from one city part to east:
+ North to east : 30 min via forest route and 1 hr 30 min via long route
+ West to east :40 min via forest and 1 hr 45 min via long route
+ south to east :30 min

Victim: Teacher, mid 40s, lives in city east, Joined this occupation more than decade ago and had no rivalries.

Crime scene: under the bridge 2-3min away from victim's home.

You move on to the Family now- 

Any personal problems with someone? 

No, even all relatives live far away. He was a teacher why would he have any issues?

What was your Husband doing in that desolate area?

It was his favourite location to enjoy, no one knew it, he said he enjoys with his close friend talking and drinking, but I don't know who his friend w as, mostly his colleagues, Since he would talk with others much. He doesn't trust people easily eiter, his close friend would have been friend since long.

Close friend, huh. well, Thank you for your time, I am sorry for your loss.


You now collect the information of the people : https://drive.google.com/file/d/1JEVPBEmde_qflPzY6zWEzhwL7w0jGxbZ/view?usp=sharing

Your suspicion grows more towards the school teachers and you ask every teacher what they were doing during that time and their family members. All the family 
members of each family confirm that the every teacher was at home around 10PM more or less. 

You still get the Teacher information: https://drive.google.com/file/d/1IzVvDn60L5-1M9sHdOcV8OsDQJrYpLxG/view?usp=sharing

Find out who the killer was. 
Dw, if your approach might be different than me, in thinking. I tried to keep it more or less straightforwarded, to prevent any discrepancies, but still if you conclude with differnt person as killer, it will still be 
acknowledged as valid answer, so dw about solving correctly.

(Bonus : Explain what was the motive of the killer i.e. give a story plot, with your own imagination)



# Q2.  Rocket Fuel Data Analysis

Scientists at a futuristic space research station are testing experimental rocket fuels for interplanetary missions.

You are given a CSV file containing:
- fuel type
- temperature
- pressure
- thrust
- efficiency
- reactor stability
- oxygen levels
- target planet

Some sensor values are missing due to system failures.

Your task is to analyze and clean the dataset using Python with Pandas, NumPy, and Matplotlib.
Steps:
+ Explore the dataset , use the .head(),.shape,etc;
+ find missing values and replace them with the mean and median for pressure
+ sort
   - temperature ascending
   - efficiency descending
+ new column: `Power_Index = Thrust_kN * Efficiency_Percent`
+ plot all the columns
+ save the modified data as modified.csv

Dataset: https://drive.google.com/file/d/1766HwO3-2k5a2jvO3z8kbw_HFT672iKE/view?usp=sharing
