import tkinter as tk

# Menu dictionary
menu = {
    'pizza': 500,
    'burger': 120,
    'tea': 50,
    'paratah': 40,
    'pasta': 120
}

# Function to add item to order
def add_item(event=None):
    global order_total
    item = entry.get().lower()
    entry.delete(0, tk.END)
    
    if item in menu:
        order_total += menu[item]
        output_label.config(text=f"{item.capitalize()} added! Current total: Rs {order_total}")
    else:
        output_label.config(text=f"Sorry, {item} is not available!")

# Main window
root = tk.Tk()
root.title("Python Restaurant")
root.geometry("400x350")
root.config(bg="#f0f0f0")
order_total = 0

# Title
title_label = tk.Label(root, text="WELCOME TO PYTHON RESTAURANT", font=("Arial", 14, "bold"),fg="blue")
title_label.pack(pady=10)

# Menu display
menu_text = "\n".join([f"{item.capitalize()}: Rs {price}" for item, price in menu.items()])
menu_label = tk.Label(root, text=menu_text, font=("Arial", 12))
menu_label.pack(pady=10)

# Entry field
entry_label = tk.Label(root, text="Enter your item:", font=("Arial", 12))
entry_label.pack()
entry = tk.Entry(root, font=("Arial", 12))
entry.pack(pady=5)
entry.focus()

# Bind Enter key
entry.bind("<Return>", add_item)

# Output label
output_label = tk.Label(root, text="", font=("Arial", 12), fg="blue")
output_label.pack(pady=10)

# Total amount label
total_label = tk.Label(root, text="Total: Rs 0", font=("Arial", 14, "bold"), fg="green")
total_label.pack(pady=10)

# Update total continuously
def update_total():
    total_label.config(text=f"Total: Rs {order_total}")
    root.after(500, update_total)

update_total()

root.mainloop()
