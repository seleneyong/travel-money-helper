# Travel-money-helper
A finance assistant that helps travellers plan how much money they should prepare for a trip. It calculates user personalised travel costs and compares the total cost with the user's available budget.

This program calculates the total costs by breaking it into visa, flights, accommodation, meals, travel insurance, transport fee, and emergency money. It uses a CSV file containing example travel costs for several different destinations. However, users can also enter their own costs and destination to personalise their travel budget.

The project also uses the Gemini API to provide budgeting suggestions based on the user's travel costs and available budget.

## Main features
1. Destination and day selection: users chooses destination and number of days(input).
2. CSV reference costs: program reads reference costs from travel costs.csv file. If destination is found, users can choose "Y/N" to decide whether they want to enter their own costs, if user entered N(no) the program uses the estimated cost from the CSV file(input).
3. Personalised costs: if user entered Y(yes) the program will asks them to enter their own costs. And if destination not found, program will ask users to enter their own destination and costs for all categories.
4. Budget checking: the Budget checking: The program compares the estimated total with the user's available budget and shows the remaining money or budget shortfall.
5. AI budgeting suggestions: Gemini AI gives budgeting suggestion based on the calculated travel costs and available budget.
6. Input validation: The program checks user inputs and handles invalid entries.

## Sample Input and Output
*Example input*

Destination: Thailand

Number of days: 6

Available budget: AUD $2000

Travel costs: example costs from the CSV file

*Example output*

The program will displays the estimated costs for the selected destination, the total estimated travel cost, and whether the available budget is sufficient. It also displays the remaining money or budget shortfall and provides AI budgeting suggestions.

## How to run the project
1. Open Travel_Money_Helper.ipynb in Google Colab.
2. Upload Travel Costs.csv to the Colab session.
3. Set up the Gemini API key in Colab Secrets using the name GEMINI_API_KEY.
4. Run the notebook cells in order to install the required libraries, load the CSV file, define the functions, run the tests and launch the Gradio interface.
5. Enter the travel details in the interface and submit them to view the estimated budget and budgeting suggestions.

## AI Assistance
I used AI assistance to help me understand Python errors, improve input validation, debug my code and integrate the Gemini API and Gradio interface. I recorded my prompts, the solutions I considered, and the changes I made in the Developer Diary.

I tested and reviewed the code as I developed the project.
