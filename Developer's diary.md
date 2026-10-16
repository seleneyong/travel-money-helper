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

##Entry 2- Calculating estimated travel costs based on CSV file

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
Third, program will multiplied the cost for accommodation, meals, and transport by the number of days, as it is a daily costs.
Fourth, display the estimated costs for the selected destination.
*Problem faced*
1. Initially, I did not use .str.lower() and .lower() when finding the selected destination typed by the users, so if user typed japan the program will state that japan is not found in the Travel Costs.csv file. Therefore, by adding this it will ignore the uppercase and lowercase differences.
2. I faced an error when calculating and displaying the estimated travel costs, I got a KeyError: 'accommodation_total'. This might happened because accommodation_total was a variable I created, not a column name in my CSV file. I made the same mistake with meals_total and transport_total when I added them to the cost_columns list.
   
AI Prompt used: "Why did i get this error and can i use my code to calculate and display the estimated travel costs?"

Solution: "Yes, you can use most of your code! The error happens because accommodation_total is a variable you created, not a column name in your CSV file.
1. Why do you get this error?
You created this variable:
```
accommodation_total = row['Accommodation_Cost'] * days
```
This calculates the total accommodation cost for the number of days.
But later, you wrote:
```
cost_columns = [    'Visa_Cost',    'Flight_Cost',    'accommodation_total',    'meals_total',    'Travel_Insurance_Cost',    'transport_total',    'Emergency_Money']
```
When you use this line:
```
row[column]
```
Python looks for a column called 'accommodation_total' in your CSV data. However, your CSV column is actually called 'Accommodation_Cost', so pandas raises a KeyError.
In simple words, you are asking pandas to find a column that does not exist in your CSV."

What I kept and changed:
This means that pandas was looking for accommodation_total as a column in my CSV file, but that column did not exist. Therefore, I kept my original code structure, and continued calculating accommodation, meals and transport costs based on the number of days. I removed cost_columns because my accommodation, meals and transport totals have already been calculated as separate variables. In addition, I used accommodation_total, meals_total and transport_total directly when displaying and calculating the costs, and I added each cost together manually to calculate total_cost.

##Entry 3 - Personalised costs
*Problem faced*
1. Initially, I did not use .strip().upper() when handling the choice typed by the users, so if user typed in with extra spaces and lowercase the program will state an error. Therefore, by adding this it will remove the extra spaces and changes lowercase to uppercase, so it can be handled corrcetly.
2. I faced an error when users enter an incorrect text, such as fifty instead of a number 50 when entering their travel costs. Therefore, I wanted the program to display "Please enter an amount in numbers" and ask the user to reenter again

AI Prompt used: "How can I make the program display 'Please enter an amount in numbers' when users enter text instead of a number for their travel costs?"

Solution:
<img width="520" height="776" alt="image" src="https://github.com/user-attachments/assets/d5252460-33cd-4f03-828a-2ed2c4c196a7" /> <img width="495" height="461" alt="image" src="https://github.com/user-attachments/assets/c5467338-625b-40d6-8ea9-8af66ea9cb97" />

What I changed:
I changed the cost input by adding try and except ValueError, a while True loop and break. This is added to both sections where users enter their own costs, whether the destination is found in the CSV file or not. Thus, when a user enter an incorrect text the program would not stop and cause an error.

#input() is used to collects what the user type
#float() is used to converts the input into a number so it can be calculated by Python
