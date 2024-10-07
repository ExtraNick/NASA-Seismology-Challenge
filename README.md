# NASA-Seismology-Challenge
 2024 NASA Space Apps Challenge Seismic Detection Across the Solar System
# How it works 
I use pandas for the .csv files data manipulation as DataFrames, using Jupyter Notebook for easing the tasks.

First, pandas is imported
The .csv file is loaded by pandas and designed to the variable "df"
The dataframe consists of: Absolute Time, Relative Time and Velocity columns
I then remove Relative time because i didn't find it necessary for the task at hand
I proceed to split Absolute time in 3 collumns:
-Hours
-Minutes
-Seconds 
The reason for this is to make the dataframe more readable for myself
At this point i also snapshot the Absolute Time under the variable Total_time, which can be used to recovering the Absolute Time column if necessary

The Data frame is then reorganized as follows:
Hour -> Minute -> Seconds -> Velocity

at this point the Dataframe could be plotted into a graph for viewing, however i ran into many issues in importing modules in both my Windows 11 and Linux machine, so i skipped this step.

The next step is getting rid of irrelevant data:
I convert velocity into float for manipulation
I take the average of the Velocity collumn
I take the highest (max) value of the Velocity column
I take the lowest (min) value of the Velocity column
I subtract the lowest value from the highest.

This accomplishes a couple things:
At this point i could tell by the average that there wasn't that much variation between the quantity of High and Low values
Imagine a graph: The  Low value hangs just as far from the Y=0 axis than the High value hangs from that same point in the graph.
By subtracting both values, i can infer a value in which general noise will fluctuate.

Knwoing this, i can proceed to the next step: removing noise from the sample
The variable "median" represents the value of noise one can expect from the readins.
I then remove every single row that contains a velocity value that is Positive and lower than the median noise variable
I then remove every single row that contains a velocity value that is Negative and higher than the median noise variable inverted (negative)
For each step described aboved, i create a snashotted dataframe derived from the Original dataframe that stores only values that are deemed relevant

With this, i now have 3 dataframes:
-Original dataframe containing ALL values
-High dataframe containing Values that are higher than the median variable (noise)
-Low dataframe containing Values that are lower than the inverted median variable (noise)

The next step is to bring these together into a single dataframe that will be exported.
I perform an outer join of the High and Low Dataframe, preserving their respective indexes that were defined in the Original dataframe
I fill the N/A (empty) cells with respective datam from the corresponding Indexes of both High and Low Dataframes on the Original dataframe

And after some cleaning up, i export everything into a single file that contains only the filtered and relevant data.

# Results
A 22,419,039 characters file was filtered into a 424,898 characters
The [graph](https://i.imgur.com/OlPQoKR.png) as viewed in a 1920x1080 screen
The [graph](https://i.imgur.com/ZONkOqW.png) as viewed in a 1366x768 screen
