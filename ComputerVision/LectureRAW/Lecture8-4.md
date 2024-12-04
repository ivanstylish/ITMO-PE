## [MainPage](../../index.md)/[Computer Vision](../README.md)/[Lecture](../Lecture.md)/8-4 RAW

语音识别：Sonix.ai  
断句与标点：chatGPT 4o  
翻译：chatGPT 4o  

Теперь поговорим об алгоритмах стереосопоставления. Для начала отметим, что большинство алгоритмов подразумевают некоторые исходные предположения об окружающем мире, то есть некоторые упрощения, которые позволяют нам игнорировать некоторые реальные явления, происходящие в реальном мире на трёхмерной сцене, снимки которой мы получаем с помощью нашей стереопары, но при этом не учитываемых в нашей модели. Это незначительно влияет на точность наших результатов, но позволяет существенно упростить наши вычисления.  
现在我们来谈谈立体匹配算法。首先，我们注意到，大多数算法都假设关于周围世界的一些初始假设，即一些简化，这些简化使我们可以忽略在三维场景中发生的一些实际现象，这些场景的照片是通过我们的立体相机获得的，但这些现象在我们的模型中没有被考虑到。这对我们的结果准确性影响不大，但却大大简化了我们的计算。

Среди таких упрощений — предположение о ламбертовых поверхностях, то есть мы предполагаем независимость освещения поверхности от угла зрения. Конечно, не во всех контекстах это справедливо, но по умолчанию считается именно так. Данное предположение позволяет проще строить функцию соответствия между различными точками на изображениях, полученных с помощью нашей стереопары. Как правило, алгоритмы стереозрения вообще не учитывают законы распространения света.  
这些简化之一是关于朗伯特表面的假设，即我们假设表面的照明与视角无关。当然，并不是在所有情况下都是如此，但默认情况下是这样认为的。这个假设使我们能够更容易地构建通过我们的立体相机获得的图像上的不同点之间的对应函数。通常，立体视觉算法完全不考虑光传播的规律。

Также присутствует предположение о том, что поверхности точно гладкие. Это означает, что чаще всего расхождение в интенсивности соседних пикселей небольшое в реальном мире. Ещё одним предположением является, что камеры откалиброваны. Эту манипуляцию мы всегда можем произвести априори с нашим комплексом. Таким образом, настраиваем параметры внутренней и внешней калибровки, то есть положение нашей стереопары в системе координат мира, а также настраиваем фокусное расстояние и фиксируем его в каждой камере. Ну и другие оптические параметры в зависимости от устройства камер.  
另一个假设是，表面是完全光滑的。这意味着在现实世界中，邻近像素的强度差异通常很小。还有一个假设是相机已经校准。我们总是可以先验地进行这项操作。因此，我们设置了内部和外部校准参数，即立体相机在世界坐标系中的位置，还设置了焦距并将其固定在每台相机中，以及其他根据相机设备而变化的光学参数。

Многие алгоритмы подразумевают ограничение упорядоченности. Это значит, что если на левом изображении точки идут слева направо в каком-то порядке, то на правом изображении они следуют в том же порядке. Также большинство алгоритмов требует ректификации изображений, то есть выполнения преобразования, при котором и правое, и левое изображение проецируются на плоскость, параллельную базовой линии, то есть линии, соединяющей оптические центры камер. Тогда, если пара (x, y) — это точка левой проекции, а (x', y') — соответствующая ей точка правой проекции, то y = y'.  
许多算法假设顺序限制。这意味着，如果左图像上的点按照某种顺序从左到右排列，那么在右图像上它们也会按照相同的顺序排列。此外，大多数算法要求对图像进行校正，即进行转换，使左图像和右图像都投影到与基线平行的平面上，即连接相机光学中心的直线上。这样，如果(x, y)是左图像中的一个点，而(x', y')是对应的右图像中的点，则y = y'。

Мы уже рассматривали один из методов ректификации в нашей лекции. Ещё одним распространённым требованием является соответствие границ интенсивности и резких перепадов функции расхождения. Это значит, что на границах объектов интенсивность меняется достаточно резко. Ещё почти все алгоритмы предполагают, что каждому пикселю одного изображения соответствует пиксель у другого. В противном случае он считается зашумлённым. Впрочем, некоторые алгоритмы игнорируют работу с такими пикселями сами.  
我们已经在讲座中讨论过一种校正方法。另一个常见的要求是强度边界和急剧变化的对应。这意味着在对象边界处，强度变化非常剧烈。几乎所有算法还假设一个图像的每个像素在另一个图像中都有一个对应的像素。否则它被认为是噪声。不过，一些算法会忽略这些噪声像素。

