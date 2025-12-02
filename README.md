import pyodbc
print("pyodbc is installed and working.")
conn=pyodbc.connect(
    "DRIVER={ODBC Driver 18 for SQL Server};"
    "SERVER=DESKTOP-FPQ15DO;"
    "Database=master;"
    "Trusted_Connection=yes;"
    "Encrypt=no;"
)
cursor = conn.cursor()
print("Connected to SQL Server Successully.!")

conn.commit()
print("Table 'students' checked successfully")


import tkinter as tk
from tkinter import ttk   # for table

students = []  # simple in-memory database


def refresh_table():
    """Refreshes the table with the latest student data."""
    for row in table.get_children():
        table.delete(row)

    for s in students:
        table.insert("", "end", values=(s["name"], s["age"], s["grade"]))


def add_student():
    name = name_entry.get()
    age = age_entry.get()
    grade = grade_entry.get()

    if name == "" or age == "" or grade == "":
        status_label.config(text="❌ All fields required!")
        return

    students.append({"name": name, "age": age, "grade": grade})
    status_label.config(text=f"✔ Student '{name}' added!")

    clear_fields()
    refresh_table()
