# Сабмит лежит в `test_results/test.csv`

# Основная модель в `3.baseline+interactions.ipynb`


# Комментарии к заданию

Формат имен признаков:
Ni_rec – извлечение никеля в готовый никелевый продукт, концентрат (значение может отсутствовать, валидны только меньше 1 и больше 0),
Ore, oreth – имена, которые означают признаки рудного сгустителя (Ore thickener) и на входе первой ФМ (напомним, ФМ – флотомашина),
resth – имена, которые означают признаки сгустителя с готовым никелевым продуктом (Final Ni thickener).
Физические характеристики: Mass (масса), Dens (плотность), Vol (объём), Ni (никель), Cu (медь), AU (флаг автоуправления, если оптимизатор управления ФМ включен, то равен 1 – фактические диапазоны на этой ФМ актуальны, в противном случае диапазонам не следует доверять, так как не обновлялись после выключения оптимизатора)
Суффиксы имён ФМ (положения в цепи агрегатов): 1.1, 1.2, …, 6.2 (см Схему флотации).
Суффиксы продуктов: F – питание ФМ, C – концентрат ФМ, T – хвосты ФМ.
Суффиксы границ фактических диапазонов, которые были выставлены технологом для оптимизатора ФМ: min, max.

Требуется заполнить файл test.csv, указав границы диапазонов признаков (20 признаков => 40 значений границ) для выбранных моментов времени. Эти таймстемпы – 20 непрерывных временных отрезков с 15-минутной дискретностью. Каждый отрезок –тест-кейс, который будет оцениваться отдельно.
Обратите внимание, что файл test.csv нужно загрузить в ваш Github (или другую систему VCS) в следующем формате: Папка test_results, файл test.csv

Важно! Границы фактического диапазона в файле исходных данных – значения, которые выставляли технологи производства для сервиса оптимизации флотации (по одному на каждую линию флотомашины, например, оптимизатор для ФМ1.1.), чтобы этот оптимизатор генерировал воздействия на рычаги управления флотацией на ФМ, которые обеспечат сходимость к середине этого диапазона. Обратите внимание, что сами границы, как и ширина диапазона – плод интеллектуального труда и фантазии технологов, которые работают посменно. Технолог ведёт процесс, наблюдает за большим кол-вом параметров и не всегда уделяет достаточное внимание оптимизатору и этим диапазонам – учитывайте человеческий фактор! Наиболее релевантные значения – при включении оптимизатора (см смену значения признака с суффиксом AU с 0 на 1). 
В данной задаче все границы фактических диапазонов (40 параметров типа min, max) для каждой 15-минутки ставим под сомнение и предлагаем вам сгенерировать свои варианты с учётом ограничений:
Ограничение 1. Каждый диапазон (признаки min, max) можно изменить не чаще 1 раза в 2 часа (не менее 8 15-минуток подряд с одной и той же парой значений границ).
Ограничение 2. Наименьшие допустимые приращения признаков min, max зависят от продукта, металла и ФМ (и одинаковы для двух линий одной ФМ). В качестве приращений используйте только кратные им значения (например, если наименьшее допустимое – 0.1, используйте 0.1, 0.2, 0.3, …):
Ni_1.*C – 0.1,
Cu_1.*C – 0.1,
Cu_2.*T – 0.01,
Cu_3.*T – 0.05,
Ni_4.*T – 0.01,
Ni_4.*C – 0.05,
Ni_5.*T – 0.01,
Ni_5.*C – 0.05,
Ni_6.*T – 0.01,
Ni_6.*C – 0.05.


# Получить: 

1) заполненный test, чтоб мы прогнали автопроверки на заведомый бред (много Null и копипасту жёсткую из train)
2) разработанный алгоритм, модель как-то описанную и представленую
3) код обучения модели, чтоб не чёрный ящик
 

