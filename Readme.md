# Метод главных компонент

Одним из решений проблемы мультиколлинеарности может подвержение наших исходных признаков функциональному преобразованию,гарантировав линейную независимость 
новых признаков, и, возможно, сократив их количество, то есть уменьшив размерность задачи.

В анализе данных, как и в любом другом анализе, порой бывает нелишним создать упрощенную модель, максимально точно описывающую реальное положение дел. Часто бывает так, что признаки довольно сильно зависят друг от друга и их одновременное наличие избыточно.

Но гораздо чаще бывает так, что признаки зависят друг от друга не так строго и не так явно. Мы можем выразить несколько признаков через один, слить воедино, так сказать, и работать уже с более простой моделью. Конечно, избежать потерь информации, скорее всего не удастся, но минимизировать ее нам поможет как раз метод PCA.

Выражаясь более строго, данный метод аппроксимирует n-размерное облако наблюдений до эллипсоида (тоже n-мерного), полуоси которого и будут являться будущими главными компонентами. И при проекции на такие оси (снижении размерности) сохраняется наибольшее количество информации.

В методе главных компонент (principal component analysis, PCA) строится минимальное число новых признаков, по которым исходные признаки восстанавливаются линейным 
преобразованием с минимальными погрешностями. PCA относится к методам обучения без учителя (unsupervised learning), поскольку матрица «объекты–признаки» F преобразуется
ез учёта целевого вектора y.

!!! PCA подходит как для регрессии, так и для классификации !!!

## Постановка задачи

Рассмотрим матрицу «объектов–признаков»

<a href="url"><img src="https://github.com/Shuregame/Python/blob/master/1.png" height="100" width="400" ></a>

Обозначим через zi = (g1(xi), . . . , gm(xi)) признаковые описания тех жеобъектов в новом пространстве Z = R m меньшей размерности, m < n:

<a href="url"><img src="https://github.com/Shuregame/Python/blob/master/2.png" height="100" width="400" ></a>

Потребуем, чтобы исходные признаковые описания можно было восстановить по новым описаниям с помощью некоторого линейного преобразования, определяемого матрицей U = (ujs)n×m:

<a href="url"><img src="https://github.com/Shuregame/Python/blob/master/3.png" height="70" width="400" ></a>

или в векторной форме: xˆ = zU T.

Восстановленное описание xˆ не обязано в точности
совпадать с исходным описанием x, но их отличие на объектах обучающей выборки
должно быть как можно меньше при выбранной размерности m. Будем искать одновременно и матрицу новых признаковых описаний G, и матрицу линейного преобразования U, при которых суммарная невязка восстановленных описаний минимальна:

<a href="url"><img src="https://github.com/Shuregame/Python/blob/master/4.png" height="70" width="430" ></a>

## Теорема

<a href="url"><img src="https://github.com/Shuregame/Python/blob/master/5.png" height="80" width="550" ></a>

# Практика

## Шаг 1. Подготовка данных

Сгенерируем выборку:
```Python
x = np.arange(1,11)
y = 2 * x + np.random.randn(10)*2
X = np.vstack((x,y))
print X

OUT:
[[  1.           2.           3.           4.           5.          
    6.           7.           8.           9.          10.        ]
 [  2.73446908   4.35122722   7.21132988  11.24872601   9.58103444   
  12.09865079  13.78706794  13.85301221  15.29003911  18.0998018 ]]
```

<a href="url"><img src="https://github.com/Shuregame/Python/blob/master/7.png" height="150" width="200" ></a>

В данной выборке у нас имеются два признака, сильно коррелирующие друг с другом. С помощью алгоритма PCA мы сможем легко найти признак-комбинацию и, ценой части информации, выразить оба этих признака одним новым. Итак, давайте разбираться!

Для описания случайной величины используются моменты. Нужные нам – мат. ожидание и дисперсия. 

Сам процесс проецирования на вектор никак не влияет на значения средних, так как для минимизации потерь информации наш вектор должен проходить через центр нашей выборки. Поэтому нет ничего страшного, если мы отцентрируем нашу выборку – линейно сдвинем ее так, чтобы средние значения признаков были равны 0. Это очень сильно упростит наши дальнейшие вычисления (хотя, стоит отметить, что можно обойтись и без центрирования).
Оператор, обратный сдвигу будет равен вектору изначальных средних значений – он понадобится для восстановления выборки в исходной размерности.

## P.S. Статья требут доработки) 