Перейдём теперь к описанию простого алгоритма стереосопоставления. Данный алгоритм использует ректифицированные изображения. Само же соответствие вдоль выбранных строк производится путём поиска минимума или максимума функции отклика в зависимости от задания функции отклика, которая сопоставляет каждой точке определённое значение в зависимости от значения интенсивности пикселя в её окрестности. Иллюстрация данного подхода показана на слайде.  
现在我们来描述一个简单的立体匹配算法。该算法使用校正后的图像。沿选定的行的对应通过搜索响应函数的最小值或最大值来进行，具体取决于响应函数的设置，该函数根据像素周围的强度值为每个点分配一个特定值。这种方法的示例在幻灯片中显示。

Отметим, что алгоритм наивного стереосопоставления не идеален. Он склонен порождать артефакты из-за зашумлённых пикселей, самой природы сканирования общего окна и ещё массы других причин. Пример изображения с наличием множества артефактов приведён на слайде. Зачастую устранение подобных артефактов производится с помощью постобработки, но их возможно изначально избежать с помощью использования более продвинутых методов, которые мы рассмотрим далее.  
需要注意的是，简单的立体匹配算法并不完美。它容易因为噪声像素、扫描窗口的本质以及许多其他原因而产生伪影。一个包含许多伪影的图像示例在幻灯片中显示。通常，通过后处理来消除这些伪影，但可以通过使用更先进的方法来避免它们，我们将在后面讨论这些方法。

Одним из подходов, позволяющих усовершенствовать процесс сопоставления, является использование Disparity Space Image (DSI), то есть изображения пространства расхождения. Данное изображение представляет собой структуру, позволяющую использовать различные методы, в том числе методы динамического программирования, для более точного сопоставления точек в процессе стереосопоставления ректифицированных пар изображений. DSI содержит в качестве столбцов векторы функции отклика, что позволяет накапливать информацию о соответствии пикселей рассматриваемых изображений. Данная идея представлена на слайде.  
一种改进匹配过程的方法是使用视差空间图像(DSI)，即视差图像。该图像是一种结构，允许使用各种方法，包括动态规划方法，更准确地匹配校正后的图像对中的点。DSI包含作为列的响应函数向量，这使得积累关于匹配像素信息成为可能。这种方法的示例在幻灯片中显示。

Теперь реализуем рассмотренную только что идею DSI. Возможно построить по формуле, представленной на слайде. Здесь X — это координата вдоль соответствующей оси, i — это номер строки, I и I' — это изображения, полученные из камер рассматриваемой стереопары, d — это смещение вдоль строк ректифицированных изображений. Следует отметить, что DSI можно строить не только по этой формуле. Возможно учитывать не само значение в точках, а функцию на основе корреляции окрестностей.  
现在实现刚才讨论的DSI概念。可以根据幻灯片中显示的公式构建DSI。在这里，X是沿相应轴的坐标，i是行号，I和I'是从立体相机获得的图像，d是沿校正后图像行的视差。需要注意的是，DSI不仅可以根据这个公式构建。还可以考虑基于周围区域相关性的函数值。

После построения DSI происходит отбрасывание строк, которые соответствуют заведомо невозможным значениям. Например, невозможные значения смещения могут возникнуть из условия того, что пиксель на левом изображении должен быть правее соответствующего ему на правом. Таким образом, задача сводится к поиску оптимального пути на полученной двумерной матрице. Имеется в виду задача стереосопоставления. То есть мы построили DSI, отмели области, которые отвечают за невозможные смещения, и решаем задачу поиска оптимального пути на двумерной матрице. Кусок подобной матрицы представлен на изображении.  
在构建DSI之后，去除对应于显然不可能值的行。例如，不可能的视差值可能由于以下条件产生：左图像上的像素应位于右图像对应像素的右侧。因此，问题归结为在得到的二维矩阵中寻找最佳路径。这是指立体匹配问题。也就是说，我们构建了DSI，去除了对应于不可能视差值的区域，然后解决在二维矩阵中寻找最佳路径的问题。矩阵的一部分示例在图像中显示。

При этом за каждый тип движения назначается определённый штраф. При поиске оптимального пути типы движения бывают по горизонтали, по вертикали и по диагонали. Последние два типа соответствуют зашумлённым областям, то есть присутствующим только на одном из изображений стереопары. Здесь следует отметить, что если некоторая поверхность на левом изображении имеет ширину девять пикселей, а на правом три пикселя, то в такой терминологии пиксель из изображения слева соответствует трём пикселям справа — это могут быть третий, шестой и девятый. Остальные шесть считаются шумом. Описанная только что задача решается методами динамического программирования.  
在此过程中，每种移动类型都会指定一个特定的惩罚。在寻找最佳路径时，移动类型可以是水平的、垂直的或对角线的。后两种类型对应于噪声区域，即仅存在于立体图像对中的一个图像上的区域。这里需要注意的是，如果左图像上的某个表面宽度为九个像素，而右图像上的宽度为三个像素，那么在这种术语中，左图像上的一个像素对应右图像上的三个像素——可能是第三、第六和第九个。其余六个像素被认为是噪声。上述问题通过动态规划方法解决。

