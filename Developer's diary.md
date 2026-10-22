#Developer Diary

##Entry 1 - Starting the project

**Project Idea**

Building a *Travel Money Helper*, which help users estimate how much money they need for a trip
This program will include calculating costs such as visa, flights, accommodation, meals, travel insurance, transport fee, and emergency money
This program can be useful for planning a trip 

**The structure of my project**
1. First, users chooses destination and number of days(input).
2. Second, program reads reference costs from travel costs.csv file.
3. Third, program checks whether the selected destination exists in the CSV file.
4. Fourth, if destination not found, program will ask users to enter their own destination and costs for all categories.
5. Fifth, if destination is found, users can choose "Y/N" to decide whether they want to enter their own costs. If Y(yes) the program will asks them to enter their own costs, if N(no) the program uses the estimated cost from the CSV file(input).
6. Sixth, python calculate the personalised budget(output).
7. Seventh, users enter their available budget, and the program checks whether their money is enough for the trip.
8. Eight, Gemini AI gives budgeting suggestion based on the calculated travel costs and available budget.
9. Ninth, program displays the final travel budget, including the total estimated costs, remaining money or budget shortfall, and AI budgeting suggestion.

##Entry 2- Calculating estimated travel costs based on CSV file

**How I started**

First, I planned what information the program need from the users such as how much needed for visa, flights, accommodation, meals, travel insurance, transport fee, and emergency money.
Second, I decided to create a "Travel Costs.csv" file, which will be used as a reference costs that store example of travel costs for different destination such as Japan, Thailand, New Zealand, Singapore, Malaysia, Korea and London (Users can replace the data with their own costs by choosing "N" ).
Third, I created a "Travel_Money_Helper.ipynb" Colab notebook, and loaded the "Travel Costs.csv" file using pandas. 

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

**Problem faced**

1. Initially, I did not use .str.lower() and .lower() when finding the selected destination typed by the users, so if user typed japan the program will state that japan is not found in the Travel Costs.csv file. Therefore, by adding this it will ignore the uppercase and lowercase differences.
   
2. I faced an error when calculating and displaying the estimated travel costs, I got a KeyError: 'accommodation_total'. This might happened because accommodation_total was a variable I created, not a column name in my CSV file. I made the same mistake with meals_total and transport_total when I added them to the cost_columns list.
   
AI Prompt used: "Why did i get this error and can I use my code to calculate and display the estimated travel costs?"

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

First, if the destination is found, and the user enters N, the program keeps the estimated cost from the CSV. If the user enters Y, they can enter their own cost. If the destination is not found, users get to enter their own destination and costs.
Second, Python then calculates the personalised travel budget using the final chosen costs.

**Problem faced**

1. Initially, I did not use .strip().upper() when handling the choice typed by the users, so if user typed in with extra spaces and lowercase the program will state an error. Therefore, by adding this it will remove the extra spaces and changes lowercase to uppercase, so it can be handled corrcetly.
   
2. I faced an error when users enter an incorrect text, such as fifty instead of a number 50 when entering their travel costs. Therefore, I wanted the program to display "Please enter an amount in numbers" and ask the user to reenter again

AI Prompt used: "How can I make the program display 'Please enter an amount in numbers' when users enter text instead of a number for their travel costs?"

Solution:

<img width="520" height="776" alt="image" src="https://github.com/user-attachments/assets/d5252460-33cd-4f03-828a-2ed2c4c196a7" /> <img width="495" height="461" alt="image" src="https://github.com/user-attachments/assets/c5467338-625b-40d6-8ea9-8af66ea9cb97" />

What I changed:
I changed the cost input by adding try and except ValueError, a while True loop and break. This is added to both sections where users enter their own costs, whether the destination is found in the CSV file or not. Thus, when a user enter an incorrect text the program would not stop and cause an error.

##Entry 4 - User"s available travel budget

First, ask how much is the user budget for the trip.
Second, compare it with total personalised cost.

**Problem faced**

1. I  was confused on how I change my code so users only can enter their available budget in a positive amount

AI Prompt used(1): "How can I change my code so that when users enter their available budget, they can only enter a positive amount? Currently, my program continues to run even when users enter a zero or a negative amount, but I want the program to display an error message 'Please enter a positive amount only' and ask them to enter their budget again until they enter a valid amount"

Solution:

<img width="482" height="739" alt="image" src="https://github.com/user-attachments/assets/1d8ec498-4d43-4a8e-9fab-23c50c1d7d3f" />

