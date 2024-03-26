# AI-driven-Language-Preservation-Game
Créez un jeu alimenté par l'IA qui enseigne et préserve les langues en voie de disparition de manière interactive et engageante.
import tkinter as tk
from tkinter import ttk, messagebox

# Mock data for demonstration purposes
languages = {'Cherokee': {'ᎣᏏᏲ': 'Hello', 'ᏩᏙᎠᏂᎩ': 'Thank you'},
             'Navajo': {'Yá’át’ééh': 'Hello', 'Ahéhee’': 'Thank you'}}

current_language = None
current_word = None

def select_language():
    global current_language
    current_language = language_var.get()
    next_word()

def next_word():
    global current_word
    if current_language:
        words = list(languages[current_language].keys())
        current_word = random.choice(words)
        word_label.config(text=current_word)
        answer_entry.delete(0, tk.END)

def check_answer():
    if current_language and current_word:
        correct_answer = languages[current_language][current_word]
        user_answer = answer_var.get()
        if user_answer.lower() == correct_answer.lower():
            messagebox.showinfo("Correct", "Your answer is correct!")
        else:
            messagebox.showinfo("Incorrect", f"The correct answer is: {correct_answer}")
    next_word()

# Setup the GUI
root = tk.Tk()
root.title("AI-driven Language Preservation Game")

main_frame = ttk.Frame(root, padding="10")
main_frame.grid(row=0, column=0, sticky=(tk.W, tk.E, tk.N, tk.S))

language_var = tk.StringVar()
ttk.Label(main_frame, text="Select a Language:").grid(row=0, column=0, sticky=tk.W)
language_menu = ttk.OptionMenu(main_frame, language_var, None, *languages.keys(), command=lambda _: select_language())
language_menu.grid(row=0, column=1, sticky=tk.W)

word_label = ttk.Label(main_frame, text="Word will appear here", font=('Helvetica', 16))
word_label.grid(row=1, column=0, columnspan=2, pady=20)

answer_var = tk.StringVar()
answer_entry = ttk.Entry(main_frame, textvariable=answer_var)
answer_entry.grid(row=2, column=0, columnspan=2, pady=5)

submit_button = ttk.Button(main_frame, text="Check Answer", command=check_answer)
submit_button.grid(row=3, column=0, columnspan=2, pady=5)

root.mainloop()
