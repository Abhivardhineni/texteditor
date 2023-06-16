# texteditor
import tkinter as tk
from tkinter import filedialog

class TextEditor:
    def __init__(self, root):
        self.root = root
        self.root.title("Text Editor")

        # Create Text widget
        self.text_widget = tk.Text(root)
        self.text_widget.pack(fill=tk.BOTH, expand=True)

        # Create Menu
        self.menu_bar = tk.Menu(root)
        self.file_menu = tk.Menu(self.menu_bar, tearoff=0)
        self.file_menu.add_command(label="Open", command=self.open_file)
        self.file_menu.add_command(label="Save", command=self.save_file)
        self.file_menu.add_separator()
        self.file_menu.add_command(label="Exit", command=root.quit)
        self.menu_bar.add_cascade(label="File", menu=self.file_menu)

        self.root.config(menu=self.menu_bar)

    def open_file(self):
        file_path = filedialog.askopenfilename(filetypes=[("Text Files", "*.txt")])
        if file_path:
            with open(file_path, "r") as file:
                content = file.read()
                self.text_widget.delete("1.0", tk.END)
                self.text_widget.insert(tk.END, content)

    def save_file(self):
        file_path = filedialog.asksaveasfilename(defaultextension=".txt", filetypes=[("Text Files", "*.txt")])
        if file_path:
            content = self.text_widget.get("1.0", tk.END)
            with open(file_path, "w") as file:
                file.write(content)

if __name__ == "__main__":
    # Create the Tkinter root window
    root = tk.Tk()

    # Create an instance of the TextEditor class
    text_editor = TextEditor(root)

    # Start the Tkinter event loop
    root.mainloop()
