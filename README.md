## Как сдавать задания

Обязательными к выполнению являются задачи без указания звездочки. Их выполнение необходимо для получения зачета и диплома о профессиональной переподготовке.

Задачи со звездочкой (*) являются дополнительными задачами и/или задачами повышенной сложности. Они не являются обязательными к выполнению, но помогут вам глубже понять тему.

Домашнее задание выполните в файле readme.md в github репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

Любые вопросы по решению задач задавайте в чате Slack.

---


# Домашнее задание к занятию "5.1. Основы виртуализации"

## Задача 1

Вкратце опишите, как вы поняли - в чем основное отличие паравиртуализации и виртуализации на основе ОС.

## Ответ на Задачу 1
Основное отличие на мой взгляд следующее:

1. Паравиртуализация позволяет запускать ядра ОС отличные от хостовой ОС 
2. При использовании паравиртуализации дистрибутивы соответствующих ОС для виртуальных машин должны быть модифицированы (т.е. возможность запуска ограничена ОС с открытым исходным кодом)
3. Виртуализация на основе ОС не позволяет запускать ОС отличные от хостовой

## Задача 2

Выберите тип один из вариантов использования организации физических серверов, 
в зависимости от условий использования.

Организация серверов:
- физические сервера
- паравиртуализация
- виртуализация уровня ОС

Условия использования:

- Высоконагруженная база данных, чувствительная к отказу
- Различные Java-приложения
- Windows системы для использования Бухгалтерским отделом 
- Системы, выполняющие высокопроизводительные расчеты на GPU

Опишите, почему вы выбрали к каждому целевому использованию такую организацию.

## Ответ на Задачу 2
- Высоконагруженная база данных, чувствительная к отказу
Я бы использовал физические сервера или аппаратную виртуализацию серверов, объединенных в кластер по нескольким причинам:
1. Отказоустойчивость. Пара отдельных физических серверов или аппаратная виртуализация на базе серверов в кластере , дублирующих другд руга обеспечит доступность базы данных даже в случае поломки одно из физических хостов
2. Нет конкуренции за ресурсы хоста. Каждый выделенные физический хост имеет свои апппаратные ресуры (аналогичная история с аппартной виртуализацией из-за ее возможности жесткого разделения ресурсов), которые не надо делить, например, в случае использования виртуальными 
машинами, соответственно есть прогнозируемая и управляемая производительность для всех компонент физического сервера.

- Различные Java-приложения
Возможно использовать виртуализацию на увроне ОС (например, Docker). JAVA приложения кроссплатформенны, можно запустить их на ОС аналогичной хосту,
( например, возможно применить микросервисную архитектуру, запустив набор микросервисов для распределенного приложения).

- Windows системы для использования Бухгалтерским отделом 
Возможно использовать паравиртуализацию на базе Hyper V от Microsoft, т.к. это позволит использовать ОС Windows, все системы установить на один хост, при отсутствии
специфических требований по отказоустойчивости и производительности Hyper V поможет сэкономить на железе и дальнейшем администрировании.

- Системы, выполняющие высокопроизводительные расчеты на GPU
Подойдет любая из систем виртуализации, позволяющая гибко и жестко распределять ресурсы gpu.

## Задача 3

Как вы думаете, возможно ли совмещать несколько типов виртуализации на одном сервере?
Приведите пример такого совмещения.

## Ответ на задачу 3

На мой взгляд вполне жизнеспособен вариант когда совмещена, например, аппаратная виртуализация и виртуализация на уровне операционной системы.

Например, средствами VMWare созданы два хоста. Первый используется по БД, а на втором разворачиваются Docker контейнеры для микросервисов.
