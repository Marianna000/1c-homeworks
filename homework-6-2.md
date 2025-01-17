# Задание к занятию "Условия и подзапросы"

## Задача № 1 "Отбор номенклатуры при обновлении цен в документе Реализация"

### Описание задачи

Изменить процедуру для команды  "Обновить цены" документа Реализация. Перечень номенклатуры получать не передачей элементов массива, а используя вложенный запрос к табличной части текущего документа.

### Требования к результату

Выгрузка информационной базы (.dt) с конфигурацией из прошлого задания в котором внести изменения для получения перечня элементов номенклатуры вложенным запросом к табличной части документа Реализация.

### Процесс выполнения

1. Использовать файл *.cf конфигурацию из прошлого задания. 
2. В форме документа Реализация для серверной процедуры команды Обновить цены внести следующие изменения:
    
    * Убрать заполнение массива элементов номенклатуры;
    * Для запроса получения цен убрать заполнение параметра СписокНоменклатуры;
    * В конструкторе запроса в параметрах виртуальной таблицы в поле условие удалить предыдущее условие и вместо него - 
      - вызвать конструктор запроса в поле условие;
      - построить запрос к табличной части документа Реализация с выборкой одного поля Номенклатура.Ссылка;
      - В операторе ГДЕ указать параметр для отбора определенной ссылки документа реализация;
      - Нажать на ОК. Полученый текст запроса использовать для условия отбора измерения Номенклатура;
    * Для запроса добавить установку параметра документа реализации текущей ссылкой, при этом проверять чтобы ссылка была не пустая;
    * Если ссылка пустая то Возврат;
3. Проверить заполнение цен для всех товаров из табличной части документа Реализация нажатием на кнопку Обновить цены.

## Задача № 2 "Заполнение строк табличной части по отбору в документе Реализация"

### Описание задачи

Добавить команду  "Заполнить строки" в табличной части документа Реализация. При заполнении добавить возможность отбора по номенклатурной группе и диапазону цен. Заполнять номенклатуру и цены из регистра Цены номенклатуры.

### Требования к результату

Прикрепить .dt файл с внесенными изменениями по реализации заполнения табличной части документа Реализация из регистра сведений Цены номенклатура по отбору.

### Процесс выполнения

* В Конфигураторе добавить обработку ЗаполнениеНоменклатуры. В обработке - 
  - создать форму и реквизиты формы ГруппаТовара - тип справочник Номенклатура с возможностью выбора только групп,
    ЦенаС, ЦенаПо - тип такой же как у ресурса Цена в регистре сведений Цены номенклатуры; 
  - Разместить реквизиты на форме;
  - Cоздать серверную функцию ПриЗакрытииНаСервере();
   - В функции ПриЗакрытииНаСервере - создать запрос. Текст запроса выбирает последние цены на дату документа Реализация из регистра сведений Цены номенклатуры. Условие в срезе 
    текста запроса формировать динамически в зависимости от значений реквизитов - ГруппаТовара, ЦенаС, ЦенаПо. При этом возможны варианты - заполнена или не заполнена группа   
    номенклатуры. ЦенаС должна быть меньше чем ЦенаПо, иначе не формировать запрос и вывести соответствующее сообщение. Если не заполнена группа товара, то отбирать цены   
    для всего товара без привязки к группе.
    Так же в зависимости от этих условий устанавливать необходимые параметры запроса.
    Создать структуру с элементами Номенклатура, Цена. В цикле заполнить массив структур из результата выборки запроса;
  - Добавить команду Заполнить и соответственно кнопку на форму. При нажатии на кнопку вызвать последовательно - команду Закрыть(), серверную функцию ПриЗакрытииНаСервере(),   
    которая возвращает заполненный массив структур. Далее вызвать команду ОповеститьОВыборе() с передачей массива структур в качестве параметра;
    
* Для командной панели табличной части документа Реализация добавить команду ЗаполнитьСтроки и соответственно кнопку;
* Переопределить событие для команды ЗаполнитьСтроки в котором реализовать открытие формы обработки ЗаполнениеНоменклатуры. В команде ОткрытьФорму() передавать в качестве владельца форму текущего документа;
* Для формы документа перекрыть событие ОбработкаВыбора на клиенте и реализовать заполнение табличной части документа из полученного массива структур в параметре   
  ВыбранноеЗначение. Заполнять значения для реквизитов Номенклатура и Цена;
* Протестировать - заполнить в регистр сведений строки и проверить заполнение строк ТЧ документа Реализация нажатием на кнопку ЗаполнитьСтроки и установкой различных вариантов     значений реквизитов формы обработки ЗаполнениеНоменклатуры.
  
