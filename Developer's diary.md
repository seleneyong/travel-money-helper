#Developer Diary

##Entry 1 - Starting the project

**Project Idea**
Building a *Travel Money Helper*, which help users estimate how much money they need for a trip
This program will include calculating costs such as visa, flights, accommodation, meals, travel insurance, transport fee, and emergency money
This program can be useful for planning a trip 

**The structure of my project**
First, users chooses destination and number of days(input).
Second, program reads reference costs from travel costs.csv file.
Third, program checks whether the selected destination exists in the CSV file.
Fourth, if destination not found, program will ask users to enter their own destination and costs for all categories.
Fifth, if destination is found, users can choose "Y/N" to decide whether they want to enter their own costs. If Y(yes) the program will asks them to enter their own costs, if N(no) the program uses the estimated cost from the CSV file(input).
Sixth, python calculate the personalised budget(output).
Seventh, users enter their available budget, and the program checks whether their money is enough for the trip.
Eight, Gemini AI gives budgeting suggestion based on the calculated travel costs and available budget.
Ninth, program displays the final travel budget, including the total estimated costs, remaining money or budget shortfall, and AI budgeting suggestion.

**How I started**
First, I planned what information the program need from the users such as how much needed for visa, flights, accommodation, meals, travel insurance, transport fee, and emergency money.
Second, I decided to create a "Travel Costs.csv" file, which will be used as a reference costs that store example of travel costs for different destination such as Japan, Thailand, New Zealand, Singapore, Malaysia, Korea and London (Users can replace the data with their own costs by choosing "N" ).
Third, I created a "Travel money helper.ipynb" Colab notebook, and loaded the "Travel Costs.csv" file using pandas. 

**Loading the CSV file**
First, I uploaded the created Travel Costs.csv file into Colab.
Second, I used df = pd.read_csv('Travel Costs.csv'), to reads the Travel Costs CSV file.
Third, I used print(df.dtypes), to check whether the costs is read as number.
Fourth, I cleaned the Visa_Cost, Flight_Cost, Accommodation_Cost, Meals_Cost, Travel_Insurance_Cost, Transport_Cost, Emergency_Money columns by removing the dollar signs and commas, then converted the text into a number so Python could use them for calculation.

**Estimated travel costs**
First, display all the available destination from the Travel Costs.csv file.
Second, users choose destination and days.
Third, 
Initially, I did not use .str.lower() and .lower() when finding the selected destination typed by the users, so if user typed japan the program will state that japan is not found in the Travel Costs.csv file. Therefore, by adding this it will ignore the uppercase and lowercase differences 


    
#input() is used to collects what the user type
#float() is used to converts the input into a number so it can be calculated by Python
