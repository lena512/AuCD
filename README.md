"""
Лабораторная работа №1
Написать программу, которая читая символы из бесконечной последовательности (эмулируется конечным файлом, читающимся поблочно), распознает, преобразует и выводит на экран лексемы по определенному правилу. Лексемы разделены пробелами. Преобразование делать по возможности через словарь. Для упрощения под выводом числа прописью подразумевается последовательный вывод всех цифр числа. Регулярные выражения использовать нельзя.
Вариант 19.
Нечетные двоичные числа, не превышающие 819210, в которых встречается не менее одной серии из двух подряд идущих единиц. Выводит на экран цифры числа, исключая единицы. Отдельно выводится прописью номер позиции, с которой начинается эта серия.
"""
d_db = {'0':'ноль', '1':'один', '2':'два', '3':'три', '4':'четыре', '5':'пять', '6':'шесть', '7':'семь', '8':'восемь', '9':'девять'}
buf_len = 1
work_buf = ""
work_buf2 = ""
limit = 819210
begins = 0
a = 0
d = 0
t_b = False
work_buf_len = buf_len
with open("text.txt","r") as file:
    buf = file.read(buf_len)
    if not buf:
        print("\nФайл text.txt пуст.\n")
    while buf:
        while buf >= '0' and buf <= '9':
            if buf >= '0' and buf <= '9':
                work_buf += buf
            buf = file.read(buf_len)
        if len(work_buf) > 0:
            f_b = True
            for i in range(len(work_buf)):
                if work_buf[i] != '0' and work_buf[i]!= '1':
                    f_b = False
        if f_b and len(work_buf) > 1 and work_buf[-1] == '1':
            for i in range(len(work_buf)):
                if work_buf[i] == '1' and work_buf[i+1] == '1':
                    begins += i
                    t_b = True
                    break
        if f_b and t_b:
            for i in range(len(work_buf)):
                if work_buf[i] == '0' or work_buf[i] == '1':
                    d = int(work_buf, base = 2)
            if d < limit:
                d2 = str(d)
                for i in range(len(d2)):
                    if d2[i] != '1':
                        work_buf2 += d2   
                print(work_buf2)
                a += 1
                begins2 = str(begins)
                for i in range(len(begins2)):
                    print(d_db[begins2[i]])
        work_buf = ''
        work_buf2 = ''
        begins = 0
        buf = file.read(buf_len)
    if a == 0:
        print('В файле нет чисел удовлетворяющих условию')
        

