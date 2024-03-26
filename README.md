#-------------------------------------------IMPORT TKINTER--------------------------------------------------------------

from tkinter import *
from tkinter import messagebox


#--------------------------------------------CREATING CONSTANTS---------------------------------------------------------


PINK = "#e2979c"
BLACK = "#050504"
GREY = "#c0b8b8"
DARK_GREY = "#887a7a"
FONT = ("Times",12 , "bold")

#----------------------------------------------------CREATING FUNCTIONS-------------------------------------------------


def calculate_bmi():
    
    global res, msg
    msg = ""
    bmi_entry.delete(0, END)
    category_entry.delete(0, END)

    try:
        weight = float(user_weight.get())
        height = float(user_height.get())
        if weight <= 0 or height <= 0:
            raise ZeroDivisionError

    except ValueError:
        messagebox.showerror("Error", "Values must be numeric")
        res = ''
    except ZeroDivisionError:
        messagebox.showerror("Error", "Height and(or)  weight value cannot be zero")
        res = ''
    else:
        user_bmi = weight / (height * height)
        user_bmi_res = round(user_bmi, 2)
        res = str(user_bmi_res)
        if user_bmi < 18.5:
            msg = "Underweight"
            category_entry.insert(0, msg)

        elif user_bmi < 25:
            msg = "Normal Healthy Weight"

        elif user_bmi < 30:
            msg = "Overweight"

        elif user_bmi < 35:
            msg = "Obese"

        else:
            msg = "Extremely Obese"

    bmi_entry.insert(0, res)
    category_entry.insert(0, msg)


def clear_values():
    user_weight.delete(0, END)
    user_height.delete(0, END)
    bmi_entry.delete(0, END)
    category_entry.delete(0, END)





#----------------------------------------UI SETUP-----------------------------------------------------------------------


window = Tk()
window.geometry("650x580")
window.configure(bg=PINK)
window.title("BMI CALCULATOR")



#------------------------------------------CREATING CHART IMAGE---------------------------------------------------------


canvas = Canvas(width=300, height=300, bg=PINK, highlightthickness=0)
chart_image = PhotoImage(file="images.png")
canvas.create_image(150,150,image=chart_image)
canvas.grid(column=2, row=1)


#---------------------------------------------CREATING WIDGETS----------------------------------------------------------


title_label = Label(window, text="BMI CALCULATOR", padx=30, pady=15, bg=PINK, font = FONT)
weight_label = Label(window, text="Your weight(in Kgs): ", padx=13, fg= BLACK ,bg=PINK, pady=10, font=FONT)
height_label = Label(window, text="Your height(in mts): ", padx=13, pady=10, fg= BLACK ,bg=PINK, font=FONT)
bmi_label = Label(window, text="BMI Value: ", padx=13, pady=10, fg= BLACK ,bg=PINK, font=FONT)
bmi_msg = Label(window, text="BMI Category: ", padx=13, pady=10, fg= BLACK ,bg=PINK, font=FONT)

#----------------------------------------------CREATING ENTRIES---------------------------------------------------------


user_weight = Entry(window, width = 20 )
user_height = Entry(window, width = 20)
bmi_entry = Entry(window, width = 20, bg=GREY, font=FONT)
category_entry = Entry(window, width=20, bg=GREY, font=FONT)

res = 0
msg = ''

#--------------------------------------------- CREATING BUTTONS USING TKINTER-------------------------------------------


compute_button = Button(window, text="Compute", padx=5, pady=5, bg=DARK_GREY, font=FONT, command=calculate_bmi)
reset_button = Button(window, text="Reset", padx=5, pady=5, bg=DARK_GREY, font=FONT, command=clear_values)


#---------------------PLACING ALL OF THEM IN THE WINDOW USING TKINTER LAYOUT MANAGER------------------------------------
title_label.grid(row=0, column=2)
weight_label.grid(row=2, column=1)
height_label.grid(row=3, column=1)
user_weight.grid(row=2, column=3)
user_height.grid(row=3, column=3)
compute_button.grid(row=4, column=3)
reset_button.grid(row=4, column=1)
bmi_label.grid(row=5, column=1)
bmi_entry.grid(row=5, column=3)
bmi_msg.grid(row=6, column=1)
category_entry.grid(row=6, column=3)

#---------------------------- TO ALWAYS DISPLAY WINDOW----------------------------------------------------------------------

window.mainloop()
