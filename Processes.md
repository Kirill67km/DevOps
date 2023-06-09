# Задание 1

---

Рассмотрим загрузку данных и многопоточность. В описанных ниже ситуациях поможет ли использование нескольких потоков для скачивания уменьшить время общей загрузки?
 - *`100 файлов на разных Web-серверах, суммарным объёмом 10 Гбайт, через подключение со скоростью 1Мбит\с;`*
 - *`100 файлов на разных Web-серверах, суммарным объёмом 10 Гбайт, через подключение со скоростью 10 Гбит\с;`*
 - *`1 файл объёмом 10 Гбайт находящийся в торрентах;`*
 - *`1 файл объёмом 10 Гбайт находящийся на FTP-сервере;`*
 - *`10 файлов объёмом по 1 Гб находящихся в общей папке компьютера секретаря.`*
  
*Приведите ответ для каждого случай в свободной форме (лучше использовать один поток скачивания, несколько, всё равно) со своим комментарием.*
Напишите ответ в свободной форме.

**В первую очередь стоит отметить, что ниже будут рассмотрены ситуации с многоядерными процессорами, поскольку в одноядерных потоки будут выполняться по очереди,
а значит увеличение скорости мы не почувствуем.

**100 файлов на разных Web-серверах, суммарным объёмом 10 Гбайт, через подключение со скоростью 1Мбит\с**

**100 файлов на разных Web-серверах, суммарным объёмом 10 Гбайт, через подключение со скоростью 10 Гбит\с;**

 `Первый и второй случай схожи, поскольку файлы находятся на разных серверах и скорость подключения не будет влиять на общее время загрузки ` 
 
**1 файл объёмом 10 Гбайт находящийся в торрентах;**

 `Да, здесь целесообразно разбить общую загрузку 1 файла на 10 потоков по 1 Гбайт, что сократит время общей загрузки `
 
**1 файл объёмом 10 Гбайт находящийся на FTP-сервере;**

 `Основное назначение FTP-сервера - удаленная передача данных, уже логично предположить, что передача данных частям - не лучшее решение, 
 к этому же стоит сказать, что ftp-сервер режет скорость загрузки, а следовательно - ничего не выиграем `
 
**10 файлов объёмом по 1 Гб находящихся в общей папке компьютера секретаря.**

 `В данном случае использовать 10 поток, тем самым мы выиграем ускоренную загрузку файлов в параллельном режиме, то есть по 1 потоку на файл `

---

# Дополнительные задания (со звездочкой*)

---

# Задание 1.1*

---

Попробуйте высказать предположение о количестве потоков скачивания, для случаев приведенных выше, если загрузка данных происходит на следующие системы:
- *`Компьютер Windows 10 64-bit\ i5-xxxx \16 Gb\ 2 TB HDD`*
- *`Компьютер Windows 10 32-bit\ i7-xxxx\ 8 Gb\ 2 TB HDD`*
- *`Ноутбук Windows 10 64-bit\ i7-xxxx\ 32 Gb\ 500 GB HDD`*
- *`Ноутбук Windows 10 64-bit\ i7-xxxx\ 32 Gb\ 2 TB HDD`*
- *`Компьютер Windows 8.1 32-bit\ i3-xxxx\ 8 Gb\ 1 TB SSD`*
- *`Компьютер Windows 10 64-bit\ i3-xxxx\ 8 Gb\ 1 TB HDD (RAID)`*

*Необязательно рассматривать все возможные комбинации, достаточно описать своими словами отличия*

**Рискну предположить, что указанные параметры в целом влияют на количество потоков скачивания и скорость загрузки данных, 
где то мы выигрываем за счет процессора нового поколения, где то за счет оперативки, где то за счет диска, 
поэтому, на мой взгляд, в данном случае будет четвертый вариант - выигрывает за счет процессора, количества оперативки, 
несмотря на то, что ноутбук, у которого производительность будет ниже по сравнению с ПК**

**Примечания:**

- *`другими запущенными процессами на компьютерах можно пренебречь;`*
- *`производительность CPU: i7 > i5 > i3.`*

---

# Задание 1.2*

---

Какой из приведенных выше компьютеров постоянно "тормозит" и почему?

**`Компьютер Windows 10 64-bit\ i3-xxxx\ 8 Gb\ 1 TB HDD (RAID)` - хоть и стоит современная ОС поколение процессора, 
количество оперативной памяти и hdd никто не отменял, а с учетом указанных в примере их - старое поколение, 
мало оперативки, да еще и hdd в raid**

---

# Задание 2*

---

Объясните, что делает команда:

*`ps -aux | grep root | wc -l >> root`*

*Ответ напишите в свободной форме*

**Записываем  количество процессов в системе в файл root, отфильтровав их по пользователю root**

*`Примечание:`*

Если вы встречаете неизвестную команду Linux, либо неизвестные параметры команды, то можете вызвать встроенную помощь:man <команда>
Например:

- *`man ps;`*
- *`man grep;`*
- *`man wc.`*

---

# Задание 3*

---

Напишите команду, которая выводит все запущенные процессы пользователя root в файл `*"user_root_ps".*`

*`ps -aux | grep root >> user_root_ps`*

---

# Задание 4*

---

Начинающий администратор захотел вывести все запущенные процессы пользователя с логином "2" в файл "user_2_ps".

*Для этого он набрал команду:*

*`ps -U 2> user_2_ps`*

*Затем, он аналогично повторил для пользователя с логином "5" вывод в файл "user_5_ps":*

*`ps -U 5> user_5_ps`*

**Вопрос:**

Почему вывод этих команд и содержимое файлов сильно отличаются друг от друга? Как должны выглядеть правильные команды?

**Проблема заключается в том, что во втором случае необходимо было использовать “>>”, 
чтобы дозаписать результаты в файл, а начинающий системный администратор перезаписал содержимое файла при помощи “>”**

*`Примечание:`*

**Если у вас в системе нет пользователей "2" и/или "5" (это нормальная ситуация), то утилита ps выводит только одну строку:
PID TTY TIME CMD**

---

<div id="header" align="center">
  <img src="https://media.giphy.com/media/O8HtuXS6zKECI/giphy.gif" width="500"/>
</div>
