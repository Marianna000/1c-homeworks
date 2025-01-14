# Задание к занятию "Типы данных"

## Задача 1 "Булевский калькулятор"

### Описание задачи
Создать обработку-булевский калькулятор, в которой значение и результат обрабатывались бы операциями **И**, **НЕ**, **ИЛИ**.

### Требования к результату
Обработка, аналогичная созданной в задании (https://github.com/netology-code/1c-homeworks/blob/master/homework-1-6.md), где значения и операции были бы булевскими. Операций должно быть три: бинарные **И**, **ИЛИ** и унарная **НЕ** (со значением реквизита **Результат**).

### Процесс выполнения
1. Вызовем команду "Новый" из подменю "Файл" и выберем вид документа "Внешняя обработка".
2. Дадим ей имя **БулевскийКалькулятор** и создадим форму, нажав на кнопку с лупой.
3. На форму обработки добавим два реквизита типа "Булево": **Значение** и **Результат**.
4. Перетащим их на форму, где они станут элементами вида **Флажок**.
5. Добавим команды **ОперацияИли**, **ОперацияИ** и **ОперацияНе**.
6. Перетащим команды на форму, чтобы они стали кнопками.
7. Из контекстного меню каждой кнопки создадим обработчик, выбрав пункт "<Действие команды>" с вариантом "Создать на клиенте".
8. В коде каждого обработчика (в процедурах с именами "ОперацияИли", "ОперацияИ", "ОперацияНе") напишем код, проводящий соответствующую операцию со значениями реквизитов **Результат** и **Значение** (операция НЕ - унарная и проводится только со значением реквизита **Результат**);
9. Сохраним обработку как файл "БулевскийКалькулятор.epf".

## Задача 2 "Реквизиты справочника Сотрудники"

### Описание задачи
Создать справочник **Сотрудники** с описанными ниже реквизитами, типы которых соответствуют их смыслу и назначению.

### Требования к результату
Выгрузка информационной базы (.dt) с конфигурацией **УправлениеИТФирмой**, в которой был бы справочник **Сотрудники** с реквизитами, типы которых соответствуют их смыслу и назначению.

### Процесс выполнения
1. Используйте конфигурацию **УправлениеИТФирмой** из предыдущих заданий (https://github.com/netology-code/1c-homeworks/blob/master/homework-1-3.md).
2. Справочник **Сотрудники** измените так, чтобы в нем были реквизиты:
* **ДатаРождения**, **ДатаПриема** и **ДатаУвольнения**.
* **ИдентификаторПользователяИнформационнойБазы**.
* **ИНН** (какова длина ИНН физического лица)?
* **Комментарий** (подумайте, нужно ли ограничивать длину комментария).
* **Недействителен**.
* **Оклад** и **СтавкаЧаса** (Число разумной длины и точности или определяемый тип; можно оставить из предыдущего задания).
* **Пол**.
* **Фотография** для хранения данных фотографии.
Реквизиты, созданные в ходе выполнения предыдущего задания, можно не трогать.
