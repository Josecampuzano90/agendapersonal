import tkinter as tk
from tkinter import ttk, messagebox
from tkcalendar import DateEntry

def agregar_evento():
    fecha = entry_fecha.get()
    hora = entry_hora.get()
    descripcion = entry_descripcion.get()
    if fecha and hora and descripcion:
        tree.insert('', 'end', values=(fecha, hora, descripcion))
        entry_fecha.set_date('')
        entry_hora.delete(0, tk.END)
        entry_descripcion.delete(0, tk.END)
    else:
        messagebox.showwarning("Campos vacíos", "Por favor, complete todos los campos.")

def eliminar_evento():
    seleccionado = tree.selection()
    if seleccionado:
        confirmacion = messagebox.askyesno("Confirmación", "¿Está seguro de eliminar el evento?")
        if confirmacion:
            tree.delete(seleccionado)
    else:
        messagebox.showwarning("Selección requerida", "Seleccione un evento para eliminar.")

root = tk.Tk()
root.title("Agenda Personal")
root.geometry("500x400")

frame_input = tk.Frame(root)
frame_input.pack(pady=10)

lbl_fecha = tk.Label(frame_input, text="Fecha:")
lbl_fecha.grid(row=0, column=0, padx=5, pady=5)
entry_fecha = DateEntry(frame_input, width=12, background='darkblue', foreground='white', borderwidth=2)
entry_fecha.grid(row=0, column=1, padx=5, pady=5)

lbl_hora = tk.Label(frame_input, text="Hora:")
lbl_hora.grid(row=1, column=0, padx=5, pady=5)
entry_hora = tk.Entry(frame_input)
entry_hora.grid(row=1, column=1, padx=5, pady=5)

lbl_descripcion = tk.Label(frame_input, text="Descripción:")
lbl_descripcion.grid(row=2, column=0, padx=5, pady=5)
entry_descripcion = tk.Entry(frame_input)
entry_descripcion.grid(row=2, column=1, padx=5, pady=5)

btn_agregar = tk.Button(frame_input, text="Agregar Evento", command=agregar_evento)
btn_agregar.grid(row=3, column=0, columnspan=2, pady=10)

frame_tree = tk.Frame(root)
frame_tree.pack()

tree = ttk.Treeview(frame_tree, columns=("Fecha", "Hora", "Descripción"), show="headings")
tree.heading("Fecha", text="Fecha")
tree.heading("Hora", text="Hora")
tree.heading("Descripción", text="Descripción")
tree.pack()

btn_eliminar = tk.Button(root, text="Eliminar Evento", command=eliminar_evento)
btn_eliminar.pack(pady=5)

btn_salir = tk.Button(root, text="Salir", command=root.quit)
btn_salir.pack(pady=5)

root.mainloop()
