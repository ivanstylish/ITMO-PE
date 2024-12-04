## [MainPage](../../index.md)/[Computer Vision](../README.md)/[Lecture](../Lecture.md)/RAW

语音识别：Youtube 转文本  
断句与标点：chatGPT 4o  
翻译：chatGPT 4o  

Мы рассмотрим далее некоторые примечательные частные случаи применения архитектуры GAN, то есть некоторые конкретные архитектуры, которые попадают под эту схему. Начнем, пожалуй, с Conditional GAN или условных генеративно-состязательных сетей. Данная модифицированная версия GAN позволяет добавлять некоторые дополнительные условия в генераторы и дискриминаторы. Эти условия могут содержать любую информацию, например, метку класса изображения или данные других моделей, в общем, все, что может позволить контролировать процесс генерации данных. Например, можно подавать дополнительный параметр как условие на класс при генерации чисел, например, в датасете типа MNIST.  
我们将进一步讨论一些显著的GAN（生成对抗网络）架构的具体应用案例。首先，我们从条件GAN（Conditional GAN，简称CGAN）开始。这种改进版的GAN允许在生成器和判别器中添加一些额外的条件。这些条件可以包含任何信息，例如图像的类别标签或其他模型的数据，总之，任何能够控制数据生成过程的东西。例如，在生成MNIST数据集中的数字时，可以将附加参数作为生成条件。

Создание таких картинок с передачей картинки в качестве дополнительного условия является задачей трансляции изображений. Как уже было упомянуто, на вход генератору и дискриминатору подается дополнительная информация. Например, в случае с многослойным перцептроном условия могут быть представлены дополнительными входными параметрами в виде дополнительного входного слоя. В генераторе априорная вероятность шума комбинируется в объединенное скрытое представление, и генератор и дискриминатор пытаются оптимизировать целевую функцию или функцию потерь. Когда дискриминатор меняет свое поведение, то и генератор его меняет, и наоборот. То есть процесс обучения и его семантический смысл не меняются. При этом дополнительные данные в генераторе и дискриминаторе представляются как расширение входных параметров.  
将图像作为附加条件传递来生成这些图像的任务称为图像翻译。如前所述，生成器和判别器会接收附加信息。例如，对于多层感知器，这些条件可以作为额外的输入参数通过额外的输入层表示。在生成器中，噪声的先验概率被组合成一个联合的隐层表示，生成器和判别器尝试优化目标函数或损失函数。当判别器改变其行为时，生成器也会相应地改变，反之亦然。即，训练过程及其语义意义不变。同时，生成器和判别器中的附加数据被表示为输入参数的扩展。

Когда речь идет о Conditional GAN (или CGAN), задача оптимизации будет выглядеть согласно формуле, представленной на слайде. В качестве примера использования данной архитектуры можно рассмотреть задачу генерации рукописных цифр. При создании изображения в генератор поступает скомбинированная информация: два параметра - обычный параметр y, задающий метку класса (мы условились, что говорим про генерацию цифр на примере MNIST), и вектор шума, как, собственно говоря, в классическом GAN. На выходе из генератора образуется изображение, полученное с помощью транспонированной свертки. Затем полученное изображение комбинируется с меткой и поступает в дискриминатор, который, в свою очередь, применяет свертки, чтобы получить полносвязанный слой. Наконец, анализируя полученную информацию с помощью полносвязанного слоя, дискриминатор принимает решение, является ли изображение сгенерированным.  
在条件GAN（CGAN）的情况下，优化任务会根据公式进行。CGAN的一个应用示例是生成手写数字。在生成图像时，生成器接收组合信息：两个参数——一个是普通参数y，指定类别标签（例如MNIST数据集中的数字生成），另一个是噪声向量，就像经典的GAN一样。生成器输出的图像通过转置卷积生成。然后，生成的图像与标签结合并传递给判别器，判别器使用卷积来获取全连接层。最后，判别器通过全连接层分析接收到的信息并决定图像是否是生成的。

Вы сейчас описали классическую свёрточную архитектуру генерации изображений с рукописными цифрами с помощью архитектуры CGAN. Также используя условные порождающие состязательные сети или CGAN, можно научиться генерировать текст по картинке и наоборот. В качестве параметра в данном случае возможно передавать изображение, которое будет описано. Более того, для такого типа нейронных сетей, принимающих в качестве параметра дополнительные параметры, можно осуществлять обусловливание. Например, можно передавать изображение местности, и в результате может быть получено аналогичное изображение этого места зимой, летом, днем или ночью. Такая задача является задачей трансляции изображений.  
你现在描述的是经典的卷积架构，通过CGAN生成手写数字图像。通过使用条件生成对抗网络（CGAN），还可以学习根据图像生成文本，反之亦然。在这种情况下，参数可以是要描述的图像。此外，对于这种接受附加参数的神经网络，可以进行条件化。例如，可以传递一个地区的图像，结果可能会生成该地区在冬天、夏天、白天或夜晚的类似图像。这种任务是图像翻译任务。

