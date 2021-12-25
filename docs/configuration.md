# Файл настроек

Файл настроек **config.yaml** создается при первом запуске программы.
Его структура проста, отредактировать можно в любом текстовом редакторе, например - Блокноте.

Используется крайне простой язык разметки YAML.
Полную и избыточную документацию по структуре YAML можно найти по адресу: [https://yaml.org/](https://yaml.org/)

## Базовые настройки

Повторяет файл настроек my_account.txt

```yaml
start_day: 1
start_month: 1
start_year: 2021
timezone: Europe/Moscow
token: t.Dlinnyii_Token_Is_TinkoffAPI
```

## Раздел настройки счетов

Разделы счетов формируются автоматически после первого запуска скрипта.

```yaml
'111222333444':
  filename: tinkoffReport_%Y.%b.%d_111222333444
  id: '111222333444'
  name: account-111222333444
  parse: True
  show empty operations: False
```

**'Название раздела'** - номер счета в API

Строки с параметрами, принадлежащими разделу, начинаются с двух пробелов - "вложены".

**filename** - Шаблон именования файла отчета для счета. По умолчанию - tinkoffReport_%Y.%b.%d_111222333444 - то есть префикс "tinkoffReport", дата формирования отчета в формате 2021.Nov.07, номер счета. Такое же имя будет в случае некорректного шаблона в настройках. (подробности формата - см. раздел [Шаблоны имени файла](#шаблоны-имени-файла))

**id** - Повторяет номер счета в API. ***Не используется.***

**name** - Название счета для Вас. Используется в выводе сообщений об ошибках. По умолчанию: account-номер счета.

**parse** - Отметка формировать ли отчет по данному счету. По умолчанию - True. (см. [Обработка булевых значений](#обработка-булевых-значений) ниже)

**show empty operations** - выводить ли в отчете "пустые"/невыполненнные операции. По умолчанию - False. (см. [Обработка булевых значений](#обработка-булевых-значений) ниже)

## Шаблоны имени файла

Шаблон, формирует имя файла, с замещением кодов на дату, составления отчета. Форматы замещения:

%Y - год в формате "2021"

%y - год в формате "21"

%b - месяц, трехбуквенное название - "May" или "Nov"

%m - месяц в виде двух цифр с ведущим нолем: "05" или "11"

%d - день в виде двух цифр, с ведущим нолем: от "01" до "31"

%H - часы в виде двух цифр, с ведущим нолем: от "00" до "23"

%M - минуты в виде двух цифр, с ведущим нолем: от "00" до "59"

Полный список кодов замещения можно посмотреть тут: [список кодов](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-format-codes)

### Примеры

Примеры формируемых имен файлов, если на дворе 15 ноября 2021 года, время 12:55:

* **tinkoffReport_%Y.%b.%d_11223344** - tinkoffReport_2021.Nov.15_11223344
* **tinkoffReport_%Y-%m-%d_11223344** - tinkoffReport_2021-11-15_11223344
* **t-R-_%Y.%b.%d_ИИС** - t-R_2021.Nov.15_ИИС
* **t-R-_%Y-%m-%d_Брокерский** - t-R_2021-11-15_Брокерский
* **t-R-_%Y-%m-%d_%H:%M_Брокерский** - t-R_2021-11-15_12:55_Брокерский

## Обработка булевых значений

За **True** принимаются значения True, Yes, On, 1 и другие положительные целые числа.

За **False** принимаются значения False, No, Off, 0 и другие отрицательные целые числа.