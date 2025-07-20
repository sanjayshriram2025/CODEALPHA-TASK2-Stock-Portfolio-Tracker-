CODEALPHA-TASK2-Stock-Portfolio-Tracker

A Python based command line application to track investments across multiple stocks. Users can input stock names and quantities, and the program calculates total investment using predefined stock prices. It also allows exporting the report to `.txt` or `.csv` format.

Features
Input stock symbols and quantities
Predefined stock price list
Calculates total investment
Export summary to `.txt` or `.csv`
Error handling for invalid inputs
UTF-8 encoding for currency symbols (₹)

Technologies Used
Python 3.10
Standard libraries: `csv`, `input`, `dict`, `file handling`
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Full Code Breakdown & Explanation

1. Import the `csv` Module

python
import csv

Imports Python’s built-in **CSV module** to write `.csv` files.
Required only if the user chooses to save the report in `.csv` format.

2. Define Hardcoded Stock Prices**

python
stock_prices = {
    "AAPL": 180,
    "TSLA": 250,
    "MSFT": 320,
    "GOOGL": 140,
    "INFY": 1500
}


A dictionary of stock symbols with their respective prices (in ruppes).
Used for calculating total investment value: `price × quantity`.

3. Initialize Portfolio & Total Investment

python
portfolio = {}
total_investment = 0


portfolio stores stocks the user selects along with their quantities.
total_investment keeps running total of money invested.

4. Greet the User & Show Available Stocks

python
print(" Welcome to Sanjay Shriram's Stock Portfolio Tracker!")
print("Available stocks:", ', '.join(stock_prices.keys()))

Shows a welcome message and lists all available stock symbols.

5. Collect Stock Entries from User

python
while True:
    stock = input("\nEnter stock symbol (or 'done' to finish): ").upper()
    
    if stock == "DONE":
        break


A  while  loop that runs until user types `done`.
.upper() makes input case-insensitive (`aapl` → `AAPL`).

6. Validate Stock Symbol

python
    if stock not in stock_prices:
        print(" Invalid stock symbol. Try again.")
        continue

 Checks if the stock exists in our dictionary.
 If not, tells the user and restarts the loop.

7. Ask for Quantity (with Error Handling)

python
    try:
        quantity = int(input(f"Enter quantity of {stock}: "))
        if quantity < 0:
            raise ValueError
        portfolio[stock] = quantity
    except ValueError:
        print(" Please enter a valid positive number.")
        continue


Gets the quantity and ensures it’s a positive integer.
If the user types something invalid (e.g. `abc`, `-5`), it catches the error and loops again.

8. Show Investment Summary

python
print("\n Investment Summary:")
for stock, qty in portfolio.items():
    price = stock_prices[stock]
    value = price * qty
    total_investment += value
    print(f"{stock}: {qty} x ₹{price} = ₹{value}")


Loops through all entries in the `portfolio` dictionary.
Multiplies price × quantity.
Adds each to `total_investment`.
Prints a formatted summary line.

9. Print Total Investment

python
print(f"\n Total Investment: {total_investment}")

Shows the final total value of all stock investments.

10. Ask User if They Want to Save the Report

python
save = input("\nDo you want to save this report? (yes/no): ").lower()
 Simple yes/no prompt to proceed to file saving.

11. Prompt Format Type (TXT or CSV)

python
format_choice = input("Save as (txt/csv): ").lower()
Asks the user how they want the report saved.

12. Save to .txt File (with UTF-8 Fix)

python
if format_choice == "txt":
    with open("portfolio_report.txt", "w", encoding="utf-8") as file:
        file.write("Stock Portfolio Report\n")
        ...
Opens a file in write mode (`"w"`) with UTF-8 encoding.
Writes the full summary into a `.txt` file, including:
All stocks with quantities and values
Total investment at the bottom

13. Save to `.csv` File (Spreadsheet Friendly)

python
elif format_choice == "csv":
    with open("portfolio_report.csv", "w", newline="", encoding="utf-8") as file:
        writer = csv.writer(file)
        writer.writerow(["Stock", "Quantity", "Price", "Value"])
        ...
Uses `csv.writer` to save portfolio data in a structured format.
Includes headers and each stock's data row by row.
Adds a total at the end.

14. Handle Invalid Format
python
else:
    print("Invalid format. Report not saved.")

If the user enters something like `doc`, it aborts the save.

 Concepts Used


`dict`Stores stock prices & portfolio entries             
`while` loop Accepts multiple stock inputs                       
`try/except`Handles invalid input (like text instead of number) 
`file handling`Saves reports as `.txt` or `.csv`                   
`csv module`Creates spreadsheet-style report                    
`utf-8` Ensures ₹ symbol works in saved files  
====================================================================================================================================================================================================================


