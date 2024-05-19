""" Text Editor """

# I updated the functionality a bit.

import tkinter as tk
from tkinter import ttk
from tkinter import StringVar
from tkinter.filedialog import askopenfilename as aofn, asksaveasfilename as asfn
import logging as lo
import ast
import os

# All this GUI is, is a basic text editor. Eventually I will add new functions, but I'm not in the mood to dig up crap I don't need to

class GUI(tk.Tk):                # The GUI function, it calls the other functions
    def __init__(self, **kwargs):
        super().__init__()
        self.geometry('750x380')  # Base geometry
        self.title('Pix Sticky 2.1')  # Title for the app
        self.frame = ttk.Frame(self)
        self.frame.pack(fill=tk.BOTH, expand=True) # This allows the GUI to scale how ever you want
        self.font_size = tk.IntVar(value=20) # font size
        self.bind("<KeyRelease>", self.pythonsyntax)
        self.labels()
        self.scrolling_frame()
        self.styles()
        self.file_menu()

    def styles(self):   # You can change the style here
        self.style = ttk.Style()
        self.style.theme_use('blue')
            
    def scrolling_frame(self):   
                                                        # This is the text editor area
        vertical = ttk.Scrollbar(self.master, orient='vertical')
        vertical.pack(side=tk.RIGHT, fill=tk.Y)

        horizontal = ttk.Scrollbar(self.master, orient='horizontal')
        horizontal.pack(side=tk.BOTTOM, fill=tk.X)

        self.text = tk.Text(self.master, width=15, height=480, wrap=tk.NONE,     # For the text widget
                         yscrollcommand=vertical.set,
                         xscrollcommand=horizontal.set, 
                         font=("Arial", self.font_size.get(), "bold")                  # Edit the font here
                         ) 
        self.text.pack(side=tk.RIGHT, fill=tk.BOTH, expand=True)     # Expandable

        vertical.config(command=self.text.yview)      # Vertical bar
        horizontal.config(command=self.text.xview)    # Horizontal bar

        self.text.insert(tk.END,'\n', "package_font")
    def pythonsyntax(self) -> None:

        self.tag_remove('syntax error', '1.0', 'end')
        content = self.get('1.0', 'end')

        try:
            ast.parse(content)
        except SyntaxError as e:
            err_me = e.msg  # error message
            err_li = e.lineno  # line error
            err_off = e.offset  # offset error

            start = f"{err_li}.0"
            end = f"{err_li}.{len(self.get(err_li + '.0', err_li + '.end'))}"
            
            self.tag_add("syntax_error", start, end)

            print(f"Syntax {err_me}")


    def file_menu(self):                  # Menu, which calls the open, save, and new file functions (They don't work too well)
        self.file = None
        self.File_var = StringVar(value="File")
        self.filemenu = ttk.OptionMenu(self.frame, self.File_var, "File",
                                       "File", "New file", "Open file", "Save file", command=self.fmc)
        self.filemenu.grid(row=0, column=0, sticky="w")

    def fmc(self, choice):        # File function caller 
        if choice == "New file":
            self.new_file()
        elif choice == "Open file":
            self.open_file()
        elif choice == "Save file":
            self.save_file()

    def new_file(self):
        self.file = None
        self.title("PixySticky2.1")
        self.text.focus_set()
        self.text.delete("1.0", 'end')

    def open_file(self):
        self.file = aofn(defaultextension=".txt",
                         filetypes=[("All Files", "*.*"),
                                    ("Text Documents", "*.txt")])
        if self.file == "":
            self.file = None
        else:
            self.title(os.path.basename(self.file))
            self.text.delete("1.0", 'end')
            with open(self.file, 'r') as f:
                self.text.insert("1.0", f.read())

    def save_file(self):
        if self.file is None:
            self.file = asfn(initialfile='Untitled.txt',
                             filetypes=[("All Files", "*.*"),
                                        ("Text Documents", "*.txt")])
            if self.file == "":
                self.file = None
            else:
                with open(self.file, 'w') as f:
                    f.write(self.text.get("1.0", "end"))

    def labels(self):               # Title and update area
        title = "Pix Sticky 2.1 (Alpha)"
        title_2 = "by 'Pixy (The Trnasporter)' or 'ThatRandomFuckingDev'"
        update = "What is new?"
        update_text1 = "I added the bottom scrollbar so it's easier"
        update_text2 = "The text is larger, and thus you can read it"
        update_text3 = "Changed the color, the base was white and had unreadable text"


        ttle = ttk.Label(self.master, text = f"{title}",      # Title of my editor (I will find a way to incorporate the name of the file being edited)
                          font = ("Arial", 75)) # Changeable font size, etc.
        ttle.pack(side = tk.TOP, expand=False, fill=tk.X)

        title_2 = ttk.Label(self.master, text = f"{title_2}",  # secondary title
                               font = ("Arial", 25))
        title_2.pack(side = tk.TOP, expand=False, fill=tk.X) # Note, I use .pack instead of .grid as I have many issues getting the .grid function of tkinter to work.
                                                             # these titles will update per update. I might eventually add an update GUI for feature sets
                                                             # it's difficult as is to keep myself from ripping my head off doing this.

        up = ttk.Label(self.master, text = f"{update} \n"     # Tittle GUI update text
                          f"{update_text1} \n"
                          f"{update_text2} \n"
                          f"{update_text3} \n",
                          font = ("Arial", 20))
        up.pack(side = tk.TOP, expand=False, fill=tk.X)

class log(GUI):
    def __init__(self, parent, GUI) -> None:
        super().__init__(parent)
        self.propagate()
        self.errors()
        self.error_logs()
        self.labels()
        self.open_file()
        self.new_file()
        self.save_file()
        self.fmc()
        self.pythonsyntax()
        self.scrolling_frame()
        self.styles()

        pass

    def error_logs(self, parent) -> False:
        if parent:
            super().labels()
            super().open_file()
            super().new_file()
            super().save_file()
            super().fmc()
            super().pythonsyntax()
            super().scrolling_frame()
            super().styles()
        else:
            print('')

    def errors(self, labels, open_file,
               new_file, save_file, fmc, 
               pythonsyntax, scrolling_frame, 
               styles):
        
        def label_error():
            try:
                labels
            except Exception as e:
                 lo.error("Error occcored with labels", e)
            else:
                 return labels
            
        def file_menu_error():
                     
            try:
                open_file, save_file, new_file
            except Exception as ef:
                  lo.error("Error opening/saving/creating file", ef)
            else:
                return open_file, save_file, new_file
            
        def syntax_error():
        
            try:
               pythonsyntax
            except Exception as epy:
                lo.error("Error with Python syntaxing", epy)
            else:
                return pythonsyntax
        
        def file_error():

            try:
               fmc
            except Exception as fce:
                lo.error("Error within the options menu", fce)
            else:
                return fmc
        
        def graphical_interface_error():

            try:
               scrolling_frame, styles
            except Exception as egui:
                lo.error("Error with the GUI", egui)
            else:
                return scrolling_frame, styles
        
        if label_error:
            print(f"{label_error}")
        else:
            labels

        if file_menu_error:
            print(f"{file_menu_error}")
        else:
            open_file, save_file, new_file

        if syntax_error:
            print(f"{syntax_error}")
        else:
            pythonsyntax

        if file_error:
            print(f"{file_error}")
        else:
            fmc
        
        if graphical_interface_error:
            print(f"{graphical_interface_error}")
        else:
            scrolling_frame, styles


# I got some help from online sources I dug up to create the save, open, and new file options. 

if __name__ == '__main__':  # Main caller loop
    app = GUI()
    app.mainloop()
