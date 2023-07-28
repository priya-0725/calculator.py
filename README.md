# calculator.py
Programming Contest Submission
import tkinter as tk

def on_button_click(event):
    current_text = display_var.get()
    button_text = event.widget.cget("text")
    
    if button_text == "=":
        try:
            result = eval(current_text)
            display_var.set(result)
        except Exception as e:
            display_var.set("Error")
    elif button_text == "C":
        display_var.set("")
    else:
        display_var.set(current_text + button_text)

# Create the main window
window = tk.Tk()
window.title("Basic Calculator")

# Variable to store display text
display_var = tk.StringVar()

# Display area
display = tk.Entry(window, textvariable=display_var, font=("Arial", 20), bd=10, justify="right")
display.grid(row=0, column=0, columnspan=4)

# Buttons
buttons = [
    "7", "8", "9", "/",
    "4", "5", "6", "*",
    "1", "2", "3", "-",
    "0", ".", "=", "+",
    "C",
]

row = 1
col = 0
for button_text in buttons:
    button = tk.Button(window, text=button_text, font=("Arial", 20), padx=20, pady=20)
    button.grid(row=row, column=col, sticky="nsew")
    button.bind("<Button-1>", on_button_click)
    col += 1
    if col > 3:
        col = 0
        row += 1

# Make the buttons expand to fill the grid cells
for i in range(5):
    window.grid_rowconfigure(i, weight=1)
    window.grid_columnconfigure(i, weight=1)

# Run the application
window.mainloop()
