# Описание проекта

Публичное методическое пособие по 3-му году обучения на направлении "Сетевое и системное администрирование" в ГБНОУ Академия Цифровых Технологий.

# Актуальность

Методичка будет полезна как преподавателям, так и студентам. Подавляющее большинство технологий, описываемых в курсе, на момент 2023-2024 года распространено в эксплуатации и получает постоянную поддержку. Технологии со статусом **deprecated** могут приводиться в качестве примера для изучения развития тех или иных историй, но им не уделено столько же внимания, сколько актуальным аналогам.

//Список технологий с разбивкой на отдельные группы (Категория под вопросом):

# Часть I: Самая база

Виртуализация -> ВМ из образа и шаблона -> Формирование сетевой связности -> Работа с командной строкой; утилиты

## Виртуализация

> **_Что такое виртуализация_** : Это процесс создания виртуальной версии физической операционной системы с абстрагированными ресурсами

В терминологии выделяют **гипервизор** - программное обеспечение на машине-хосте, которое отвечает за распределение ресурсов между виртуальными машинами и контроль над ними. В качестве примера, домашний Windows 10 будет являться хостом для развёрнутой в программе VirtualBox (гипервизор) операционной системы Linux Ubuntu (виртуальная машина/виртуалка). 

Типизация:

1. Гипервизор первого типа - это специализированная ОС, которая ставится на пустое железо или параллельно основной системе, и обладает всем необходимым функционалом для распределения и контроля над ресурсами виртуалок. Отличается быстрым взаимодействием с железом, взаммен же придётся учитывать и обеспечивать совместимость драйверов.

**Примеры**: Hyper-V, KVMб ESXi

![Pasted image 20230916235801](https://github.com/cocojamba69/SSA-Courses-3y/assets/63653997/aa8231f5-96a6-4f39-a125-9df5221c5416)

2. Гипервизор второго типа - это программное обеспечение под управлением операционной системы, причём последняя берёт на себя задачи распределения физических ресурсов. Из плюсов простота в эксплуатации и в подключении веб-интерфейса. Фаворит в обучении с нуля.

**Примеры**: VirtualBox, VMware Workstation, OpenVZ

![Pasted image 20230917000703](https://github.com/cocojamba69/SSA-Courses-3y/assets/63653997/a5258251-08b5-44be-98e0-041807443572)

В рамках 3-го года обучения мы будем пользоваться гипервизором VMware, поэтому особенности развёртывания и обслуживания VM-ок зачастую будут проходить через призму субъективной позиции этого вендора.

**Для работы виртуальной машины ей необходимо выделить место на жёстком диске, оперативную память и ядра процессора**

**Процессор является конкурентноспособным**: несколько виртуальных машин под одним хостом, при условии не слишком большой нагрузки на виртуальные ОС, способны сосуществовать в рабочем режиме, конкурируя за общие ядра.

В противовес, жёсткий диск и оперативная память - неконкурентноспособны. В кластере всегда необходимо следить за тем, чтобы у всех была своя непересекающаяся оперативная память: в зависимости от задач конкретной VM ей можно выделить от 800 до 2048 Мб.

В VMsphere есть две методики выделения пространства на жёстком диске: _thin_ и **thick** provisioning. Thick - это монолитное выделение места на машине-хосте. Выделил 30Гб, но заполнил всего 16 - остальные будут недоступны для использования другими VM-ами и хостом. По аналогии thin provisioning выделяет память динамически.

