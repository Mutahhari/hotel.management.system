# hotel_system.py

import random
import time

def show_flowchart():
    print("\n========== HOTEL SYSTEM FLOW ==========\n")
    print("START")
    print("  ↓")
    print("Show Flow Chart")
    print("  ↓")
    print("Do you have a Vehicle?")
    print("  ↓")
    print("Select Customer Type")
    print("  ↓")
    print("Select Stay Type")
    print("  ↓")
    print("Swimming Pool (Night / Full Day Only)")
    print("  ↓")
    print("Food Ordering")
    print("  ↓")
    print("Room / Table Assignment")
    print("  ↓")
    print("Payment Method")
    print("  ↓")
    print("Feedback")
    print("  ↓")
    print("Generate Full Receipt")
    print("  ↓")
    print("END")
    print("\n======================================\n")
    time.sleep(2)


def run_hotel_system():

    menus = {
        "Breakfast": {1: ("Egg & Bread", 200), 2: ("Omelette", 250), 3: ("Tea", 100)},
        "Lunch": {1: ("Biryani", 350), 2: ("Chicken Karahi", 800), 3: ("Cold Drink", 120)},
        "Dinner": {1: ("BBQ", 900), 2: ("Handi", 850), 3: ("Green Tea", 150)}
    }

    discounts = {"Family": 0.10, "Friends": 0.05, "Couple": 0.15}

    room_prices = {
        "Normal": {"Furnished": 3000, "Luxury": 5000},
        "VIP": {"Furnished": 6000, "Luxury": 9000}
    }

    parking_fees = {"Bike": 50, "Car": 150, "SUV": 250}
    pool_fees = {"Family": 500, "Friends": 400, "Couple": 300}

    items = []
    subtotal = 0

    # -------- FLOW CHART --------
    show_flowchart()

    # -------- VEHICLE --------
    print("Do you have a vehicle?")
    print("1. No\n2. Yes")
    if input("Select: ") == "2":
        print("1. Bike\n2. Car\n3. SUV")
        vt = input("Select: ")
        vehicle = "Bike" if vt == "1" else "Car" if vt == "2" else "SUV"
        subtotal += parking_fees[vehicle]
        items.append(f"{vehicle} Parking")

    # -------- CUSTOMER --------
    while True:
        print("\nCustomer Type:")
        print("1. Family\n2. Friends\n3. Couple")
        c = input("Select: ")
        if c == "1": customer = "Family"; break
        if c == "2": customer = "Friends"; break
        if c == "3": customer = "Couple"; break

    # -------- STAY --------
    while True:
        print("\nStay Type:")
        print("1. Short Stay")
        print("2. Night Stay")
        print("3. Full Day Stay")
        st = input("Select: ")
        if st in ["1", "2", "3"]: break

    stay_name = "Short Stay" if st == "1" else "Night Stay" if st == "2" else "Full Day Stay"

    # -------- SWIMMING (ONLY NIGHT / FULL DAY) --------
    if st in ["2", "3"]:
        print("\nSwimming Pool Access?")
        print("1. Yes\n2. No")
        if input("Select: ") == "1":
            subtotal += pool_fees[customer]
            items.append("Swimming Pool")

    # -------- FOOD --------
    def order_food():
        nonlocal subtotal
        while True:
            print("\nMeal Type:")
            print("1. Breakfast\n2. Lunch\n3. Dinner\n0. Finish")
            m = input("Select: ")
            if m == "0":
                break
            meal = menus[{"1": "Breakfast", "2": "Lunch", "3": "Dinner"}[m]]
            for i in meal:
                print(i, meal[i][0], "- Rs", meal[i][1])
            ch = input("Item: ")
            if ch.isdigit() and int(ch) in meal:
                name, price = meal[int(ch)]
                items.append(name)
                subtotal += price

    order_food()

    # -------- ROOM --------
    if st in ["2", "3"]:
        print("\nRoom Category:")
        print("1. Normal\n2. VIP")
        room_cat = "Normal" if input("Select: ") == "1" else "VIP"

        print("Room Type:")
        print("1. Furnished\n2. Luxury")
        room_type = "Furnished" if input("Select: ") == "1" else "Luxury"

        room_cost = room_prices[room_cat][room_type]
        subtotal += room_cost
        items.append(f"{room_cat} {room_type} Room")

    # -------- PAYMENT --------
    print("\nPayment Method:")
    print("1. Cash\n2. Online")
    payment = "Cash" if input("Select: ") == "1" else "Online"

    # -------- FEEDBACK --------
    feedback = input("\nPlease give your feedback: ")

    # -------- BILL --------
    discount = subtotal * discounts[customer]
    total = subtotal - discount
    booking_id = random.randint(1000, 9999)

    print("\n========== FULL RECEIPT ==========")
    print("Booking ID:", booking_id)
    print("Customer Type:", customer)
    print("Stay Type:", stay_name)
    print("Items:")
    for i in items:
        print(" -", i)
    print("Subtotal: Rs", subtotal)
    print("Discount: Rs", discount)
    print("Total Bill: Rs", total)
    print("Payment Method:", payment)
    print("Feedback:", feedback)
    print("=================================")
    print("Thank you for visiting our hotel ")


# -------- RUN --------
if __name__ == "__main__":
    run_hotel_system()
