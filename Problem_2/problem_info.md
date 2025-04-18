# **Задача: Расчет параметров запуска группировки спутников (50 баллов)**

## **Условие задачи**

Компания "SpaceY" запускает уникальную **спутниковую группировку** для мониторинга экватора. Спутники будут собирать данные о состоянии океана, его уровне, солености и течениях, обеспечивая регулярное и точное обновление информации. Это позволит не только повысить точность климатических прогнозов, но и помочь в решении глобальных экологических проблем, таких как изменение климата и повышение уровня моря.

Для выполнения миссии необходимо, чтобы спутники двигались по **периодическим** траекториям (в проекции на поверхность Земли), с точностью до километра на экваторе. Это требует точного подбора начальных данных — радиус-вектора и скорости аппарата. Нас также интересует информация об уровне океана на всей земной поверхности, а значит сетка, образуемая подспутниковыми траекториями (расстояние между точками пересечения линии экватора и граундтреков), должна быть регулярной  и достаточно **мелкой** – на экваторе расстояние между подспутниковыми треками не должно превышать **200 км**. Задача — определить **минимальное** количество аппаратов и их **начальные скорости** так, чтобы получилась группировка, удовлетворяющая поставленным требованиям (движение аппаратов — пассивное).


## **Подробное описание задачи**

### **Постановка задачи**
Задачу предлагается решать в следующих постепенно усложняющихся постановках:
1. Все аппараты движутся в рамках **задачи двух тел**. На их начальные данные не накладывается никаких дополнительных ограничений.
2. Все аппараты движутся в рамках **задачи двух тел**. Для оптимизации выведения **плоскости их орбит** (долгота восходящего узла в начальный момент) должны **совпадать**.
3. Все аппараты движутся в модели гравитации, которая учитывает влияние **второй зональной гармоники** $J_2$. На их начальные данные не накладывается никаких дополнительных ограничений.
4. Все аппараты движутся в модели гравитации, которая учитывает влияние **второй зональной гармоники** $J_2$. Для оптимизации выведения **плоскости их орбит должны быть близки** (разница между долготами восходящих узлов должна составлять не более 0.1 градуса)

### **Общие ограничения для каждой постановки:**

Высоты орбит аппаратов не должны выходить за пределы 400-600 км (это связано с наличием остаточной атмосферы Земли и ограничениями на энергопотребление радара)

Орбиты будем полагать околокруговыми с одинаковыми радиусами, с наклонение равным $98^{\circ}$. Также будем полагать, что гравитационный параметр Земли $\mu=398600.4415 \cdot 10^9\, \text{м}^3/\text{с}^2$, радиус Земли $R = 6371302 \, \text{м}$, скорость вращения Земли $\omega_E = 7.29211\cdot 10^{-5} \, \text{c}^{-1}$ (в начальный момент времени считаем, что инерциальная система координат и система координат, связанная с Землей, совпадают), коэффициент второй зональной гармоники $J_2 = 1082.8\cdot 10^{-6}$, для расчета подспутниковой точки Земля считается сферой указанного выше радиуса. 

### **Требования к решению**

1. Найти минимальное количество аппаратов, которые решают поставленную задачу (периодичность измерений, то есть период граундтреков, не более 100 часов, расстояние между треками на экваторе не более 200 км, восходящий и нисходящий трек считаются разными)
2. Найти начальные данные для каждого аппарата (радиус-вектор и скорость аппарата относительно инерциальной системы отсчёта), обеспечивающие периодичность и равномерность подспутниковых треков
3. Визуализировать получающиеся треки на поверхности Земли

## **Формат выходных данных**

В качестве выходных данных вы указываете начальные радиус-вектора и скорости каждого аппарата в инерциальной системе координат, а также результаты моделирования их движения для интервала времени, равного восьми суткам (сохраняем их положение и скорость каждую минуту). Также вы должны приложить файл с визуализацией треков на карте Земли. 

Выходные данные для каждого из пунктов:

1. Картинка с траекториями на всей поверхности Земли. Картинка с траекториями на части Земли, соответствующей восточной долготе [0;30] градусов и широтам [-20;20] градусов (допустимые форматы: .png, .bmp, .jpg, .tiff)

2. Начальные данные (радиус-вектор и скорость, формат double, ~15 значащих цифр), и количество витков, соответствующее периоду. 

3. .csv-файл, разделители – запятые, децимальный символ – точка, порядок данных (по строкам): $t, x_1, y_1, z_1, v_{x_1}, v_{y_1}, v_{z_1}, \dots, x_N, y_N, z_N, v_{x_N}, v_{y_N}, v_{z_N}$. Данные для каждого аппарата сохраняются каждые 60 секунд, единицы измерения – метры, килограммы, секунды. Для вычислений использовать переменные типа double, сохранять можно 8 значащих цифр. Интервал интегрирования – 120 часов.

4. Также от вас потребуется некоторое обоснование выбранной методики построения орбит.

## **Список источников**

1. *Овчинников М.Ю.* Введение в динамику космического полета
2. *Мирер С.А.* Механика космического полета. Орбитальное движение. Часть 1
3. *Мирер С.А.* Механика космического полета. Орбитальное движение. Часть 3
4. *Иванов Д.С., Трофимов С.П., Широбоков М.Г.* Численное моделирование орбитального и
углового движения космических аппаратов