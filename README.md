# Применение непрерывного вейвлет-преобразования для поиска краев объектов на изображении

## 1. Описание схемы подразделения

Пусть $s\in\mathbf{N}$ и $\mathbf{Z}^s$ -- целочисленная решетка. Схема подразделения определяется заданной последовательностью $a=\{a_{\alpha}\}_{\alpha\in\mathbf{Z}^s}$ . Оператор $\mathrm{S}$ действует на последовательности по формуле: 

$(\mathrm{S}\lambda)_{\alpha}=\sum\limits_{\beta\in\mathbf{Z}^s} a_{\alpha-2\beta}\lambda_{\beta},~\lambda\in l_{\infty}(\mathbf{Z}^s)$

**Определение 1.** Схема подразделения $\lambda^m=\mathrm{S}\lambda^{m-1}$ сходится для $\lambda\in l_{\infty}(\mathbf{Z}^s)$, если существует непрерывная функция $f_{\lambda}$, такая что $\lim\limits_{m\to +\infty}\left\| f_{\lambda}\left(\frac{\cdot}{2^m}\right)-\lambda^m\right\|_{\infty} = 0$.

## 2. Поиск краев на изображении

**Определение 2.** Вейвлетом называется функция $\psi \in \mathrm{L}_{1} ({\bf R}^2)\cap\mathrm{L}_{2} ({\bf R}^2)$, удовлетворяющая условию $\int\limits_{\mathbf{R}^2}\psi (\mathrm{x})d\mathrm{x} =0$.

**Определение 3.** Для функции $f(x,y)$ вейвлет-преобразование определено равенством:

$$
W_s f(x,y) = \iint\limits_{\mathbf{R}^2} f(x-u,y-v)\psi_s(u,v)dudv
$$

где $\psi_s(u,v) = \frac{1}{s^2}\psi\left(\frac{u}{s},\frac{v}{s}\right)$.

### 2.1. Вычисление $W_sf$

Путем свертки изображения с предварительно созданными фильтрами, получаем вейвлет-коэффициенты $W_sf$.

### 2.2. Алгоритм определения края

1. Находим точки, для которых $|\nabla W_{s_j}f(x,y)|\geqslant T$, где $T$ - порог.

2. Среди найденных точек оставляем те, которые удовлетворяют условию $\frac{1}{R}\leqslant \frac{|\nabла W_{s_j} f(x,y)|}{|\nabла W_{s_l} f(x,y)|}\leqslant R$ для всех $j$ и $l$.

## Основные шаги алгоритма EdgeDetect.ipynb

1. **Создание маски подразделения:** Задается маска подразделения с использованием целочисленной решетки.
2. **Определение функции вейвлета:** Реализуется функция вейвлета на основе схемы подразделения и маски.
3. **Вычисление вейвлет-преобразования изображения:** Изображение подвергается свертке с вейвлет-функцией для различных масштабов.
4. **Определение градиента:** Вычисляется градиент вейвлет-преобразования для каждого масштаба.
5. **Пороговая фильтрация:** Определяются точки, в которых градиент превышает порог.
6. **Уточнение краев:** С использованием отношения градиентов на разных масштабах выбираются точки, соответствующие краям объектов.

## Использование

1. Загрузите изображение в переменную `f`.
2. Выберите значения параметров: порог `T`, коэффициент `R`, и значения масштабов `s_values`.
