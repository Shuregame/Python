# Python
```Python
import numpy as np
np.set_printoptions(precision=2, suppress=True) #precision=2 - сколько знаков после запятой; suppress - ноль будет нулем

X = np.array([[1, 2, 0],
             [0, 0, 5],
             [3, -4, 2],
             [1, 6, 5],
             [0, 1, 0]])
print("X - начальная матрица: ", X)
U, S, W = np.linalg.svd(X) #вычисляем U,S,W матрицу и присваиваем каскадом
print("U:", '\n',  U, '\n', "S", '\n', S, '\n', "W", '\n', W)
V = W.T
print("Обратная матрица к W: ", '\n', V)
# S - должна соответсвовать размерности исходной матрицы, поэтому:
D = np.zeros_like(X, dtype=float)
D[np.diag_indices(min(X. shape))] = S # shape - ???
print("Дигональная матрица D: ", '\n', D)
np.dot(U.T, U) #Скалярное произведение(получаем единичную матрицу)
np.dot(W.T, W) #Аналогично
A = np.dot(np.dot(U, D), V.T)
print("Перемножая скалярные произведения (U,D) на транспанированную V получаем исходную матрицу ", '\n', A)
```
