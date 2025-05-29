import tkinter as tk

class CalculatorApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Simple Calculator")
        self.root.configure(bg="#2c3e50")
        self.expression = ""

        self.entry = tk.Entry(root, font=("Poppins", 30), bg="#2c3e50", fg="white",
                              borderwidth=0, justify="right")
        self.entry.insert(0, "0")
        self.entry.grid(row=0, column=0, columnspan=4, pady=20, padx=10, sticky="nsew")

        buttons = [
            ("AC", 1, 0, "#15d4ea"), ("DL", 1, 1, "#15d4ea"), ("/", 1, 2, "#15d4ea"), ("%", 1, 3, "#15d4ea"),
            ("7", 2, 0), ("8", 2, 1), ("9", 2, 2), ("*", 2, 3, "#15d4ea"),
            ("4", 3, 0), ("5", 3, 1), ("6", 3, 2), ("-", 3, 3, "#15d4ea"),
            ("1", 4, 0), ("2", 4, 1), ("3", 4, 2), ("+", 4, 3, "#15d4ea"),
            ("00", 5, 0), ("0", 5, 1), (".", 5, 2), ("=", 5, 3, "#fb7c14")
        ]

        for (text, row, col, *color) in buttons:
            self.create_button(text, row, col, color[0] if color else "#34495e")

        for i in range(6):
            self.root.rowconfigure(i, weight=1)
        for j in range(4):
            self.root.columnconfigure(j, weight=1)

    def create_button(self, text, row, col, bg_color):
        btn = tk.Button(self.root, text=text, font=("Poppins", 18), fg="white", bg=bg_color,
                        relief="flat", activebackground="#7f8c8d", command=lambda: self.on_click(text))
        btn.grid(row=row, column=col, sticky="nsew", padx=5, pady=5, ipadx=10, ipady=10)

    def on_click(self, char):
        if char == "AC":
            self.expression = ""
        elif char == "DL":
            self.expression = self.expression[:-1]
        elif char == "=":
            try:
                self.expression = str(eval(self.expression))
            except:
                self.expression = "Error"
        else:
            if self.expression == "0" or self.expression == "Error":
                self.expression = char
            else:
                self.expression += char
        self.entry.delete(0, tk.END)
        self.entry.insert(0, self.expression)


if __name__ == "__main__":
    root = tk.Tk()
    root.geometry("400x550")
    CalculatorApp(root)
    root.mainloop()