Теперь мы рассмотрим DCGAN. DCGAN представляет собой модификацию подхода GAN, которая использует в своей основе глубокие свёрточные нейросети. Следует отметить, что задача поиска удобного представления признаков на больших объемах и размеченных данных является одной из наиболее активных сфер исследований, в частности представления изображений и видео. Одним из удобных способов поиска представлений может быть DCGAN. Использование свёрточных нейронных сетей напрямую не давало хороших результатов, поэтому были внесены ограничения на слои свёрток. Эти ограничения лежат в основе DCGAN, а именно: замена всех pooling-слоев на strided-свёртки в дискриминаторе и частично strided-свёртки в генераторе, что позволяет сетям находить подходящие понижения и повышения размерности. Во-вторых, это использование batch-нормализации для генератора и дискриминатора, то есть нормализация входа таким образом, чтобы среднее значение было равно нулю и дисперсия была равна единице. Следует использовать batch-нормализацию для выходного слоя генератора и входного дискриминатора. Далее, это удаление всех полносвязанных скрытых уровней для более глубоких архитектур. Помимо этого, используется ReLU в качестве функции активации в генераторе для всех слоев, кроме последнего, где используется Tanh. Использование Leaky ReLU в качестве функции активации в дискриминаторе для всех слоев. Помимо задачи генерации объектов, данный алгоритм хорошо показывает себя в извлечении признаков.  
接下来我们讨论DCGAN。DCGAN是GAN方法的修改版，它基于深度卷积神经网络。值得注意的是，在大规模标注数据上寻找合适的特征表示是研究的活跃领域之一，特别是图像和视频的表示。DCGAN可以作为寻找表示的一种方便方法。直接使用卷积神经网络并未取得良好的结果，因此对卷积层进行了限制。这些限制是DCGAN的基础，即：用步幅卷积替代判别器中的所有池化层，并在生成器中部分替代步幅卷积，这允许网络找到合适的降维和升维方式。其次，在生成器和判别器中使用批量归一化，即通过标准化输入使平均值为零、方差为一。生成器的输出层和判别器的输入层使用批量归一化。接着是删除所有全连接的隐藏层，以便实现更深的架构。此外，生成器的所有层使用ReLU作为激活函数，除了最后一层使用Tanh。判别器的所有层使用Leaky ReLU作为激活函数。除了生成对象的任务，该算法在特征提取方面也表现良好。

Теперь мы рассмотрим StackGAN. Само название данной архитектуры говорит об основной идее, которая в них заложена. Большинство из нас уже знакомы с выражением "стакать слои", то есть добавлять новые слои в нашу свёрточную архитектуру. Здесь используется та же идея, но на уровне уже не слоев, а последовательной обработки, точнее генерации изображения с помощью нескольких итераций последовательного применения различных архитектур. Итак, StackGAN - это порождающая состязательная сеть для генерации фотореалистичных изображений размером 256x256. Причем генерация происходит из текстового описания. Генерировать фотореалистичные изображения сразу сложно, поэтому и была придумана двухэтапная модель. На первой стадии данной архитектуры рисуются скетчи с примитивными формами и цветами, основанные на текстовом описании в низком разрешении. StackGAN принимает на вход изображения с первого этапа и текстовое описание и генерирует изображение в высоком разрешении с фотореалистичными деталями. Чтобы улучшить разнообразие синтезированных изображений и стабилизировать обучение, вместо conditional GAN использовался метод conditional augmentation. Ранее использовались CGAN, и, поскольку на вход можно было подавать условия, просто добавляя слои, увеличивающие размер изображения, достичь хороших результатов не удалось. Поэтому основной задачей было повысить разрешение изображений. Одной из ключевых особенностей архитектуры StackGAN является conditional augmentation, так как она позволила расширить количество примеров тренировочного сета путем небольших случайных изменений в исходных изображениях, что увеличивало многообразие данных.  
现在我们讨论StackGAN。这种架构的名字本身就揭示了其核心思想。大多数人已经熟悉“堆叠层”的概念，即在卷积架构中添加新层。同样的想法在StackGAN中使用，但在多次迭代的顺序处理中进行，即通过多次应用不同架构来生成图像。因此，StackGAN是一种生成对抗网络，用于生成256x256像素的照片级真实图像，生成是基于文本描述完成的。生成照片级真实图像直接很困难，因此设计了两阶段模型。在这种架构的第一阶段，根据文本描述绘制低分辨率的基本形状和颜色草图。StackGAN接收第一阶段的图像和文本描述，并生成高分辨率的照片级真实图像。为了提高合成图像的多样性和稳定训练，使用了条件扩增方法，而不是条件GAN。之前使用的是CGAN，由于可以输入条件，简单地通过添加层来增加图像尺寸，但未能取得良好效果。因此，主要任务是提高图像的分辨率。StackGAN架构的一个关键特点是条件扩增，因为它通过对原始图像进行小的随机改变来增加训练集示例的数量，从而增加了数据的多样性。

