# Задание к занятию "Конструктор запросов"

## Задача "Обновление цен в документе Реализация"

### Описание задачи

Добавить команду и соответственно кнопку "Обновить цены" в командную панель табличной части документа Реализация. При нажатии на кнопку присходит обновление цен номенклатуры в табличной части на дату документа.

### Требования к результату

Выгрузка информационной базы (.dt) с конфигурацией из задания https://github.com/netology-code/1c-homeworks/blob/master/homework-5-5.md в котором реализовать алгоритм обновления цен в табличной части документа Реализация.

### Процесс выполнения

1. Взять конфигурацию из файла https://github.com/netology-code/1c-homeworks/blob/master/homework-5-5.md.
2. Периодичность регистра сведений Цены номенклатуры должна быть установлена в значение в Пределах дня.
3. В форме документа Реализация - создать команду ОбновитьЦены и перетащить в командную панель табличной части.
4. Перекрыть действие команды и выбрать пункт "Создать на клиенте и процедуру на сервере".
5. В процедуре на сервере реализовать процесс обновления цен следующим образом:
    
    * Добавить проверку на заполненность табличной части Товары;
    * Сформировать массив элементов, который содержит в себе перечень всей номенклатуры из табличной части;
    * Из контекстного меню выбрать Конструктор запроса с обработкой результата, в котором выбрать Тип обработки = Обход результата;
    * На закладке Таблицы и поля конструктора добавить в Таблицы Цены.СрезПоследних;
    * В параметрах виртуальной таблицы укажите параметр периода и условие Номенклатура в (&СписокНоменклатуры);
    * Выбираем поля - Номенклатура и Цена и нажимаем на кнопку Ок;
    * Для запроса устанавливаем значения параметров такие как дата объекта и заполненный массив элементов номенклатуры табличной части;
    * Выполняем запрос и проверяем чтобы результат был не пустой. Иначе возврат;
    * Если запрос не пустой - делаем выборку и обходим в цикле все записи результата выполнения запроса;
    * В табличной части документа находим строки и в цикле подставляем цену из текущей записи результата запроса.
      Поиск строк табличной части осуществляем через НайтиСтроки(). В качестве параметра заполняем структуру значением номенклатуры из   
      записи результата запроса.
    * Если цена новая отличается от старой то пересчитываем сумму найденной строки;
   
