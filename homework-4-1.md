# Задание к занятию "Справочники"

## Задача 1 "Версия конфигурации"

### Описание задачи
Добавить константу **ВерсияКонфигурации**, которая будет хранить версию конфигурации из свойств метаданных, с которой программа запускалась в последний раз. Хранение версии в данных позволит обнаружить запуск программы с измененной версией и запустить код, заполняющий недостающие данные при обновлении версии.

### Требования к результату
Выгрузка информационной базы (.dt) с конфигурацией из диплома блока А, в которой:
* Присутствует константа ВерсияКонфигурации, скрытая из командного интерфейса.
* Присутствует код, при начале работы системы сравнивающий версию из метаданных и версию из константы, и, при обнаружении отличий, устанавливающий значение константы равным версии из свойств метаданных.

### Процесс выполнения
* Создать константу **ВерсияКонфигурации** типа **Строка**, которая будет хранить текущую версию конфигурации. Скрыть ее из командного интерфейса, сняв флажок "Использовать стандартные команды".
* Создать общий модуль **ОбновлениеИнформационнойБазыВызовСервера** с экспортной процедурой **ПриНачалеРаботыСистемы**, которая:
  * Проверит, совпадает ли версия конфигурации (Метаданные.Версия) со значением константы (Константы.ВерсияКонфигурации.Получить()).
  * При совпадении ничего не сделает.
  * При выявлении разницы вызовет ОбновлениеИнформационнойБазы.ПриИзмененииВерсии(СтараяВерсия, НоваяВерсия).
  * И установит значение константы равным новой версии из метаданных.
* Таким образом, при обновлении информационной базы старой версии на конфигурацию новой версии будут выполнены обработчики обновления, необходимые новой версии. Сами обработчики обновления писать пока не нужно (процедура ПриИзмененииВерсии будет пустой).
* Проверьте, что при изменении версии в метаданных и запуске программы значение константы обновляется. Открыть константу можно через режим технического специалиста.

## Задача 2 "Контактная информация"

### Описание задачи
Добавить в справочник "Контрагенты" табличную часть "Контактная информация" для хранения адресов, телефонов и т.п. в разрезе видов контактной информации, так, как это делается в реальных прикладных решениях, вместо хранения каждого вида контактной информации в отдельном реквизите, как мы это делали раньше. Заполнить предопределенные виды контактной информации недостающими данными и сделать обработчик переноса контактной информации из отдельных реквизитов в табличную часть - так, как это делается при обновлении в реальных прикладных решениях.

**Важно!** Чтобы проверить успешность переноса, не забудьте предварительно заполнить контактную информацию некоторых контрагентов в отдельных реквизитах.

### Требования к результату

Выгрузка информационной базы (.dt) с конфигурацией из диплома блока А, в которой:

* Присутствует справочник ВидыКонтактнойИнформации с пятью предопределенными элементами: ЮридическийАдресКонтрагента, ПочтовыйАдресКонтрагента, ФактическийАдресКонтрагента, ТелефонКонтрагента, EMailКонтрагента и реквизитом Тип (ПеречислениеСсылка.ТипыКонтактнойИнформации).
* В справочнике Контрагенты присутствует табличная часть КонтактнаяИнформация, данные которой выведены на форму контрагента таблицей (а прежние реквизиты, напротив, имеют префикс Удалить и скрыты).
* Присутствует код, при начале работы системы сравнивающий версию из метаданных и версию из константы, и:
  * при переходе на версию 1.0.0.1 или более новую, а также при первом запуске инициирующий заполнение типов предопределенных элементов справочника ВидыКонтактнойИнформации.
  * при переходе на версию 1.0.0.2 или более новую, а также при первом запуске инициирующий перенос контактной информации из реквизитов Удалить<...> в ТЧ КонтактнаяИнформация.

### Процесс выполнения

#### Виды контактной информации

* Создать перечисление ТипыКонтактнойИнформации со значениями: Адрес, Телефон, EMail.
* Создать справочник ВидыКонтактнойИнформации с реквизитом Тип (ПеречислениеСсылка.ТипыКонтактнойИнформации), включив его в роль БазовыеПрава на просмотр и чтение. Справочник будет расширяемым для пользователей, а значение реквизита Тип позволит программе понять, как работать с этим видом КИ.
* Создать предопределенные виды контактной информации: ЮридическийАдресКонтрагента, ПочтовыйАдресКонтрагента, ФактическийАдресКонтрагента, ТелефонКонтрагента, EMailКонтрагента.
* В модуле менеджера справочника создать экспортную процедуру ЗаполнитьПредопределенныеЭлементы(), которая заполнит реквизит Тип у всех предопределенных элементов этого справочника (в Конфигураторе можно задать только код и наименование предопределенных элементов, но не другие реквизиты).
* Установить версию конфигурации в метаданных на произвольное значение (напримере, 1.0.0.1).
* В процедуре ОбновлениеИнформационнойБазы.ПриИзмененииВерсии:
  * Проверить, не находится ли версия 1.0.0.1 между значениями параметров СтараяВерсия и НоваяВерсия, включая границы (если старая версия пуста - значит, она меньше любой текущей).
  * Если версия 1.0.0.1 находится между старой и новой версией, включая границы - вызвать процедуру ЗаполнитьПредопределенныеЭлементы().
* Таким образом, и при первом запуске, и при обновлении будут заполнены предопределенные элементы.

#### Контрагенты

* Нужно использовать справочник Контрагенты из диплома блока А.
* Стандартному реквизиту Наименование дать синоним "Краткое наименование".
* Добавить табличную часть КонтактнаяИнформация с реквизитами Вид (СправочникСсылка.ВидыКонтактнойИнформации) и Значение (Строка).
* Прежним реквизитам, отвечавшим за контактную информацию, нужно добавить к наименованию префикс "Удалить" (Например: УдалитьЮридическийАдресКонтрагента) и скрыть их из форм. Совсем удалять их нельзя, чтобы можно было перенести старые данные.
* Добавить в форму контрагента (лучше на отдельную закладку) новую табличную часть.
* В модуле менеджера справочника создать экспортную процедуру ЗаполнитьТабличнуюЧастьКонтактнаяИнформация(), которая:
  * Откроет выборку всех элементов справочника (Справочники.Контрагенты.Выбрать()).
  * Для каждого элемента очистит ТЧ КонтактнаяИнформация и заполнит ее значениями старых реквизитов (с префиксом Удалить).
  * Запишет каждый элемент.
* В процедуре ОбновлениеИнформационнойБазы.ПриИзмененииВерсии при обновлении на версию 1.0.0.2 вызвать процедуру ЗаполнитьТабличнуюЧастьКонтактнаяИнформация().
* Взвести версию в метаданных на 1.0.0.2.
* Запустить программу и удостовериться, что ранее введенная контактная информация не утеряна и доступна теперь уже через новую табличную часть, как в реальных прикладных решениях.
