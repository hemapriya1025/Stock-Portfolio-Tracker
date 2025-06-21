# Stock-Portfolio-Tracker
A Stock Portfolio Tracker is a simple tool that calculates and displays the total investment value based on predefined stock prices and user-input stock quantities.
# Step 1: Hardcoded stock prices
stock_prices = {
    "AAPL": 180,
    "TSLA": 250,
    "GOOG": 135,
    "AMZN": 125,
    "MSFT": 310
}

portfolio = {}  # To store user-entered stocks and quantities

print("📈 Welcome to the Stock Portfolio Tracker")
print("Available stocks:", ', '.join(stock_prices.keys()))
print("Enter 'done' when you're finished.\n")

# Step 2: User input loop
while True:
    stock_name = input("Enter stock symbol (e.g., AAPL): ").upper()
    
    if stock_name == 'DONE':
        break
    
    if stock_name not in stock_prices:
        print("❌ Stock not found. Please enter one from the list.")
        continue
    
    try:
        quantity = int(input(f"Enter quantity of {stock_name} shares: "))
    except ValueError:
        print("⚠️ Please enter a valid number.\n")
        continue

    portfolio[stock_name] = portfolio.get(stock_name, 0) + quantity
    print("✅ Stock added.\n")

# Step 3: Calculate total investment
total_investment = 0
print("\n📊 Your Portfolio Summary:")
for stock, qty in portfolio.items():
    value = stock_prices[stock] * qty
    total_investment += value
    print(f"{stock}: {qty} shares × ${stock_prices[stock]} = ${value}")

print(f"\n💰 Total Investment Value: ${total_investment}")

# Step 4 (Optional): Save to file
save = input("Would you like to save this to a file? (yes/no): ").lower()
if save == 'yes':
    with open("portfolio_summary.txt", "w") as file:
        file.write("Stock Portfolio Summary:\n")
        for stock, qty in portfolio.items():
            value = stock_prices[stock] * qty
            file.write(f"{stock}: {qty} shares × ${stock_prices[stock]} = ${value}\n")
        file.write(f"\nTotal Investment Value: ${total_investment}")
    print("✅ Summary saved to 'portfolio_summary.txt'")
