# BaseSchedule
Базовое расписание на которое накладываются замены с сайта.

## Структура расписания звонков

### CallSchedule

`FileVersion` - версия файла.

`Data` - ключ=CallScheduleBuilding,значение=CallScheduleData.

`Note` - опциональное поле, строка, примечание к файлу.

### CallScheduleBuilding

строка:
```
A1  - Корпус "А" 1 этаж,
C   - Корпус "С" пока что эквивалентно Корпусу "А" 1 этаж,
A2  - Корпус "А" 2 этаж,
А3  - Корпус "А" 3 этаж,
Т1  - Корпус "Т" чётная сторона,
Т2  - Корпус "Т" НЕ чётная сторона,
SUB - Субботнее расписание звонков для всех корпусов,
P1  - Расписание "Пара - час",
UNK - Неизвестное расписание, практика.
```

### CallScheduleData

Массив где индекс=номер пары минус один (первая пара - 0), а значение строка времени.

Строка может состоять из четырёх сегментов:

`10:15 - 10:55 - 11:00 - 11:40`

Что значит:

`начало пары - конец первой половины - начало второй половины - конец пары`

Либо из двух сегментов для расписаний пара час и практики:

`10:50 - 11:50`

Что значит:

`начало пары - конец пары`

БЕЗ ПЕРЕРЫВОВ!

Время всегда записано в 24-часовой системе, в поясе UTC+5.


## Структура основного расписания пар

### Schedule

`FileVersion` - версия файла.

`Data` - ключ=группа,значение=`ScheduleGroup`.

`Note` - опциональное поле, строка, примечание к файлу.

### ScheduleGroup

Массив из 6-и элементов `ScheduleDay`, где 0 - понедельник а 6 - суббота.

### ScheduleDay

Массив из `ScheduleLesson`.

### ScheduleLesson

`Subject` - строка предмет

`Room` - строка аудитории

`Teacher` - преподаватель, может быть пустой если неизвестен.

`Para` - номер пары, если он >10 но <20, эта пара только на первой неделе, если >20 то второй.

Пример:

`13` - это третья пара только на первой неделе.

`23` - это третья пара только на второй неделе.

`3` - это всегда третья пара.
