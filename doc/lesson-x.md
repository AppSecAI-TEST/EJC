# Lesson xx: Algorithms: sort
## Вступление
Алгоритмы - набор инструкций, описывающий действия, которые необходимо выполнить для достижения некоторого результата. Они описываются в такой обширной теме, как "Алгоритмы и структуры данных". Именно под таким названием можно найти различные программы обучения, книги или дополнительные курсы.
Нас окружают данные. Везде. Всё вокруг нас - это нескончаемый поток данных. И одно из основных действий, которое мы вополняем с этими данными - сортировка.

## Сортировка пузырьком (bubble sort)
Одним из самых простейших алгоритмов сортировка является сортировка пузырьком (или методом простого обмена). Ещё её иногда называют глупой сортировкой.
Назвали ей так по аналогии с пузырьками в воде. Как известно, воздух легче воды, поэтому пузырьки воздуха всплывают. В пузырьково сортировке более легкие (с меньшим значением) элементы постепенно "всплывают" в начало массива, а более тяжелые друг за другом опускаются на дно (в конец массива).

Написать и понять её не составляет труда.
Имея массив данных, мы берём пару элементов и сравниваем их. Если элемент слева больше, чем элемент справа - меняем их местами.
Завершитя всё тогда, когда за полный проход по массиву не будет сделано ни одной замены.
Статьи про пузырьковые сортировки:
[Пузырьковая сортировка и все-все-все](https://habrahabr.ru/post/204600/).
[Глупая сортировка и некоторые другие, поумнее](https://habrahabr.ru/post/204968/).
Временная сложность: Квадратичная, т.е. O(n2).

## Перемена мест (swap)
Дополнительно может возникнуть вопрос, а как же можно поменять значения местами?
Существует несколько способов.
**Первый и самый понятный**: использование промежуточной переменной.
**Второй вариант**: XOR SWAP (см. [How does the XOR (^) swap algorithm work?](https://stackoverflow.com/questions/21093606/how-does-the-xor-swap-algorithm-work))
```
a = a^b;
b = a^b;
a = a^b;
```
**Третий вариант**: "математические костыли"
```java
int x=2;
int y=4;
y=(x+y)-(x=y);
```

## Сортировка вставками (Insertion Sort)
Ещё одним простым способом сортировки является сортировка вставками.
Отличное описание приведено в статье "[В мире алгоритмов: Сортировка Вставками](https://m.habrahabr.ru/post/181271/)".
Суть до ужаса проста. Перемещаемся слева направо. Каждый элемент сравнивае с элементами слева в поисках того места, в которое можно как-бы "вставить" обрабатываемый элемент.
Поэтому и называется способ: сортировка вставками. В выше указанной статье приведён хороший бытовой пример: сортировка денег в кошельке.
Временная сложность: Квадратичная, т.е. O(n2).

Так же можно посмотреть про сортировку вставками тут: "[Сортировка массива](https://edunow.su/site/content/algorithms/sortirovka_massiva)"

## Быстрая сортировка (Quick Sort)
Более сложным алгоритмом сортировки является алгоритм под названием: Быстрая сортировка. Она же сортировка Хоара.
Интересно, что алгоритм был придуман Хоаром во время его пребывания в Советском Союзе, где он обучался в Московском университете компьютерному переводу и занимался разработкой русско-английского разговорника.

Хороший и подробный разбор представлен в статье на medium.com: "[Информатика в JavaScript: Быстрая сортировка (Quicksort)](https://medium.com/devschacht/nicholas-c-zakas-computer-science-in-javascript-quicksort-afa07c0a47f0)".

Как в старых добрых задачах. Из пункта А в пункт Б направился маркер. Ему на встречу из пункта Б в пункт А направился другой маркер )

Определены начальный элемент ``first`` и ``last`` - границы, в которых мы работаем. При первой итерации мы имеем не разделённый (логически) массив, поэтому они равны началу и концу массива.


Выбирается опорный элемент (значение элемента массива ```source```), который называют **pivot**:
``` int pivot = source[(first + last) / 2]; ```

Выполняем действия в рамках цикла, **do - while**

Сначала двигаем левый маркер (А). Двигаем, пока его **значение** не станет или больше чем pivot (т.е. требуется перенести элемент вправо), или пока мы не дойдём до самого pivot (т.е. переносить нечего):
``` while (source[leftMarker] < pivot) ```

Потом двигаем правый маркер (Б). Двигаем, пока его **значение** не станет или меньше чем pivot (т.е. требуется перенести элемент влево), или пока мы не дойдём до самого pivot (т.е. переносить нечего):
``` while (source[rightMarker] > pivot) ```

Далее, проверяем, что левый маркер или не дошёл до правого маркера, или они стоят в одном месте: ``` if (leftMarker <= rightMarker) ```
При этом, если левый маркер не дошёл до позиции правого, значит найдены значения для перемещения. Поэтому при ``` if (leftMarker < rightMarker) ``` выполнить замену.
В рамках условия leftMarker <= rightMarker так же увеличиваем каждый маркер на 1.

Выполняем эти действия пока левый маркер меньше или равен правому:
``` while (leftMarker <= rightMarker) ```

Далее мы завершили выполнение для текущей итерации по текущему размеру массива (в самый первый раз, как мы помним, от 0 элемента до последнего).
У нас есть 2 маркера.
Выполняем повторную итерацию по отрезку: от левого маркера до конечной границы (``last``).
Выполняем повторную итерацию по отрезку: от начальной границы ``first`` до правого маркера.
Условие для начала итераций: позиция маркера меньше, чем позиция границы.

При помощи рекурсии выполняются действия для новых отрезков, обозначенными границами прошлой итерации + положением маркера.

## Материалы
Все указанные сортировки описаны здесь: "[Сортировка массива](https://edunow.su/site/content/algorithms/sortirovka_massiva)"
Визуализация алгоритмов:
[sorting.at](http://sorting.at/)
[visualgo.net](https://visualgo.net/en/sorting)
[Бесплатный курс на Coursera](https://www.coursera.org/learn/algorithms-part1)
[Видеолекции курса «Алгоритмы и структуры данных» от Яндекс](https://yandexdataschool.ru/edu-process/courses/algorithms)