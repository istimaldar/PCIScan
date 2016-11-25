import os
import tkinter as tk
from tkinter import ttk


class MainWindow(tk.Tk):
    def __init__(self):
        tk.Tk.__init__(self)

        self.table = ttk.Treeview()
        self.table["columns"] = ("#1", "#2", "#3", "#4", "#5")
        self.table.heading("#0", text="Номер шины")
        self.table.heading("#1", text="Номер устройства")
        self.table.heading("#2", text="Vendor ID")
        self.table.heading("#3", text="Device ID")
        self.table.heading("#4", text="Расшифрованное Vendor ID")
        self.table.heading("#5", text="Расшифрованное Device ID")
        IDs = self.parce_dev_id()
        for string in open('/proc/bus/pci/devices', 'r'):
            self.table.insert("", 0,    text=string.split()[0][:2], values=(string.split()[0][-2:],
                                                                            string.split()[1][:4],
                                                                            string.split()[1][-4:],
                                                                            IDs["Vendor"][string.split()[1][:4]],
                                                                            IDs["Device"][string.split()[1][-4:]]))
        self.table.pack(expand=tk.TRUE, fill=tk.BOTH)

        self.mainloop()

    def parce_dev_id(self):
        VIDs = {}
        DIDs = {}
        for line in open('pci.ids', 'r'):
            tabs = line[:2].rfind('\t')
            if tabs > -1 and len(line.rstrip().lstrip('\t').split()) > 1:
                DIDs[line.rstrip().lstrip('\t').split()[tabs]] = " ".join(line.rstrip().lstrip('\t').split()[tabs + 1:])
            elif len(line.rstrip().lstrip('\t').split()) > 1:
                VIDs[line.rstrip().lstrip('\t').split()[0]] = " ".join(line.rstrip().lstrip('\t').split()[1:])
        return {"Vendor": VIDs, "Device": DIDs}


if __name__ == "__main__":
    MainWindow()