However, I realised this code did not handle the cases where the user might entered a text such as fifty, instead of a number.

Therefore, I changed my AI Prompt used(2):
"How can I change my code so that users can only enter a valid positive number for their available budget? Currently, my program continues to run when users enter a zero or a negative amount, but I want the program to display an error message, 'Please enter a valid positive amount only'. Additionally, when a user enters text, I want the program to display an error message, 'Please enter an amount in numbers', and ask the user to enter their budget again until they enter a valid positive number. Can you explain how to fix this using simple Python code?"

Solution:

<img width="490" height="485" alt="image" src="https://github.com/user-attachments/assets/65278eed-60bf-41b5-b348-7d3c75a1da90" />
<img width="493" height="724" alt="image" src="https://github.com/user-attachments/assets/f0aab75c-7181-4881-b6e0-eba726e9c593" />

What I changed:
I changed my code to handle both negative amount and text inputs. I used a try and except ValueError to avoid the program to stop running when user entered a text, a while loop to keep asking until the user enter an amount greater than zero, and a if condition to display an error message when the user entered zero or a negative number. 

##Entry 5 - Conversational assistant to give budgeting suggestion

First, set up the API key in colab secrets.
Second, install and connect to Gemini.
Third, create the ask_gemini(prompt) function, which accepts a prompt, send it to Gemini and receives the response.
Fourth, test whether the Gemini works.
Fifth, connect Gemini to my existing calculated travel budget.

**Problem faced**

1. I was unsure about how I can set up the Gemini API to work with my existing travel budget calculation. I wanted to understand how to send a prompt to Gemini and receives budgeting suggestions based on the user's destination, travel costs and available budget

AI Prompt used: "Can you explain in simple words what I need to do to add the Gemini API to work with my existing travel budget calculation? Explain how the API key, prompt and Gemini response work, and how they can fit into my project. I want to understand the steps before I start writing the code myself."

Solution:

<img width="516" height="786" alt="image" src="https://github.com/user-attachments/assets/ef988d55-6abb-4980-8923-d8c999db962e" />
<img width="532" height="791" alt="image" src="https://github.com/user-attachments/assets/c846a651-55cc-46a5-9a50-30f04df551b9" />
<img width="529" height="479" alt="image" src="https://github.com/user-attachments/assets/3e8a669e-4324-41fa-a9be-ff5a24d5d00f" />

What I did:
After reading the AI's explanation, I learned that I need to create an ask_gemini(prompt) function to send a prompt and receive Gemini's response. I have not connected everything together yet, so my next step is to set up and test the Gemini API before linking it to my budget calculation.

2. I set a personality for Gemini so that it could give budgeting suggestions in the style I wanted. However, I noticed that Gemini's responses did not always match the personality I had set. This made me unsure how to change my prompt or code to make Gemini follow the personality more closely.

AI Prompt used: "How can I fix my Gemini API code so that Gemini follows the personality I set? I created a personality variable that tells Gemini to be a friendly travel budgeting assistant, include multiple relevant emojis in every sentence, and give practical and realistic suggestions. However, Gemini's responses do not follow these instructions. Can you help me identify what is wrong with my code and explain how to fix it using simple Python code?"

Solution:

<img width="657" height="560" alt="image" src="https://github.com/user-attachments/assets/07410ef2-65e4-4c00-92e6-7c716ae917bd" />
<img width="684" height="749" alt="image" src="https://github.com/user-attachments/assets/0811c9f4-52bf-4bd3-a2c2-384da878deed" />
<img width="665" height="465" alt="image" src="https://github.com/user-attachments/assets/9d610853-7b3c-4828-b781-4caf22ad415a" />

What I changed:
I changed my code by adding the personality instruction to the contents when calling Gemini. Thus, Gemini could receive both the personality instructions and the prompt. 
   
##Entry 6 - Travel Money Helper interface

First, install Gradio and import the libraries.
Second, create the processing function.
Third, create the Gradio interface.

I identified several objects in my solution, including the destination textbox, days number input, available_budget number input, and result textbox. I also used the demo Blocks object to organise the Gradio interface and the calculate button to connect the user's inputs to my processing function.

One decision I made myself was to validate the user's inputs inside my get_travel_details() function instead of relying only on the Gradio interface, because I wanted my program to handle invalid inputs and display a clear error message before processing the travel details.

**Problem faced**

1. I wanted to make sure users entered the correct travel details before submitting the travel deails, such as entering a destination, a positive number of days, and a positive available budget

