# NASA-Seismology-Challenge
 2024 NASA Space Apps Challenge Seismic Detection Across the Solar System
# How it works 
I use pandas for the .csv files data manipulation as DataFrames, using Jupyter Notebook for easing the tasks.

First, pandas is imported <br>
The .csv file is loaded by pandas and designed to the variable "df"<br>
The dataframe consists of: Absolute Time, Relative Time and Velocity columns<br>
I then remove Relative time because i didn't find it necessary for the task at hand<br>
I proceed to split Absolute time in 3 collumns:<br>
-Hours<br>
-Minutes<br>
-Seconds <br>
The reason for this is to make the dataframe more readable for myself<br>
At this point i also snapshot the Absolute Time under the variable Total_time, which can be used to recovering the Absolute Time column if necessary

The Data frame is then reorganized as follows:<br>
Hour -> Minute -> Seconds -> Velocity

at this point the Dataframe could be plotted into a graph for viewing, however i ran into many issues in importing modules in both my Windows 11 and Linux machine, so i skipped this step.

The next step is getting rid of irrelevant data:<br>
I convert velocity into float for manipulation<br>
I take the average of the Velocity collumn<br>
I take the highest (max) value of the Velocity column<br>
I take the lowest (min) value of the Velocity column<br>
I subtract the lowest value from the highest.<br>

This accomplishes a couple things:<br>
At this point i could tell by the average that there wasn't that much variation between the quantity of High and Low values<br>
Imagine a graph: The  Low value hangs just as far from the Y=0 axis than the High value hangs from that same point in the graph.<br>
By subtracting both values, i can infer a value in which general noise will fluctuate.<br>

Knwoing this, i can proceed to the next step: removing noise from the sample<br>
The variable "median" represents the value of noise one can expect from the readins.<br>
I then remove every single row that contains a velocity value that is Positive and lower than the median noise variable<br>
I then remove every single row that contains a velocity value that is Negative and higher than the median noise variable inverted (negative)<br>
For each step described aboved, i create a snashotted dataframe derived from the Original dataframe that stores only values that are deemed relevant<br>

With this, i now have 3 dataframes:<br>
-Original dataframe containing ALL values<br>
-High dataframe containing Values that are higher than the median variable (noise)<br>
-Low dataframe containing Values that are lower than the inverted median variable (noise)<br>

The next step is to bring these together into a single dataframe that will be exported.<br>
I perform an outer join of the High and Low Dataframe, preserving their respective indexes that were defined in the Original dataframe<br>
I fill the N/A (empty) cells with respective datam from the corresponding Indexes of both High and Low Dataframes on the Original dataframe<br>

And after some cleaning up, i export everything into a single file that contains only the filtered and relevant data.

# Results
A 22,419,039 characters file was filtered into a 424,898 characters
The graph of the data as viewed in a 1920x1080 screen ![graph](https://i.imgur.com/OlPQoKR.png)
<br>
The graph of the data as viewed in a 1920x1080 screen ![graph](https://i.imgur.com/ZONkOqW.png)



Y axis -> Velocity <br>
X axis -> The Index of each reading <br>
Since the indexes update with  each reading (going off once every 4 seconds on average), i did not include the time values in the graph

Data was tested with the Mars training data<br>
When testing was attempted with Moon training data, the code did not work 

## TO DO 
These are things i would work on if i had more time: <br>
Find a way to get the program to work with moon data <br>
Fix plotly and matplot import <br>
Gett proper graphs <br>
Test data with more samples
