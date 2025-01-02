# Entrees
This program shows which entrees are the most popular, how much each entree earned over the night, as well as the grand total of all entrees added together. Anyone wanting to know how much each of their entrees are selling in one day, as well as get a total earned overall over a day. Write a program that tracks how much of each entree is sold, what the total is earned from each individual entree, as well as the total earned from ALL entrees added together. The entrees on the menu are 1) spaghetti with meatballs ($10.00), 2) rib eye steak and potatoes ($25.00) 3) cobb salad ($12.00), 4)Red Snapper in butter sauce ($30.00) and 5) Margherita Pizza ($15.95). 


menu = {
    "Spaghetti with Meatballs": {"price": 10.00, "daily_sales": 0, "total_sales": 0.00},
    "Rib Eye Steak and Potatoes": {"price": 25.00, "daily_sales": 0, "total_sales": 0.00},
    "Cobb Salad": {"price": 12.00, "daily_sales": 0, "total_sales": 0.00},
    "Red Snapper in Butter Sauce": {"price": 30.00, "daily_sales": 0, "total_sales": 0.00},
    "Margherita Pizza": {"price": 15.95, "daily_sales": 0, "total_sales": 0.00}
}

def process_order(entree, quantity):
    """
    Processes an order for a given entree and quantity.

    Args:
        entree: The name of the entree.
        quantity: The number of orders for the entree.
    """
    if entree in menu:
        menu[entree]["daily_sales"] += quantity
        menu[entree]["total_sales"] += menu[entree]["price"] * quantity
    else:
        print(f"Invalid entree: {entree}")

def calculate_daily_sales():
    """
    Calculates and displays the daily sales for each entree and the total daily sales.
    """
    daily_total = 0.00
    print("\nDaily Sales Report:")
    for entree, info in menu.items():
        daily_total += info["total_sales"]
        print(f"{entree}:")
        print(f" - Quantity Sold: {info['daily_sales']}")
        print(f" - Total Earned: ${info['total_sales']:.2f}")
        print("-" * 20)
    print(f"Total Daily Sales: ${daily_total:.2f}")
    return daily_total

def reset_daily_sales():
    """
    Resets the daily sales count for each entree.
    """
    for entree in menu:
        menu[entree]["daily_sales"] = 0
        menu[entree]["total_sales"] = 0.00

# Get sales data for each day of the week
daily_sales_totals = []

for day in ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]:
    print(f"\n** {day} **")
    for entree in menu:
        while True:
            try:
                quantity_sold = int(input(f"Enter quantity sold for {entree}: "))
                break 
            except ValueError:
                print("Invalid input. Please enter a whole number.")
        process_order(entree, quantity_sold)
    daily_sales = calculate_daily_sales()
    daily_sales_totals.append(daily_sales)
    reset_daily_sales()

# Calculate and display total weekly sales
weekly_sales = sum(daily_sales_totals)
print(f"\nTotal Weekly Sales: ${weekly_sales:.2f}")
