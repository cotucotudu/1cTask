# 1cTask

Задача заключалась в поиске градиентных элементов-прямоугольников. 
На вход получаем пиксельное изображение, на выход -- прямоугольники площадью не меньше 9 пикселей, заданные своими верхним левым и нижним правым углом, в которых выполняется следующий критерий градиентной заливки:

Критерий:
для каждого пикселя и для каждой его компоненты цвета последовательность компонент цвета - монотонная по вертикали и по горизонтали внутри прямоугольника


В HandingIN.ipynb работа происходит с pixilbig.png, его можно скачать из репрозитория или заменить другой пиксельной картинкой. Надо заменить "Downloads/pixilbig.png" на путь к картинке, с которой происходит работа.

Для каждого пикселя и для каждой компоненты цвета мы получаем сначала вертикальные, а потом горизонтальные монотонные максимальные по длине подпоследовательности, заканчивающиеся в данном пикселе. Результаты для вертикальных подпоследовательностей сохраняются в Result2, а для горизонтальных -- в Result1.
Механизм получения максимальной монотонной подпоследовательности таков: для первой цветовой компоненты получаем максимальную по длине невозрастающую подпоследовательность, заканчивающуюся в определенном пикселе и максимальную по длине неубывающую подпоследовательность. Из них мы выбираем максимальную по длине и получаем максимальную по длине монотонную подпоследовательность, заканчивающуюся в определенном пикселе. Когда этот поиск происходит для следующей цветовой компоненты, мы сравниваем длины для двух цветов и находим минимальную длину монотонной подпоследовательности, заканчивающейся в каждом пикселе уже по двум цветам. Затем аналогично и по третьей цветовой компоненте.

После заполнения Result1 и Result2 нам необходимо найти прямоугольники такие, что в них каждая строка будет строкой с монотонной последовательностью цветов (по всем трем компонентам). Для этого мы выбираем левый верхний угол, из него идем по горизонтали и находим правую границу по первой строке (после правой границы последовательность перестает быть монотонной), затем то же самое делаем для вертикали и находим нижнюю границу по первому столбцу. Повторяем действия для всех строк и столбцов внутри образовавшегося прямоугольника. Переходим на следующую строку и теперь начинаем прямоугольники из нового верхнего левого угла

В вывод попадут прямоугольники, соответствующие критерию и имеющие площадь не больше 9 пикселей.
