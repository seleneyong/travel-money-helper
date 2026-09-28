#Developer Diary

##Entry 1 - Starting the project

**Project Idea**
Building a *Travel Money Helper*, which help users estimate how much money they need for a trip
This program will include calculating costs such as visa, flights, accommodation, meals, travel insurance, and emergency money
This program can be useful for planning a trip 

**The structure of my project**
First, users chooses destination(input).
Second, users chooses number of days(input).
Third, program reads reference costs from travel costs.csv file(output).
Forth, program shows estimated costs for different destination(output).
Fifth, Users can choose "Y/N" for entering their own costs(input).
Six, python calculate the personalised budget(output).
Seven, AI gives budgeting suggestion.
Eight, Final travel budgeting.

**How I started**
First, I planned what information the program need from the users such as how much needed for visa, flights, accommodation, meals, travel insurance, and emergency money.
Second, I decided to create a "Travel costs.csv" file, which will be used as a reference costs that store example of travel costs for different destination such as Japan, Thailand, New Zealand, Singapore, Malaysia, Korea and London (Users can replace the data with their own costs by choosing "N" ).
Third, I created a "Travel money helper.ipynb" Colab notebook, and loaded the "Travel costs.csv" file using pandas. 
