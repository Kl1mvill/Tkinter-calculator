# Калькулятор на Tkinter
## Графический интерфейс
![2023-06-24_10-35-02.png](https://ie.wampi.ru/2023/06/24/2023-06-24_10-35-02.png)
## Принцип работы
Сначала мы импортируем Tkinter. Создаем окно и убираем возможность изменять размер окна, а также добавляем заголовок.
```py
from tkinter import *

root = Tk()
root.resizable(width=False, height=False)
root.title("Калькулятор")
```

Потом создаем функции для изменения текста в поле ввода калькулятора с помощью кнопок.
```py
# Очищает поле ввода калькулятора и обнуляет calc_operation.
def clear_all():
    global calc_operation
    calc_operation = ""
    text_input.set("")


# Удаляет последний символ из поля ввода калькулятора и calc_operation.
def delete_char():
    global calc_operation
    calc_operation = calc_operation[:-1]
    text_input.set(calc_operation)


# Выполняет математическую операцию, записанную в calc_operation, и выводит результат в поле ввода.
def button_equal():
    global calc_operation
    try:
        temp_op = str(eval(calc_operation))

    except ZeroDivisionError:
        clear_all()
        add_char("На ноль делить нельзя!")

    text_input.set(temp_op)
    calc_operation = temp_op

"""

Добавляет символ в calc_operation и в поле ввода.
При некоторых условиях, таких как если в строчке находится только символ 0, а пользователь вводит цифры то ноль удаляется.
Если в calc_operation находится сообщение "На ноль делить нельзя!", весь текст удаляется, чтобы можно было ввести новое выражение.
Если calc_operation пуст, и вводится знак математической операции, то ничего не происходит.

"""
def add_char(char):
    global calc_operation

    if calc_operation == "0" and char in "1234567890":
        delete_char()

    if calc_operation in "На ноль делить нельзя!":
        clear_all()

    if calc_operation == "" and char in "*//-+": return

    calc_operation += char
    text_input.set(calc_operation)
```

Создаем словарь с настройками для кнопок разных видов.
```py
# Настройки вида кнопок
button_params_number = {'bd':5, 'fg':'#949494', 'bg':'#3C3636', 'font':('sans-serif', 18, 'bold')}
button_params_sign = {'bd':5, 'fg':'#000', 'bg':'#949494', 'font':('sans-serif', 18, 'bold')}
```

Создаем переменные для дисплея калькулятора, а также сам дисплей.
```py
calc_operation = ""
text_input = StringVar() 

calculator_display = Entry(root, font=('sans-serif', 20, 'bold'), textvariable=text_input,
                     bd=5, insertwidth = 5, bg='#949494', justify='right').grid(columnspan=5, padx = 10, pady = 20)
```

Создаем кнопки и используем ранее созданные настройки для кнопок, а также добавляем команды. 
С помощью метода `grid()` мы выстраиваем кнопки в виде сетки. 
```py
# --- первая колонка ---

C = Button(root, button_params_sign, text="C",
            command=clear_all).grid(row=1, column=0, sticky="nsew")

Del = Button(root, button_params_sign, text="⌦",
            command=delete_char).grid(row=1, column=1, sticky="nsew")

left_par = Button(root, button_params_sign, text='(',
            command=lambda: add_char("(")).grid(row=1, column=2, sticky="nsew")

right_par = Button(root, button_params_sign, text=')',
            command=lambda: add_char(")")).grid(row=1, column=3, sticky="nsew") 


# --- вторая колонка ---

button_7 = Button(root, button_params_number,  text="7",
            command=lambda: add_char("7")).grid(row=2, column=0, sticky="nsew")

button_8 = Button(root, button_params_number, text="8",
            command=lambda: add_char("8")).grid(row=2, column=1, sticky="nsew")

button_9 = Button(root, button_params_number, text="9",
            command=lambda: add_char("9")).grid(row=2, column=2, sticky="nsew")

div = Button(root, button_params_sign, text="/",
            command=lambda: add_char("//")).grid(row=2, column=3, sticky="nsew")


# --- третья колонка ---

button_4 = Button(root, button_params_number, text="4", 
            command=lambda: add_char("4")).grid(row=3, column=0, sticky="nsew")

button_5 = Button(root, button_params_number, text="5", 
            command=lambda: add_char("5")).grid(row=3, column=1, sticky="nsew")

button_6 = Button(root, button_params_number, text="6", 
            command=lambda: add_char("6")).grid(row=3, column=2, sticky="nsew")

mul = Button(root, button_params_sign, text="*", 
            command=lambda: add_char("*")).grid(row=3, column=3, sticky="nsew")


# --- четвертая колонка ---

button_1 = Button(root, button_params_number, text="1", 
            command=lambda: add_char("1")).grid(row=4, column=0, sticky="nsew")

button_2 = Button(root, button_params_number, text="2", 
            command=lambda: add_char("2")).grid(row=4, column=1, sticky="nsew")

button_3 = Button(root, button_params_number, text="3", 
            command=lambda: add_char("3")).grid(row=4, column=2, sticky="nsew")

sub = Button(root, button_params_sign, text="-", 
            command=lambda: add_char("-")).grid(row=4, column=3, sticky="nsew")


# --- пятая колонка ---

button_0 = Button(root, button_params_number, text="0", 
            command=lambda: add_char("0")).grid(row=5, column=0, sticky="nsew")

point = Button(root, button_params_sign, text=".", 
            command=lambda: add_char(".")).grid(row=5, column=1, sticky="nsew")

equal = Button(root, button_params_sign, text="=", 
            command=button_equal).grid(row=5, column=2, sticky="nsew")

add = Button(root, button_params_sign, text="+", 
            command=lambda: add_char("+")).grid(row=5, column=3, sticky="nsew")
```

Запускаем приложение.
```py
root.mainloop()
```
