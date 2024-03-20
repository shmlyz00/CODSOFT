import tkinter as tk
from tkinter import ttk
from tkinter import Tk, Button, PhotoImage, messagebox,scrolledtext
import os
import pickle

window=tk.Tk()
window.title("tp do liste")
window.config(bg="#D3D3D3")
# window.resizable(width=False, height=True)
label=tk.Label(window, text=" to do list",font=("times new roman  ",20,"bold") ,bg="#D3D3D3", fg="#6A5ACD")
label.pack()
def load_tasks():
    if os.path.exists('tasks.dat'):
        with open('tasks.dat', 'rb') as f:
            return pickle.load(f)
    return []

# Save tasks to file to ensure old tasks are not lost
def save_tasks(tasks):
    with open('tasks.dat', 'wb') as f:
        pickle.dump(tasks, f)

def add():
    
    if val.get()!="":
       list_task.insert(tk.END, val.get())
    else:
        messagebox.showwarning("warning","please enter a task")
    entry.delete(0, 'end')
def delet():
    selected_index = list_task.curselection()
    if selected_index:
        list_task.delete(selected_index)
    else:
        messagebox.showwarning("warning","please select a task")
# frame for entry and button of add and del

val=tk.StringVar()
entry=ttk.Entry(window, textvariable=val)
entry.pack(side="top",padx=10, pady=10)
frame=tk.Frame(window,bg="#D3D3D3")
frame.pack()
add_button=tk.Button(frame,text="add", command= add, bg="#90EE90")
window.bind('<Return>', lambda event: add())
add_button.grid(column=0 , row=1, padx=20, pady=10)
del_button=tk.Button(frame,text="del", command=delet, bg="#F08080")
window.bind('<Delete>', lambda event: delet())
del_button.grid(column=1, row=1 , padx=10, pady=10)
# frame for liste of tasks 
fram1=tk.Frame(window , bg="#D3D3D3")

list_task=tk.Listbox(fram1,width=55, height=25,
                     bg="#FFFFFF", fg="#000000",
                     font=("Times",10),                   
                     )
list_task.pack()
fram1.pack()
scrol = ttk.Scrollbar(list_task)
scrol.place(relx=1, y=0, relheight=1, anchor="ne") 
list_task.config(yscrollcommand=scrol.set)
scrol.config(command=list_task.yview)

window.mainloop()
