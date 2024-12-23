# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
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
Разработать оптимальный баланс изменения сложности для десяти уровней игры Dragon Picker.

## Задание 1
### Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице.
Ход работы:
- На сложность уровня влияют переменные, которые отвечают за движение дракона: скорость, вероятность поменять направление, дистанция движение влево или вправо. Также на сложность влияет переменная дракона, отвечающая за интервал между бросанием яиц.
- По моему мнению линейное нарастание сложности будет оптимальным
- Надо написать скрипт на питоне, который заполнит таблицу данными, а затем визуализируем их

```py

import gspread
import pandas as pd


# Данные для уровней сложности
data = {
    "Level": list(range(1, 11)),
    "Speed": [4, 6, 8, 10, 12, 14, 16, 18, 20, 22],
    "TimeBetweenEggDrops": [1.5, 1.4, 1.3, 1.2, 1.1, 1, 0.9, 0.8, 0.7, 0.6],
    "ChanceDirection": [0.01, 0.015, 0.02, 0.025, 0.03, 0.035, 0.04, 0.045, 0.05, 0.055],
    "LeftRightDistance": [11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
}

# Создаем DataFrame
df = pd.DataFrame(data)

gc = gspread.service_account(filename='unitydatascience-445516-bed97c061547.json')
sh = gc.open("UnityWorkshop3")

# Формируем список данных для записи
values = df.values.tolist()

# Обновляем диапазон данных за один раз
sh.sheet1.update('A2:E11', values)

```

- Ссылка на таблицу: https://docs.google.com/spreadsheets/d/1Ks30zJnwiKVzFMwMeEeH7IVj8mOqdv1kT17u8JTn4NY/edit?gid=0#gid=0
- Также создаем скрипт, который визуализирует данные в питоне

```py

import pandas as pd
import matplotlib.pyplot as plt

# Данные для уровней сложности
data = {
    "Level": list(range(1, 11)),
    "Speed": [4, 6, 8, 10, 12, 14, 16, 18, 20, 22],
    "TimeBetweenEggDrops": [1.5, 1.4, 1.3, 1.2, 1.1, 1, 0.9, 0.8, 0.7, 0.6],
    "ChanceDirection": [0.01, 0.015, 0.02, 0.025, 0.03, 0.035, 0.04, 0.045, 0.05, 0.055],
    "LeftRightDistance": [11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
}

# Создаем DataFrame
df = pd.DataFrame(data)

# Визуализация данных
plt.figure(figsize=(12, 8))

# Скорость
plt.subplot(2, 2, 1)
plt.plot(df["Level"], df["Speed"], marker='o', label="Speed", color='blue')
plt.title("Dragon Speed by Level")
plt.xlabel("Level")
plt.ylabel("Speed")
plt.grid(True)

# Время между сбросами
plt.subplot(2, 2, 2)
plt.plot(df["Level"], df["TimeBetweenEggDrops"], marker='o', label="Time Between Egg Drops", color='red')
plt.title("Time Between Egg Drops by Level")
plt.xlabel("Level")
plt.ylabel("Time (seconds)")
plt.grid(True)

# Шанс смены направления
plt.subplot(2, 2, 3)
plt.plot(df["Level"], df["ChanceDirection"], marker='o', label="Chance Direction", color='green')
plt.title("Chance of Changing Direction by Level")
plt.xlabel("Level")
plt.ylabel("Chance")
plt.grid(True)

# Дистанция движения
plt.subplot(2, 2, 4)
plt.plot(df["Level"], df["LeftRightDistance"], marker='o', label="Left Right Distance", color='purple')
plt.title("Left-Right Distance by Level")
plt.xlabel("Level")
plt.ylabel("Distance")
plt.grid(True)

plt.tight_layout()
plt.show()

```


## Задание 2
### Создайте 10 сцен на Unity с изменяющимся уровнем сложности.

- Создаём 10 сцен и на каждом создаём Level Manager, в котором будет хранится номер уровня.

```csharp

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class LevelManager : MonoBehaviour
{
    public int currentLevel;
}

```
- Дальше переходим в скрипт дракона. На старте мы определяем LevelManager, берем данные текущего уровня из таблицы и присаиваем их значения дракону.

```csharp

using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using Random = UnityEngine.Random;
using SimpleJSON;


public class EnemyDragon : MonoBehaviour
{
    public GameObject dragonEggPrefab;
    public float speed = 1;
    public float timeBetweenEggDrops = 1f;
    public float leftRightDistance = 10f;
    public float chanceDirection = 0.1f;
    private LevelManager levelManager;
    
    void Start()
    {
        levelManager = GameObject.Find("LevelManager").GetComponent<LevelManager>();
        StartCoroutine(GoogleSheets());
        Invoke("DropEgg", 2f);
    }

    IEnumerator GoogleSheets()
    {
        var url =
            "https://sheets.googleapis.com/v4/spreadsheets/1AWIzQIQIJpiYiGZp7hzbYT2hgNwW152vB1AbJE1aX-o/values/A2:E11?key=AIzaSyCo6uB0fxKN7kmr77Z5xhPSQ0vs0abXIg4";
        UnityWebRequest request = UnityWebRequest.Get(url);
        yield return request.SendWebRequest();

        if (request.result == UnityWebRequest.Result.Success)
        {
            var jsonData = JSON.Parse(request.downloadHandler.text);
            var values = jsonData["values"];
            for (int i = 0; i < values.Count; i++)
            {
                var row = values[i];
                var level = int.Parse(row[0]);
                if (level == levelManager.currentLevel)
                {
                    speed = float.Parse(row[1]);
                    timeBetweenEggDrops = float.Parse(row[2]);
                    chanceDirection = float.Parse(row[3]);
                    leftRightDistance = float.Parse(row[4]);
                    Debug.Log($"Данные уровня {level}: Speed={speed}, TimeBetweenEggDrops={timeBetweenEggDrops}, ChanceDirection={chanceDirection}, LeftRightDistance={leftRightDistance}");
                    break;
                }
            }
        }
        else
        {
            Debug.LogError("Ошибка загрузки: " + request.error);
        }
    }
    
    void DropEgg(){
        Vector3 myVector = new Vector3(0.0f, 5.0f, 0.0f);
        GameObject egg = Instantiate<GameObject>(dragonEggPrefab);
        egg.transform.position = transform.position + myVector;
        Invoke("DropEgg", timeBetweenEggDrops);
    }

    // Update is called once per frame
    void Update()
    {
        Vector3 pos = transform.position;
        pos.x += speed * Time.deltaTime;
        transform.position = pos;

        if (pos.x < -leftRightDistance){
            speed = Mathf.Abs(speed);
        }
        else if (pos.x > leftRightDistance){
            speed = -Mathf.Abs(speed);
        }
    }

    private void FixedUpdate() {
        if (Random.value < chanceDirection){
            speed *= -1;
        }
    }
}

```
- После запускаем

## Задание 3
### Решение в 80+ баллов должно визуализировать данные из google-таблицы, и с помощью Python передавать в проект Unity. В Python данные также должны быть визуализированы.

- Данные визуализировны и в таблице и в питоне.

## Выводы

- Я смог создать линейное нарастание уровня сложности для 10 уровней игры Dragon Picker. Также сделана визуализация данных в таблице и эти данные передаются в юнити.

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
