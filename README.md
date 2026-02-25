import tkinter as tk
from tkinter import messagebox
import random

# Create window
root = tk.Tk()
root.title("Smart Skill Partner Finder")
root.geometry("500x600")
root.configure(bg="#667eea")

# Variables
name_var = tk.StringVar()
skill_var = tk.StringVar()
level_var = tk.StringVar(value="Beginner")
time_var = tk.StringVar()
goal_var = tk.StringVar()

# Title
title = tk.Label(root, text="Create Your Smart Profile",
                 font=("Arial", 16, "bold"), bg="#667eea", fg="white")
title.pack(pady=10)

# Input Fields
def create_label(text):
    return tk.Label(root, text=text, bg="#667eea", fg="white", font=("Arial", 10))

create_label("Name").pack()
tk.Entry(root, textvariable=name_var).pack(pady=5)

create_label("Skill").pack()
tk.Entry(root, textvariable=skill_var).pack(pady=5)

create_label("Skill Level").pack()
tk.OptionMenu(root, level_var, "Beginner", "Intermediate", "Advanced").pack(pady=5)

create_label("Available Time").pack()
tk.Entry(root, textvariable=time_var).pack(pady=5)

create_label("Learning Goal").pack()
tk.Entry(root, textvariable=goal_var).pack(pady=5)

# Profile Display Area
profile_frame = tk.Frame(root, bg="white")
profile_frame.pack(pady=15, fill="both", expand=True)

def create_profile():
    name = name_var.get()
    skill = skill_var.get()
    level = level_var.get()
    time = time_var.get()
    goal = goal_var.get()

    if not name or not skill or not time or not goal:
        messagebox.showerror("Error", "Please fill all fields!")
        return

    score = random.randint(80, 100)

    for widget in profile_frame.winfo_children():
        widget.destroy()

    tk.Label(profile_frame, text=f"Name: {name}", bg="white").pack()
    tk.Label(profile_frame, text=f"Skill: {skill}", bg="white").pack()
    tk.Label(profile_frame, text=f"Level: {level}", bg="white").pack()
    tk.Label(profile_frame, text=f"Time: {time}", bg="white").pack()
    tk.Label(profile_frame, text=f"Goal: {goal}", bg="white").pack()
    tk.Label(profile_frame, text=f"Compatibility Score: {score}%", 
             fg="green", bg="white", font=("Arial", 12, "bold")).pack(pady=5)

    find_button = tk.Button(profile_frame, text="Find Matching Partner",
                            command=find_match, bg="#764ba2", fg="white")
    find_button.pack(pady=10)

def find_match():
    level = level_var.get()

    if level == "Beginner":
        partner = ("Sneha Patil", "Python Basics", "4 PM – 5 PM", 92)
    elif level == "Intermediate":
        partner = ("Rahul Sharma", "Python OOP", "5 PM – 6 PM", 94)
    else:
        partner = ("Aman Verma", "Advanced Python & AI", "7 PM – 8 PM", 96)

    tk.Label(profile_frame, text="🎉 Match Found!", fg="green",
             bg="white", font=("Arial", 14, "bold")).pack(pady=5)

    tk.Label(profile_frame, text=f"Partner: {partner[0]}", bg="white").pack()
    tk.Label(profile_frame, text=f"Skill: {partner[1]}", bg="white").pack()
    tk.Label(profile_frame, text=f"Common Time: {partner[2]}", bg="white").pack()
    tk.Label(profile_frame, text=f"Compatibility: {partner[3]}%", 
             fg="green", bg="white").pack(pady=5)

    tk.Button(profile_frame, text="Send Chat Request 💬",
              command=lambda: messagebox.showinfo("Success",
              "Chat request sent successfully!"),
              bg="#667eea", fg="white").pack(pady=5)

# Button
tk.Button(root, text="Generate Profile",
          command=create_profile,
          bg="#764ba2", fg="white",
          font=("Arial", 11, "bold")).pack(pady=10)

root.mainloop()
