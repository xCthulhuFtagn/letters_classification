# letters

# Дано:

Здоровенная картинка. На ней большое количество букв, которые могут быть перевернуты. 
Картинка для каждого студента генерируется персонально. И через небольшое количество времени после создания репозитория будет добавлена в репозиторий ботом.

### Шрифты
Список шрифтов, которые могут попасться. Все эти шрифты есть в колабе. В одной картинке все буквы нарисованы одним типом шрифта.
```python
font_list = [ 
    '/usr/local/lib/python3.10/dist-packages/matplotlib/mpl-data/fonts/ttf/DejaVuSans-Bold.ttf',
    '/usr/local/lib/python3.10/dist-packages/matplotlib/mpl-data/fonts/ttf/DejaVuSansMono-Bold.ttf',
    '/usr/local/lib/python3.10/dist-packages/matplotlib/mpl-data/fonts/ttf/DejaVuSansMono.ttf',
    '/usr/local/lib/python3.10/dist-packages/matplotlib/mpl-data/fonts/ttf/DejaVuSans.ttf',
    '/usr/local/lib/python3.10/dist-packages/matplotlib/mpl-data/fonts/ttf/DejaVuSerif-Italic.ttf',
    '/usr/local/lib/python3.10/dist-packages/matplotlib/mpl-data/fonts/ttf/DejaVuSerif.ttf',
 ]
 
import random
from PIL import Image, ImageDraw, ImageFont
import matplotlib.pyplot as plt

font = ImageFont.truetype(random.choice(font_list), size=random.randint(100, 200))
font
 ```
 
Если при подгрузке шрифтов возникает ошибка `resource not found`, проверьте версию питончика `!python --version` и проставьте соответствующее значение в пути к шрифтам. Например `/usr/local/lib/python3.10/` -> `/usr/local/lib/python3.12/`

Размер шрифта для каждой буквы рандомный, от 100 до 200.

**Цвет букв**
```python
color = (random.randint(0, 200), random.randint(0, 200), random.randint(0, 200))
```

**Цвет кружков**
```python
color = (random.randint(0, 200), random.randint(0, 200), random.randint(0, 200), random.randint(50, 70))
```

Всего на картинке 10к букв. 

**Нужно: посчитать количество раз, которое встречается каждая буква и закоммитить результат в файл** `letters.csv`


* предобработать исходное изображение, выделить из него буквы отдельно
* разметить или сгенерировать обучающий датасет
* обучить модель на вашем датасете
* протестировать на тестовой выборке и подготовить сабмишн

### Предобработка

* Есть ли какой-то паттерн, какой угол наклона у разных букв? Попробуем вывести формулу наклона для всех букв для начала для первой строки, для первого столбца, потом для второго и найдите закономерность.

### Поиск границ буквы

Обратим внимание, что размер картинки кратен количеству букв и по вертикали, и по горизонтали. Заметив это, можно выделить область, где гаранитрованно есть одна и только одна буква. В рамках этой области смещение буквы будет рандомным. Угол наклона буквы не рандомный, см предыдущий пункт.

Еще в каждой области буквы может быть от 10 до 40 кружочков -- это зашумление, чтобы усложнить задачку


### Обучение модели

Обучим классификатор на свертках

* Обратим внимание, что размер шрифта может быть тоже разным (от 100 до 200)
* Какие аугментации будем использовать?
* Какие аугментации не стоит использовать?
* Имеет ли смысл использовать предобученную модель? (скорее всего, нет)
* Как отследить переобучение?