Теперь рассмотрим сам алгоритм поиска кратчайшего пути по допустимой области, которую мы выделили. Пример данной области представлен на слайде. Здесь горизонтальная ось — это ось x, вертикальная ось — это ось y, то есть ось смещения. Чёрные пиксели соответствуют близким к нулю значениям. Скачки в I' соответствуют зашумлённым областям. Горизонтальные участки означают нахождение точного соответствия. Наклонные участки соответствуют наклонным поверхностям. Если на изображении заранее известны точки, положения которых возможно определить достаточно точно, то количество возможных путей сокращается за счёт использования ограничения, основанного на том, что путь должен проходить так, чтобы он не противоречил расстановке таких точек.  
现在我们来讨论在选定区域内寻找最短路径的算法。选定区域的示例在幻灯片中显示。这里水平轴是x轴，垂直轴是y轴，即视差轴。黑色像素对应于接近零的值。I'中的跳跃对应于噪声区域。水平段表示精确匹配。斜线段表示倾斜表面。如果图像上事先已知一些点，其位置可以相当准确地确定，那么可以通过使用基于路径必须通过这些点的限制来减少可能路径的数量。

Возможны также многозначные соответствия, то есть случаи, когда точке одного изображения может соответствовать одна точка из небольшого набора вариантов на другом изображении. Одна из главных особенностей рассматриваемого нами метода заключается в том, что каждая строка обрабатывается независимо, что имеет очевидный негативный эффект. Функция глубины пикселя может иметь вид "гребёнки". Однако положительным моментом является возможность параллелизации вычислений. Из эмпирических опытов следует, что основное время, как правило, тратится на построение DSI, в частности, на вычисление корреляции. Чтобы уменьшить эффект "гребёнки", возможно использовать следующую методику: заранее каким-либо образом выделить границы на изображениях, например, по резкому перепаду интенсивности с помощью техник, которые мы рассматривали ранее в курсе. Таким образом, границам объектов на DSI соответствуют вертикальные и диагональные линии. Тогда стоимость пути уменьшается, если он проходит по этим линиям.  
还可能存在多值匹配的情况，即一个图像上的点可以在另一个图像上的一小组选项中对应一个点。我们讨论的方法的一个主要特点是每行独立处理，这显然有负面影响。像素的深度函数可能呈现“梳子”形状。然而，正面的一点是可以并行化计算。经验表明，主要时间通常花在构建DSI上，特别是计算相关性。为了减少“梳子”效应，可以使用以下方法：预先通过某种方式在图像上标记边界，例如，通过使用我们在课程中先前讨论的技术对强度的急剧变化进行标记。因此，DSI上的对象边界对应于垂直和对角线。这样，如果路径经过这些线，其成本将减少。

Ну и напоследок нельзя не сказать, что хоть мы и рассмотрели стиль работы пассивной стереопары в рамках нашей лекции, но всё же современные методы стереосопоставления, как и другие методы компьютерного зрения, всё чаще решаются с помощью нейросетевых инструментов. Например, Pyramidal Stereo Matching Network производит построение DSI, используя данные из feature extractors, объединение характерных признаков, а также специальные модули, строение которых можно видеть на слайде. Для определения диспаритета существуют и другие методы, основанные на нейросетях, но все они примерно действуют по одному и тому же принципу: происходит извлечение признаков, их обработка и различные преобразования в блоках комбинированных сверхмощных архитектур. С множеством подобных архитектур вы можете ознакомиться самостоятельно.  
最后需要提到的是，尽管我们在讲座中讨论了被动立体相机的工作方式，但现代立体匹配方法和其他计算机视觉方法越来越多地使用神经网络工具。例如，Pyramidal Stereo Matching Network使用特征提取器的数据构建DSI，结合特征以及可以在幻灯片中看到的特殊模块的结构。为了确定视差，还存在其他基于神经网络的方法，但它们大致遵循相同的原则：提取特征，对其进行处理，并在组合的强大架构模块中进行各种转换。您可以自行了解这些架构的详细信息。

На этом лекция закончена. Спасибо за внимание.  
本讲座到此结束。感谢您的关注。