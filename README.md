Stock_Prices={"APL":180,"TSLA":250,"GOOGL":150,"MSFT":420}

def main():
    print("_ _ _ STOCK PORTFOLIO TRACKER _ _ _")
    print(f"AVAILABLE STOCKS IN SYSTEM: {list(Stock_Prices.keys())}\n")

    portfolio = {}

    while True:
        stock=input("Enter stock symbol (or type 'done' to finish): ").strip().upper()
        if stock=='DONE':
            print("Alright! Here is your Portfolio Summary!")
            break
        if stock not in Stock_Prices:
            print(f"Stock '{stock}' not found! Please choose from: {list(Stock_Prices.keys())}")
            continue
        try:
            quantity=int(input(f"Enter quantity for {stock}: "))
            if quantity<0:
                print("Quantity cannot be negative!")
                continue
        except ValueError:
            print("Invalid input! Please enter a whole number for quantity!")
            continue
        portfolio[stock]=portfolio.get(stock,0)+quantity

    print("\n" + "=" * 10 + "YOUR PORTFOLIO SUMMARY" + "=" * 10)
    total_investment=0

    if not portfolio:
        print("Your portfolio is empty!")
        return

    for stock_item,qty in portfolio.items():
        price=Stock_Prices[stock_item]
        item_total=price*qty
        total_investment+=item_total
        print(f"{stock_item}:{qty} shares @ ${price} = ${item_total}")

    print("_" * 44)
    print(f"Total Investment Value: ${total_investment}")
    print("=" * 44)

    try:
        import csv
        with open("portfolio_summary.csv","w", newline="") as file:
            writer=csv.writer(file)
            writer.writerow(["Stock","Quantity","Price","Total Value"])

            for stock_item,qty in portfolio.items():
                price=Stock_Prices[stock_item]
                item_total=price*qty
                writer.writerow([stock_item,qty,price,item_total])

        print("\n PORTFOLIO SUCCESSFULLY SAVED TO 'portfolio_summary.csv'!")
    except Exception as e:
        print(f"An error occured while saving the file: {e}")
main()


            


                



    # Python-Task
Created a stock portfolio using python