AI Prompt used: "How can I improve my Gradio interface so that users must enter a destination, a positive number of days, and a positive available budget before submitting their travel details? Can you explain to me what I should do and why?"

Solution:

<img width="564" height="804" alt="image" src="https://github.com/user-attachments/assets/6fffc4ff-023d-47d5-92c9-b986b801a991" />
<img width="563" height="724" alt="image" src="https://github.com/user-attachments/assets/27830bd8-e3c0-4cca-83e3-9cd78228b0fa" />
<img width="537" height="440" alt="image" src="https://github.com/user-attachments/assets/00f508b3-9088-40d4-a10c-050409e97889" />

What I changed and rejected:
I added a condition inside my get_travel_details() function to check whether the user entered a destination. I used if not destination or not destination.strip() to make sure the destination was not empty or only made up of spaces.
For the number of travel days, I used if days <= 0 instead of the solution generated by AI, to display an error message if the user enters zero or a negative number. Additionally, I did not add minimum=1 to my Gradio Number component because I already included this check in my processing function.
For the available budget, I used if available_budget <= 0 instead of the solution generated by AI, to display an error message if the user enters zero or a negative amount.

2. While working on my Travel Money Helper, I faced a problem with my Gradio interface. At first, my program could only calculate travel costs using the information in my Travel Costs.csv file. If a user wanted to travel to a destination that was not in the CSV, the program would display a message saying that the destination could not be found. However, I want my program to address user's that might want to travel to other destinations or use their own estimated costs.

AI Prompt used: "How to improve my Gradio interface so users could choose whether to use the CSV costs or enter their own costs? and how to allow users to enter all their own costs when their destination was not available in the CSV? explain to me in simple and easy understanding

Solution:

<img width="795" height="668" alt="image" src="https://github.com/user-attachments/assets/b7ba500f-4f6c-4a84-b2c6-a1c10c1f24ec" />
<img width="743" height="801" alt="image" src="https://github.com/user-attachments/assets/0abbe33b-01cf-46f4-a35a-2acb5a05b1a7" />


What I did:
I used a dropdown for the Y/N choices for all seven costs, so user can choose whether to use the eastimated cost from CSV file or enters their own costs. Additionally, I also updated my get_travel_details() function to checks whether the destination exists in the CSV file. Besides that, I also updated the inputs connected to the submit button so the program can use the user's choices to calculate the total travel cost and compare it with their available budget.

3. I faced an error in the Gradio, initially, I did not know what is wrong in my code. Thus, I asked AI to help me identified what is wrong.

