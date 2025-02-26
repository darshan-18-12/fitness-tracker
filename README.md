# fitness-tracker
import json
import datetime
import matplotlib.pyplot as plt

# File to store workout data
DATA_FILE = "fitness_data.json"

def load_data():
    try:
        with open(DATA_FILE, "r") as file:
            return json.load(file)
    except FileNotFoundError:
        return []

def save_data(data):
    with open(DATA_FILE, "w") as file:
        json.dump(data, file, indent=4)

def log_workout():
    date = input("Enter the date (YYYY-MM-DD): ")
    exercise = input("Enter exercise name: ")
    duration = float(input("Enter duration in minutes: "))
    calories = float(input("Enter calories burned: "))
    
    entry = {
        "date": date,
        "exercise": exercise,
        "duration": duration,
        "calories": calories
    }
    
    data = load_data()
    data.append(entry)
    save_data(data)
    print("Workout logged successfully!")

def view_progress():
    data = load_data()
    if not data:
        print("No data available.")
        return
    
    print("\nWorkout History:")
    for entry in data:
        print(f"{entry['date']} - {entry['exercise']} - {entry['duration']} min - {entry['calories']} cal")

def plot_progress():
    data = load_data()
    if not data:
        print("No data to visualize.")
        return
    
    dates = [entry['date'] for entry in data]
    calories = [entry['calories'] for entry in data]
    
    plt.figure(figsize=(10,5))
    plt.plot(dates, calories, marker='o', linestyle='-', color='b')
    plt.xlabel("Date")
    plt.ylabel("Calories Burned")
    plt.title("Calorie Burn Progress Over Time")
    plt.xticks(rotation=45)
    plt.grid()
    plt.show()

def main():
    while True:
        print("\nPersonal Fitness Tracker")
        print("1. Log Workout")
        print("2. View Progress")
        print("3. Plot Progress")
        print("4. Exit")
        
        choice = input("Choose an option: ")
        
        if choice == "1":
            log_workout()
        elif choice == "2":
            view_progress()
        elif choice == "3":
            plot_progress()
        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()


This script allows users to log workouts, track progress, and visualize calorie burn over time using Matplotlib. Let me know if you want additional features like goal setting or workout categories!