Далее мы рассмотрим LAPGAN. LAPGAN представляет собой генеративную параметрическую модель, которая представлена пирамидой Лапласа с каскадом свёрточных нейронных сетей. Внутри которой генерируется изображение постепенно, от исходного изображения с низким разрешением к изображению с высоким разрешением. На каждом уровне пирамиды обучается свёрточная генеративная модель, используя подход GAN. Такая стратегия позволяет декомпозировать задачу генерации изображений на последовательность уровней, что упрощает её решение. Теперь, после того как мы поговорили о процессе генерации в LAPGAN, поговорим еще о процессе его обучения. На самом деле идея довольно проста: мы берем исходное изображение с тренировочного датасета, а затем уменьшаем его и увеличиваем размер для получения низкочастотного изображения. Далее мы вычитаем его увеличенное изображение из исходного и получаем некоторый отпечаток с низкими частотами, то есть со значимой информацией. Именно такой отпечаток мы пытаемся генерировать с помощью нашего генератора и проделываем такую процедуру для различных разрешений. На каждом уровне тренируется дискриминатор, который различает сгенерированное изображение от реального низкочастотного. Применяя подобную схему на разных масштабах, мы тренируем нашу сеть.  
接下来我们讨论LAPGAN。LAPGAN是一种生成参数模型，由卷积神经网络级联组成的拉普拉斯金字塔表示。图像在其中逐级生成，从低分辨率的初始图像到高分辨率图像。在金字塔的每一层使用GAN方法训练卷积生成模型。这样的策略将图像生成任务分解为多个级别，使其更易解决。现在，在讨论了LAPGAN的生成过程之后，我们再讨论一下它的训练过程。实际上，想法非常简单：我们从训练数据集中取出原始图像，然后缩小并放大它以获得低频图像。然后，我们从原始图像中减去放大的图像，得到带有低频信息的图像，这些是我们试图通过生成器生成的内容。我们在不同分辨率上进行这种操作。每个层次训练一个判别器，以区分生成的低频图像和真实低频图像。通过在不同尺度上应用这种方案，我们训练了我们的网络。

Теперь мы рассмотрим еще одно очень популярное решение на основе GAN - именно CycleGAN. CycleGAN - это такой тип генеративно-состязательной сети, использующийся для переноса стиля изображения. CycleGAN можно обучить конвертировать изображение из одного домена в другой. Обучение выполняется без учителя, то есть не существует способа однозначного сопоставления изображений из обоих этих доменов при обучении сетей. Датасет на это не рассчитан и этого не предполагает. Данная сеть способна распознавать объекты на изображениях исходного домена и выполнять необходимые преобразования для соответствия внешнему виду объекта на изображениях целевого домена. Первоначальная реализация этого алгоритма была обучена превращению лошадей в зебр, яблок в апельсины и фотографий в картины. Результаты оказались потрясающими.  
接下来我们讨论基于GAN的另一个非常流行的解决方案——CycleGAN。CycleGAN是一种用于图像风格迁移的生成对抗网络。CycleGAN可以训练将图像从一个域转换到另一个域。训练是无监督的，即在训练过程中不存在这些域之间图像的一一对应关系。数据集并未设计或假设这一点。该网络能够识别源域图像中的对象并执行必要的转换，使其符合目标域图像的外观。最初的实现训练了将马变成斑马、将苹果变成橙子以及将照片变成画作的转换，结果令人惊叹。