AI Prompt used: "Why is the result error in my Gradio, and how can I fix it? Please explain it in a simple and easy way.
```python
# Install and import the libraries

# install the Gradio library
!pip install -q gradio

# import the libraries
import gradio as gr
import pandas as pd

# load the travel costs CSV file
df = pd.read_csv("Travel Costs.csv")


# Create the processing function

# defines a function to receive the user's travel details from Gradio
def get_travel_details(
    destination, days, available_budget,
    visa_choice, user_visa_cost,
    flight_choice, user_flight_cost,
    accommodation_choice, user_accommodation_cost,
    meals_choice, user_meals_cost,
    insurance_choice, user_travel_insurance_cost,
    transport_choice, user_transport_cost,
    emergency_choice, user_emergency_money
):

    # checks whether the destination is entered
    if not destination or not destination.strip():
        return "Please enter a destination."

    # checks whether the number of days is positive
    if days is None or days <= 0:
        return "Please enter a positive number of days."

    # checks whether the available budget is positive
    if available_budget is None or available_budget <= 0:
        return "Please enter a positive amount."

    # checks whether the number of days is a whole number
    if not float(days).is_integer():
        return "Please enter a whole number of travel days."

    days = int(days)

    # finds the destination in the CSV
    row = df[
        df["Destination"].str.strip().str.lower()
        == destination.strip().lower()
    ]

    # store the user's own costs
    own_costs = {
        "Visa_Cost": user_visa_cost,
        "Flight_Cost": user_flight_cost,
        "Accommodation_Cost": user_accommodation_cost,
        "Meals_Cost": user_meals_cost,
        "Travel_Insurance_Cost": user_travel_insurance_cost,
        "Transport_Cost": user_transport_cost,
        "Emergency_Money": user_emergency_money
    }

    # store the user's Y/N choices
    choices = {
        "Visa_Cost": visa_choice,
        "Flight_Cost": flight_choice,
        "Accommodation_Cost": accommodation_choice,
        "Meals_Cost": meals_choice,
        "Travel_Insurance_Cost": user_travel_insurance_cost,
        "Transport_Cost": user_transport_cost,
        "Emergency_Money": user_emergency_money
    }

    # if the destination is not in the CSV, the user must enter every cost
    if row.empty:
        selected_costs = {}

        for category, amount in own_costs.items():
            if amount is None or amount < 0:
                return (
                    f"Destination not found in the CSV. "
                    f"Please enter a valid cost for {category}."
                )

            selected_costs[category] = amount

        cost_source = "Your own costs (new destination)"

    else:
        # get the matching CSV row
        row = row.iloc[0]
        selected_costs = {}

        # select either the CSV cost or the user's own cost
        for category, choice in choices.items():

            if choice == "Y":
                amount = own_costs[category]

                if amount is None or amount < 0:
                    return (
                        f"Please enter a valid cost for {category} "
                        f"because you selected Y."
                    )

                selected_costs[category] = amount

            else:
                selected_costs[category] = row[category]

        cost_source = "CSV estimates and/or your own costs"

    # calculate daily costs
    accommodation_total = (
        selected_costs["Accommodation_Cost"] * days
    )
    meals_total = selected_costs["Meals_Cost"] * days
    transport_total = selected_costs["Transport_Cost"] * days

    # calculate the total cost for the trip
    total_cost = (
        selected_costs["Visa_Cost"]
        + selected_costs["Flight_Cost"]
        + accommodation_total
        + meals_total
        + selected_costs["Travel_Insurance_Cost"]
        + transport_total
        + selected_costs["Emergency_Money"]
    )

    # compare the cost with the available budget
    remaining_budget = available_budget - total_cost

    if remaining_budget >= 0:
        budget_message = (
            f"Money remaining: AUD ${remaining_budget:.2f}"
        )
    else:
        budget_message = (
            f"Budget shortfall: AUD ${abs(remaining_budget):.2f}"
        )

    # display the result
    return (
        f"Destination: {destination.strip()}\n"
        f"Number of days: {days}\n"
        f"Cost source: {cost_source}\n"
        f"Estimated total cost: AUD ${total_cost:.2f}\n"
        f"Available budget: AUD ${available_budget:.2f}\n"
        f"{budget_message}"
    )


# Create the Gradio interface

# creates a Gradio interface
with gr.Blocks() as demo:

    # displays the title
    gr.Markdown("# Travel Money Helper ✈️💰")

    # displays the description
    gr.Markdown(
        "Enter your travel details to start planning your travel budget."
    )

    # creates a text box where the user enters their destination
    destination = gr.Textbox(
        label="Destination",
        placeholder="e.g. Japan"
    )

    # creates a number input for the length of the trip
    days = gr.Number(
        label="Number of travel days",
        precision=0
    )

    # creates a number input for the user's available budget
    available_budget = gr.Number(
        label="Available budget (AUD $)",
        minimum=0.01
    )

    # ask whether to use the CSV cost or enter their own cost
    visa_choice = gr.Dropdown(
        choices=["Y", "N"],
        value="N",
        label="Enter your own visa cost? (Y/N)"
    )
    user_visa_cost = gr.Number(
        label="Your visa cost (AUD $)", value=None
    )

    flight_choice = gr.Dropdown(
        choices=["Y", "N"],
        value="N",
        label="Enter your own flight cost? (Y/N)"
    )
    user_flight_cost = gr.Number(
        label="Your flight cost (AUD $)", value=None
    )

    accommodation_choice = gr.Dropdown(
        choices=["Y", "N"],
        value="N",
        label="Enter your own accommodation cost? (Y/N)"
    )
    user_accommodation_cost = gr.Number(
        label="Your accommodation cost per day (AUD $)",
        value=None
    )

    meals_choice = gr.Dropdown(
        choices=["Y", "N"],
        value="N",
        label="Enter your own meals cost? (Y/N)"
    )
    user_meals_cost = gr.Number(
        label="Your meals cost per day (AUD $)",
        value=None
    )

    insurance_choice = gr.Dropdown(
        choices=["Y", "N"],
        value="N",
        label="Enter your own travel insurance cost? (Y/N)"
    )
    user_travel_insurance_cost = gr.Number(
        label="Your travel insurance cost (AUD $)",
        value=None
    )

    transport_choice = gr.Dropdown(
        choices=["Y", "N"],
        value="N",
        label="Enter your own transport cost? (Y/N)"
    )
    user_transport_cost = gr.Number(
        label="Your transport cost per day (AUD $)",
        value=None
    )

    emergency_choice = gr.Dropdown(
        choices=["Y", "N"],
        value="N",
        label="Enter your own emergency money? (Y/N)"
    )
    user_emergency_money = gr.Number(
        label="Your emergency money (AUD $)",
        value=None
    )

    # creates a button to submit the travel details
    calculate = gr.Button("Submit Travel Details")

    # creates a text box to display the result
    result = gr.Textbox(label="Your Travel Details")

    # connects the button to the processing function
    calculate.click(
        fn=get_travel_details,
        inputs=[
            destination, days, available_budget,
            visa_choice, user_visa_cost,
            flight_choice, user_flight_cost,
            accommodation_choice, user_accommodation_cost,
            meals_choice, user_meals_cost,
            insurance_choice, user_travel_insurance_cost,
            transport_choice, user_transport_cost,
            emergency_choice, user_emergency_money
        ],
        outputs=result
    )

# launches the Gradio interface
demo.launch()
```
"

