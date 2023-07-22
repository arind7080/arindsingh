# arindsingh
pythobn project
ARIND.py
import tkinter as tk
import qrcode
import pickle


def vypocet():
    global vysledok
    try:
        prve = float(entry_prve.get())
        druhe = float(entry_druhe.get())
        vysledok = prve + druhe
        vysledok_label.config(text=f"Výsledok: {vysledok}")
    except ValueError:
        open_new_window()
def qr_code():
    global vysledok, qr_counter
    qr_counter += 1
    qr = qrcode.make(f"Výsledok je {vysledok}")
    qr.save(f"qrcode{qr_counter}.png")
    save_counter()

def open_new_window():
    new_window = tk.Toplevel(root)
    new_window.title("Error Window")
    new_window.geometry("300x200")
    label = tk.Label(new_window, text="Toto je nové okno!")
    label.pack()

def load_counter():
    try:
        with open('counter.txt', 'r') as file:
            return int(file.read())
    except FileNotFoundError:
        return 0

def save_counter():
    with open('counter.txt', 'w') as file:
        file.write(str(qr_counter))

root = tk.Tk()
root.title("Kalkulačka")
root.geometry("400x300")

label = tk.Label(root, text="Kalkulačka", font=("Montserrat Bold", 16))
label.pack()


label_prve = tk.Label(root, text="Zadaj prvé čislo:", font=("Montserrat Bold", 10))
label_prve.pack()
entry_prve = tk.Entry(root)
entry_prve.pack()


label_druhe = tk.Label(root, text="Zadaj druhé čislo:", font=("Montserrat Bold", 10))
label_druhe.pack()
entry_druhe = tk.Entry(root)
entry_druhe.pack()

button = tk.Button(root, text="Vypočítať", command=vypocet, width=30, height=2)
button.pack()

vysledok_label = tk.Label(root, text= "Vysledok je ", font=("Montserrat Bold", 10))
vysledok_label.pack()

button = tk.Button(root, text="QR code", command=qr_code, width=30, height=2)
button.pack()

qr_counter = load_counter() 

root.mainloop()


