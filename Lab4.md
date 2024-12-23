# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
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
Изучить устройство перцепрона и принцип его работы. Создать перцептроны, реализующие логические элементы. Визуализировать графиками зависимости количества эпох от ошибки обучения и построить визуальную модель работы перцептрона в Unity.

## Задание 1
### в проекте Unity реализовать перцептрон, который умеет производить вычисления:
### OR | дать комментарии о корректности работы
### AND | дать комментарии о корректности работы
### NAND | дать комментарии о корректности работы
### XOR | дать комментарии о корректности работы

Ход работы:
- Сделаем в юнити 4 сцены, каждая из которых будет отвечать за какую-либо 1 операцию. Далее пустому объекту присваиваем класс Perceptron и настраиваем входные и выходные данные

- OR (Логическое ИЛИ)
- Корректность работы: Перцептрон корректно обучается выполнять операцию OR, так как она линейно разделима. Весовые коэффициенты и смещение (bias) настраиваются так, чтобы разделить данные 0 и 1 вдоль прямой линии в пространстве. Обучается в среднем за 4 эпохи
- Результат: Входы (0,0) дают 0, остальные (0,1), (1,0), (1,1) дают 1.

- AND (Логическое И)
- Корректность работы: Перцептрон корректно обучается для операции AND, поскольку она также линейно разделима. Весовые коэффициенты увеличиваются для повышения строгости границы принятия решения. Обучается в среднем за 7 эпох
- Результат: Только вход (1,1) дает 1, все остальные дают 0.

- NAND (Отрицание И)
- Корректность работы: Перцептрон корректно обучается выполнять операцию NAND, поскольку она является инверсией AND. Сама операция линейно разделима, так что стандартный алгоритм обучения справляется с ней без проблем. Обучается в среднем за 7 эпох
- Результат: Все входы, кроме (1,1), дают 1, а (1,1) дает 0.

- XOR (Исключающее ИЛИ)
- Корректность работы: Перцептрон не сможет корректно обучиться выполнять операцию XOR, так как она не является линейно разделимой. Два класса (выходы 0 и 1) нельзя разделить одной прямой в пространстве. Для выполнения XOR потребуется многослойная сеть (например, двухслойный перцептрон с нелинейной функцией активации).

## Задание 2
### Построить графики зависимости количества эпох от ошибки  обучения. Указать от чего зависит необходимое количество эпох обучения.

- Ссылка на таблицу: https://docs.google.com/spreadsheets/d/1bH8Ymq4sC8HF9ada5_-FIBB0bVU2hd5ZNwGnfKIBntw/edit?gid=0#gid=0
- Если нелинейно разделимые данные (например, XOR), то базовый перцептрон не сможет обучиться независимо от количества эпох, так как он неспособен разделить такие данные. Для этих задач требуется более сложная архитектура, например многослойный перцептрон. А если линейно разделимые данные (например, OR, AND, NAND), то задача будет решена.
- В случае линейно разделимых данных количество эпох варируется от начальных значения весов и смещения (bias). Если начальные веса и смещение близки к оптимальным значениям, перцептрон обучается быстрее. Если начальные значения слишком далеки от оптимальных, потребуется больше эпох, чтобы достигнуть сходимости. Но в среднем количество эпох будет как в таблице с примерно такими ошибками в каждой эпохе.

## Задание 3
### Построить визуальную модель работы перцептрона на сцене Unity.

- На каждой сцене создаем плато и четыре ряда кубиков. В каждом ряду по два кубика, которые мы раскрашиваем. Белый цвет - это 0, а черный цвет - это 1. В первом ряду 2 белых, во втором белый и черный, в третьем черный и белый, в четвертом 2 черных.
- Дальше добавим в скрипт перцептрона список testResults, который хранит результат вычислений после тренировки.

```csharp

using System.Collections;
using System.Collections.Generic;
using System.Linq;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;
	public List<double> testResults;

	[SerializeField] private int trainNumber;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(trainNumber);
		
		testResults.Add(CalcOutput(0, 0));
		testResults.Add(CalcOutput(0, 1));
		testResults.Add(CalcOutput(1, 0));
		testResults.Add(CalcOutput(1, 1));
		
		
		Debug.Log("Test 0 0: " + testResults[0]);
		Debug.Log("Test 0 1: " + testResults[1]);
		Debug.Log("Test 1 0: " + testResults[2]);
		Debug.Log("Test 1 1: " + testResults[3]);
	}
	
	void Update () {
		
	}
}

```

- Дальше каждому верхнему кубику добавляем скрипт ChangeColor, который получает нужный результат вычислений перцептрона и красит оба кубика в нужный цвет. Если результат равен 0, то покрасит оба кубика в белый, а если результат равен 1, то красит оба кубика в черный

```csharp

using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ChangeColor : MonoBehaviour
{
    public Perceptron perceptron;
    [SerializeField] private int experementNumber;

    private void OnCollisionEnter(Collision other)
    {
        var perceptronRes = perceptron.GetComponent<Perceptron>().testResults;

        for (var i = 0; i < perceptronRes.Count; i++)
        {
            if (i == experementNumber && perceptronRes[i] == 0)
            {
                other.gameObject.GetComponent<Renderer>().material.color = Color.white;
                this.gameObject.GetComponent<Renderer>().material.color = Color.white;
                break;
            }
            else if (i == experementNumber && perceptronRes[i] == 1)
            {
                other.gameObject.GetComponent<Renderer>().material.color = Color.black;
                this.gameObject.GetComponent<Renderer>().material.color = Color.black;
                break;
            }
        }
    }
}

```

- Запускаем сцену и верхний кубик падает на нижный и красит оба кубика в соответствии с результатами работы перцептрона в списке testResults. Если total error в итоге равен 0, то сцена отработает корректно. В сцене Xor коректной визуальной модели не будет, потому что перцептрон не может решить эту задачу.

## Выводы

Я изучил устройство перцептрона и понял принцип его работы. Создал перцептроны, реализующие логические элементы. Визуализировал в гугл таблице зависимости количества эпох от ошибки обучения и понял от чего зависит необходимое количество эпох. Построил визуальную модель работы перцептрона в Unity.

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