Solution:

<img width="662" height="691" alt="image" src="https://github.com/user-attachments/assets/3313e1d1-8f97-4eab-a20b-9338fa0d6dd9" />
<img width="684" height="614" alt="image" src="https://github.com/user-attachments/assets/23ed592f-e767-4d0a-a172-33a73b2da4a1" />
<img width="672" height="309" alt="image" src="https://github.com/user-attachments/assets/7ff1c3ef-c884-4db0-874f-cf53300cb75f" />

What I added:
I added the code to find the matching destination before checking whether it existed in the CSV file, because it is need to search for the user's destination in the CSV file and store the result in the row variable before using row.empty.

##Entry 7 - Testing 

I tested my Travel Money Helper to check whether the program works correctly, using Python assert statements which help to check whether the results matched the expected outputs.
First, I tested the travel cost calculation.
Second,  I tested whether an empty destination is rejected.
Third, I tested whether the function rejects a zero travel day.
Fourth, I tested what happened when the user chooses Y, but leaves the flight cost empty.
Fifth, I tested whether the function rejects a negative flight cost.
Sixth, I tested the destination that is not in the CSV file.
Seventh, I tested whether choosing Y replaces the CSV cost with the user's own cost.
Eigth, I tested program correctly displays a budget shortfall, when estimated travel cost is higher than the available budget.
Additionally, I also tested whether the Gemini gives budgeting suggestions.
Lastly, I tested whether the Gradio is connected to Gemini to give budget suggestion.

**Problem faced**

1.I got an AssetionError when testing whether the Gradio is connected to Gemini for budgeting suggestion. When I used the Gradio interface, it only stated the result of destination, number of days, cost source, estimated total cost, available budget, and the money remaining. This shows that my Gradio is not connected to my Gemini AI for giving budgeting suggestion.

AI Prompt used: "How can I fix the error when testing whether my Gradio is connected to Gemini AI for budgeting suggestions? My Gradio interface only displays the travel budget calculation but does not show the Gemini AI suggestions. Can you explain to me what I need to change in my code and why, in a simple and easy-to-understand way?"

Soluion:

<img width="757" height="686" alt="image" src="https://github.com/user-attachments/assets/1682f262-cde5-4d42-9ec6-d799785c8f94" />
<img width="752" height="697" alt="image" src="https://github.com/user-attachments/assets/72dfc53f-a34c-4f6f-8245-42710fac5d6a" />
<img width="657" height="780" alt="image" src="https://github.com/user-attachments/assets/046d2456-7756-4d7a-9872-1940338123ed" />
<img width="696" height="521" alt="image" src="https://github.com/user-attachments/assets/100c857c-3b1e-4276-82b1-e5d755be10fe" />
<img width="663" height="642" alt="image" src="https://github.com/user-attachments/assets/16432173-4bed-42fe-a20f-220b9617c806" />

What I changed:
I added the Gemini function call, get_budget_suggestions(), after calculating the total travel cost and before the final return statement in my processing function. I also updated my return statement to include the Gemini Budgeting Suggestions. After updating my code, I ran my code again and tested the function using an example of a user travelling to Japan for 5 days with an available budget of $3000. This test passed, and my Gradio interface output included both the travel budget calculation and the Gemini budgeting suggestions.


