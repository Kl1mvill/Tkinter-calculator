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