Итак, рассмотрим подробнее саму архитектуру CycleGAN. CycleGAN состоит из двух GAN. Эти две сети обучаются одновременно и циклически, так что у них получается формировать соотношение между одними и теми же объектами и совершать соответствующие визуальные преобразования. На рисунке представлена общая архитектура циклической схемы обучения двух сетей. При обучении обе эти сети обучаются, то есть каждая из них состоит из генератора и дискриминатора. Дискриминатор со временем обучается различать реальные и имитированные изображения, а генератор будет обучен конвертировать входное изображение из исходного домена в целевой.  
让我们更详细地看看CycleGAN的架构。CycleGAN由两个GAN组成。这两个网络同时训练，并以循环方式训练，因此它们能够在同一对象之间形成关系并进行相应的视觉转换。图中展示了两网络循环训练的整体架构。在训练中，这两个网络同时训练，即每个网络由生成器和判别器组成。判别器会随着时间推移学习区分真实和模拟图像，而生成器将学习将源域图像转换到目标域。

Чтобы убедиться, что это преобразование имеет смысл, вводится условие восстановления. Это означает, что одновременно обучается другой набор, состоящий из генератора и дискриминатора, то есть второй GAN, который восстанавливает изображение в исходном домене из целевого домена. При этом соблюдается условие, что эта реконструкция должна быть похожа на исходное изображение. Вычисляется функция потерь, которую стремятся минимизировать в процессе обучения, обычно между исходным изображением и восстановленным применением второго GAN из сгенерированного. Данная схема чем-то похожа на автоэнкодер, за исключением того, что исходное изображение для восстановления оригинального ищется не в каком-то промежуточном слое из какого-то латентного представления, а из явно сгенерированного с помощью первого GAN изображения во втором домене.  
为了确保这种转换有意义，引入了恢复条件。这意味着同时训练另一个生成器和判别器组成的集合，即第二个GAN，从目标域中恢复原始域的图像。并且需要遵循一个条件，即这种重建应该类似于原始图像。计算损失函数并在训练过程中最小化，通常是在源图像与第二个GAN从生成图像恢复的图像之间进行。这个架构有点像自编码器，但不同的是，恢复原始图像并不是在某个中间层的隐表示中找到的，而是通过第一个GAN在第二个域中显式生成的图像中找到的。

CycleGAN отличается от стандартной парадигмы GAN тем, что он не генерирует изображение из случайного шума. CycleGAN использует данное изображение, чтобы получить другую версию этого изображения. Это перевод изображения в изображение, который позволяет CycleGAN превращать лошадь в зебру. Тем не менее, перевод изображения в изображение не является функцией, уникальной для CycleGAN, просто CycleGAN - одна из первых моделей, которая позволяет осуществлять это обучение с использованием непарного датасета. Это означает, что, как уже говорилось, не нужно иметь изображение, например, конкретной лошади и того, как эта лошадь будет выглядеть на том же снимке, только если бы она была зеброй. То есть не нужно парного сопоставления для обучения CycleGAN. В тренировочной выборке вместо этого можно иметь несколько лошадей и несколько зебр отдельно. Это полезно в ситуациях, когда невозможно получить парные данные. Например, если мы хотим иметь возможность генерировать версию зебры из лошади, нет смысла рисовать каждую лошадь как зебру, чтобы получить парные данные. Функция непарного преобразования изображения в изображение очень мощная и имеет множество приложений. С помощью CycleGAN можно генерировать изображение предмета из другого домена в том же контексте, в котором был запечатлен предмет из оригинального домена. Таким образом, можно превращать лошадей в зебр, яблоки в апельсины, менять стиль картин, менять, к примеру, время года на картине, улучшать различные аспекты фотографий, делать адаптивное ретуширование. В общем, список сфер, где можно применять CycleGAN, очень широкий, и инструмент этот чрезвычайно мощный. Более того, он достаточно удобный, благодаря тому, что не нужно иметь парно размеченные данные.  
CycleGAN与标准的GAN不同之处在于，它不是从随机噪声中生成图像。CycleGAN使用给定的图像来生成该图像的另一版本。这个图像到图像的翻译功能使CycleGAN能够将马变成斑马。然而，图像到图像的翻译并不是CycleGAN独有的功能，只是CycleGAN是最早使用非配对数据集进行这种训练的模型之一。这意味着，如前所述，不需要具有特定马和该马作为斑马的配对图像来训练CycleGAN。训练集可以分别包含多张马和多张斑马的图片。这在无法获得配对数据的情况下非常有用。例如，如果我们希望生成斑马版本的马，绘制每匹马的斑马版本没有意义。非配对图像到图像转换功能非常强大，并有许多应用。通过CycleGAN，可以生成目标域的对象图像，保持原始域的上下文。例如，可以将马变成斑马，将苹果变成橙子，改变画作的风格，改变画作的季节，改进照片的各个方面，进行自适应修饰。总之，CycleGAN的应用领域非常广泛，而且这个工具非常强大。更重要的是，由于不需要配对标记数据，它非常方便。