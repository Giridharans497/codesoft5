# codesoft5

import tkinter as tk
from tkinter import messagebox

class Contact:
    def __init__(self, name, phone, email):
        self.name = name
        self.phone = phone
        self.email = email

class ContactBookApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Giridharan Contact Book")

        self.contacts = []

        self.label_name = tk.Label(root, text="Person Name:")
        self.label_phone = tk.Label(root, text="Mobile Number:")
        self.label_email = tk.Label(root, text="Email Address:")

        self.entry_name = tk.Entry(root)
        self.entry_phone = tk.Entry(root)
        self.entry_email = tk.Entry(root)
        

        self.button_add = tk.Button(root, text="Additional Truecaller Contact", command=self.add_contact)
        self.button_view = tk.Button(root, text="View Access Contacts", command=self.view_contacts)
        self.button_delete = tk.Button(root, text="Delete Person Contact", command=self.delete_contact)

        self.label_name.grid(row=0, column=0, padx=15, pady=10, sticky=tk.E)
        self.label_phone.grid(row=1, column=0, padx=15, pady=10, sticky=tk.E)
        self.label_email.grid(row=2, column=0, padx=15, pady=10, sticky=tk.E)

        self.entry_name.grid(row=0, column=1, padx=20, pady=15)
        self.entry_phone.grid(row=1, column=1, padx=20, pady=15)
        self.entry_email.grid(row=2, column=1, padx=20, pady=15)

        self.button_add.grid(row=3, column=0, columnspan=2, pady=10)
        self.button_view.grid(row=4, column=0, columnspan=2, pady=10)
        self.button_delete.grid(row=5, column=0, columnspan=2, pady=10)

    def add_contact(self):
        name = self.entry_name.get()
        phone = self.entry_phone.get()
        email = self.entry_email.get()

        if name and phone and email:
            new_contact = Contact(name, phone, email)
            self.contacts.append(new_contact)
            messagebox.showinfo("Success", f"Contact {name} added successfully!")
        else:
            messagebox.showerror("Error", "Please fill in all fields.")

        self.clear_entries()

    def view_contacts(self):
        if not self.contacts:
            messagebox.showinfo("Info", "Contact book is empty.")
        else:
            contact_list = "\n".join([f"Name: {contact.name}, Phone: {contact.phone}, Email: {contact.email}" for contact in self.contacts])
            messagebox.showinfo("Contacts", contact_list)

    def delete_contact(self):
        name_to_delete = self.entry_name.get()
        if not name_to_delete:
            messagebox.showerror("Error", "Please enter the name to delete.")
            return

        for contact in self.contacts:
            if contact.name.lower() == name_to_delete.lower():
                self.contacts.remove(contact)
                messagebox.showinfo("Success", f"Contact {name_to_delete} deleted successfully!")
                self.clear_entries()
                return

        messagebox.showerror("Error", f"Contact with name '{name_to_delete}' not found.")

    def clear_entries(self):
        self.entry_name.delete(0, tk.END)
        self.entry_phone.delete(0, tk.END)
        self.entry_email.delete(0, tk.END)

def main():
    root = tk.Tk()
    app = ContactBookApp(root)
    root.mainloop()

if __name__ == "__main__":
    main()