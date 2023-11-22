

User
create python app that with a GUI that manages a SQL database 
ChatGPT
Absolutely, creating a Python app with a GUI that manages a SQL database is a fantastic project! To achieve this, you'll need a few key libraries:

Tkinter for the GUI elements.
SQLite3 for handling the SQL database operations.
Python's sqlite3 module to interact with SQLite databases.
Here's a simple example to get you started:

python
Copy code
import tkinter as tk
import sqlite3

# Function to create a new table in the database
def create_table():
    connection = sqlite3.connect('database.db')
    cursor = connection.cursor()
    cursor.execute('''CREATE TABLE IF NOT EXISTS Users (
                        id INTEGER PRIMARY KEY,
                        name TEXT,
                        age INTEGER)''')
    connection.commit()
    connection.close()

# Function to insert data into the database
def insert_data(name, age):
    connection = sqlite3.connect('database.db')
    cursor = connection.cursor()
    cursor.execute("INSERT INTO Users (name, age) VALUES (?, ?)", (name, age))
    connection.commit()
    connection.close()

# Function to view data from the database
def view_data():
    connection = sqlite3.connect('database.db')
    cursor = connection.cursor()
    cursor.execute("SELECT * FROM Users")
    rows = cursor.fetchall()
    connection.close()
    return rows

# GUI setup
def main():
    root = tk.Tk()
    root.title("Database Manager")

    # Create table button
    create_table_btn = tk.Button(root, text="Create Table", command=create_table)
    create_table_btn.pack()

    # Entry fields
    name_label = tk.Label(root, text="Name:")
    name_label.pack()
    name_entry = tk.Entry(root)
    name_entry.pack()

    age_label = tk.Label(root, text="Age:")
    age_label.pack()
    age_entry = tk.Entry(root)
    age_entry.pack()

    # Insert data button
    def insert_data_command():
        name = name_entry.get()
        age = age_entry.get()
        insert_data(name, age)

    insert_data_btn = tk.Button(root, text="Insert Data", command=insert_data_command)
    insert_data_btn.pack()

    # View data button
    def view_data_command():
        data = view_data()
        for row in data:
            print(row)  # Replace with your display logic

    view_data_btn = tk.Button(root, text="View Data", command=view_data_command)
    view_data_btn.pack()

    root.mainloop()

if __name__ == "__main__":
    main()
This code provides a basic framework for a GUI that allows you to create a table, insert data (name and age), and view the data from the SQLite database. It's important to enhance this with error handling, better UI design, and security measures for production-level applications.

Remember to install tkinter if you haven't already, as it's usually included in Python's standard library, and sqlite3 is included by default as well.
