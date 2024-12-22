# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Мезенцев Кирилл Дмитриевич
- РИ230950
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
установить необходимое программное обеспечение, которое пригодится для создания интеллектуальных моделей на Python. Рассмотреть процесс установки игрового движка Unity для разработки игр. Также написать программу Hello World на python в Jupyter Notebook и на C# в Unity.

## Задание 1
### Написать программу Hello World на Python с запуском в Jupiter Notebook.
Ход работы:
- Скачать Anaconda-Navigator, в ней запустить jupiter-notebook, в нём создать папку python файлов для проектов и там создать файл python, в котором будет написано:

```py

print('Hello World!')

```

- Запускаем код и видим сообщение Hello World!.


## Задание 2
### Написать программу Hello World на C# с запуском на Unity.

- Скачиваем Unity, создаем 3d проект. Далее в окне Hierarchy создаем Empty object, для объекта создаем скрипт HelloWorld и пишем скрипт.

```csharp

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class HelloWorld : MonoBehaviour
{
    // Выводим "Hello, World!" в консоль при старте игры
    void Start()
    {
        Print("Hello World");
    }
}

```

- После сохраняем изменения и нажимаем на кнопку Play. При старте игры в консоль выведется строка Hello World

## Задание 3
### Оформить отчет в виде документации на github (markdown-разметка).

- [https://github.com/Fountainebleu/AD-in-GameDev/edit/main/WorkShop1.md](https://github.com/Fountainebleu/AD-in-GameDev/blob/main/WorkShop1.md)
  
## Выводы

Я узнал как скачать Jupiter Notebook и запустить в ней код на питон. Узнал как скачать Unity и создать 3d проект. Также понял как в юнити создать объект и создать для него скрипт. Еще проанализировал какие сущности можно обучить ML-Agent-ом.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
