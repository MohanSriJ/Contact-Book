import tkinter as tk
from tkinter import messagebox, simpledialog
import csv
import os

# File to save contacts
FILE_NAME = "contacts.csv"

# Contact storage
contacts = {}

# Load contacts from CSV file
def load_contacts():
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r", newline="") as file:
            reader = csv.reader(file)
            for row in reader:
                if len(row) == 4:
                    name, phone, email, address = row
                    contacts[name] = {"phone": phone, "email": email, "address": address}
        view_contacts()

# Save contacts to CSV file
def save_contacts():
    with open(FILE_NAME, "w", newline="") as file:
        writer = csv.writer(file)
        for name, details in contacts.items():
            writer.writerow([name, details["phone"], details["email"], details["address"]])
    messagebox.showinfo("Saved", "Contacts saved successfully! 💾")

# Add a new contact
def add_contact():
    name = name_entry.get().strip()
    phone = phone_entry.get().strip()
    email = email_entry.get().strip()
    address = address_entry.get().strip()

    if name == "" or phone == "":
        messagebox.showwarning("Input Error", "Name and Phone are required!")
        return

    contacts[name] = {"phone": phone, "email": email, "address": address}
    messagebox.showinfo("Success", f"Contact '{name}' added successfully! ✅")
    clear_entries()
    view_contacts()

# Display contacts in the listbox
def view_contacts():
    contact_list.delete(0, tk.END)
    if not contacts:
        contact_list.insert(tk.END, "No contacts saved.")
    else:
        for name, details in contacts.items():
            contact_list.insert(tk.END, f"{name} - {details['phone']}")

# Search contact
def search_contact():
    search_name = simpledialog.askstring("Search Contact", "Enter name or phone:")
    if not search_name:
        return

    contact_list.delete(0, tk.END)
    found = False
    for name, details in contacts.items():
        if search_name.lower() in name.lower() or search_name in details["phone"]:
            contact_list.insert(tk.END, f"{name} - {details['phone']}")
            found = True

    if not found:
        contact_list.insert(tk.END, "No match found.")

# Delete contact
def delete_contact():
    selected = contact_list.curselection()
    if not selected:
        messagebox.showwarning("Select Error", "Select a contact to delete!")
        return

    contact_info = contact_list.get(selected[0])
    name = contact_info.split(" - ")[0]

    if name in contacts:
        del contacts[name]
        messagebox.showinfo("Deleted", f"Contact '{name}' deleted ❌")
        view_contacts()

# Update contact
def update_contact():
    selected = contact_list.curselection()
    if not selected:
        messagebox.showwarning("Select Error", "Select a contact to update!")
        return

    contact_info = contact_list.get(selected[0])
    name = contact_info.split(" - ")[0]

    if name in contacts:
        phone = simpledialog.askstring("Update Contact", f"Enter new phone (current: {contacts[name]['phone']})")
        email = simpledialog.askstring("Update Contact", f"Enter new email (current: {contacts[name]['email']})")
        address = simpledialog.askstring("Update Contact", f"Enter new address (current: {contacts[name]['address']})")

        contacts[name] = {
            "phone": phone if phone else contacts[name]['phone'],
            "email": email if email else contacts[name]['email'],
            "address": address if address else contacts[name]['address']
        }
        messagebox.showinfo("Updated", f"Contact '{name}' updated successfully! 📝")
        view_contacts()

# Clear input fields
def clear_entries():
    name_entry.delete(0, tk.END)
    phone_entry.delete(0, tk.END)
    email_entry.delete(0, tk.END)
    address_entry.delete(0, tk.END)

# Main Window
root = tk.Tk()
root.title("📒 Contact Book")
root.geometry("520x520")
root.config(bg="#1e1e2e")

# Title
title_label = tk.Label(root, text="📒 Contact Book", font=("Arial", 20, "bold"), fg="#f1fa8c", bg="#1e1e2e")
title_label.pack(pady=15)

# Input Fields
frame = tk.Frame(root, bg="#1e1e2e")
frame.pack(pady=10)

tk.Label(frame, text="Name:", font=("Arial", 12), fg="white", bg="#1e1e2e").grid(row=0, column=0, padx=5, pady=5)
name_entry = tk.Entry(frame, font=("Arial", 12), width=25)
name_entry.grid(row=0, column=1)

tk.Label(frame, text="Phone:", font=("Arial", 12), fg="white", bg="#1e1e2e").grid(row=1, column=0, padx=5, pady=5)
phone_entry = tk.Entry(frame, font=("Arial", 12), width=25)
phone_entry.grid(row=1, column=1)

tk.Label(frame, text="Email:", font=("Arial", 12), fg="white", bg="#1e1e2e").grid(row=2, column=0, padx=5, pady=5)
email_entry = tk.Entry(frame, font=("Arial", 12), width=25)
email_entry.grid(row=2, column=1)

tk.Label(frame, text="Address:", font=("Arial", 12), fg="white", bg="#1e1e2e").grid(row=3, column=0, padx=5, pady=5)
address_entry = tk.Entry(frame, font=("Arial", 12), width=25)
address_entry.grid(row=3, column=1)

# Buttons
btn_frame = tk.Frame(root, bg="#1e1e2e")
btn_frame.pack(pady=10)

tk.Button(btn_frame, text="➕ Add", font=("Arial", 12, "bold"), bg="#50fa7b", command=add_contact).grid(row=0, column=0, padx=5)
tk.Button(btn_frame, text="🔍 Search", font=("Arial", 12, "bold"), bg="#8be9fd", command=search_contact).grid(row=0, column=1, padx=5)
tk.Button(btn_frame, text="📝 Update", font=("Arial", 12, "bold"), bg="#ffb86c", command=update_contact).grid(row=0, column=2, padx=5)
tk.Button(btn_frame, text="❌ Delete", font=("Arial", 12, "bold"), bg="#ff5555", command=delete_contact).grid(row=0, column=3, padx=5)

# Save Button
save_btn = tk.Button(root, text="💾 Save Contacts", font=("Arial", 12, "bold"), bg="#6272a4", fg="white", command=save_contacts)
save_btn.pack(pady=10)

# Contact List
contact_list = tk.Listbox(root, font=("Arial", 12), width=50, height=12, bg="#282a36", fg="white", selectbackground="#6272a4")
contact_list.pack(pady=15)

# Footer
footer = tk.Label(root, text="Made with ❤️ in Python", font=("Arial", 11), fg="#ff79c6", bg="#1e1e2e")
footer.pack(side="bottom", pady=10)

# Load contacts on start
load_contacts()

root.mainloop()
