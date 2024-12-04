<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>

## [MainPage](../index.md)/[Computer NetWork](README.md)/HomeWork

# Лабораторные работы по дисциплине «Компьютерные сети» «Моделирование компьютерных сетей в среде NetEmul»

# Лабораторная работа №2 «Локальные сети» 

## 1. ЦЕЛЬ РАБОТЫ

Изучение принципов настройки и функционирования локальных сетей, построенных с использованием концентраторов и коммутаторов, а также процессов передачи данных на основе стека протоколов TCP/IP, с использованием программы моделирования компьютерных сетей NetEmul.  
使用NetEmul计算机网络建模程序，研究使用集线器和交换机构建的本地网络的设置和操作原理，以及基于TCP/IP协议栈的数据传输过程。

В процессе выполнения лабораторной работы (ЛР) необходимо:  
在进行实验室工作（LP）的过程中，有必要：

- построить модели трёх локальных сетей:  
  构建三个本地网络的模型：
  1) односегментной сети с использованием концентратора,  
     使用集线器的单网段网络 
  2) односегментной сети с использованием коммутатора;  
     使用交换机的单网段网络；  
  4) многосегментной локальной сети;  
     多网段本地网络；
- выполнить настройку сети, заключающуюся в присвоении IP-адресов интерфейсам сети;  
  执行网络配置，包括为网络接口分配 IP 地址；
- выполнить тестирование разработанных сетей путем проведения экспериментов по передаче данных (пакетов и кадров) на основе протоколов UDP и TCP;  
  通过基于UDP和TCP协议进行数据传输（数据包和帧）实验来测试开发的网络；
- проанализировать результаты тестирования и сформулировать выводы об эффективности смоделированных вариантов построения локальных сетей;  
  分析测试结果并就构建本地网络的模拟选项的有效性得出结论；
- сохранить разработанные модели локальных сетей для демонстрации процессов передачи данных при защите лабораторной работы.  
  保存开发的本地网络模型，以在保护实验室工作时演示数据传输过程。

## 2. ЭТАПЫ И ПОРЯДОК ВЫПОЛНЕНИЯ РАБОТЫ

### Этап 1. Локальная сеть с концентратором (Сеть 1) 

1. Построение сети с концентратором.  
   构建具有集线器的网络。
   1. Построить сеть из N1 компьютеров, объединенных в локальную сеть c помощью концентратора (хаба). Для формирования связей между устройствами необходимо выбрать соединяемые интерфейсы (кнопка **Создать соединение** в меню устройств) на каждом из устройств.  
      使用集中器（集线器）构建连接到本地网络的 N1 计算机网络。 要在设备之间建立连接，您必须在每个设备上选择要连接的接口（设备菜单中的 **创建连接** 按钮）。
   3. Присвоить имена (идентификаторы) всем устройствам сети (пункт **Задать описание**… в меню управления соответствующего устройства) для отслеживания протекающих в них процессов (последовательности и содержания передаваемых пакетов и кадров) в Журналах устройств.  
      为所有网络设备分配名称（标识符）（相应设备控制菜单中的**设置描述**...项），以跟踪其中发生的进程（传输数据包和帧的顺序和内容）在设备日志中。
   4. Для наглядности и облегчения анализа протекающих в сети процессов при передаче пакетов и кадров желательно визуализировать MAC- и IP-адреса на модели сети (кнопка **Вставить текстовую запись** в меню устройств).  
      为了清楚起见并便于分析传输数据包和帧时网络中发生的过程，建议在网络模型上可视化 MAC 和 IP 地址（设备菜单中的 **插入文本条目** 按钮）。
   5. Проанализировать содержимое таблиц маршрутизации и arp-таблиц.  
      分析路由表和arp表的内容。
   Описать: 描述：
      - какая информация находится в таблицах;  
        表中有哪些信息；
      - как формируется каждая запись в таблицах?  
        表中的每条记录是如何形成的？

2. Настройка компьютеров.

   1. Подключить для каждого настраиваемого компьютера **Журнал** для анализа передаваемых данных после назначения (присвоения) IP- адреса (пункт **Показать журнал** меню управления компьютера).  
      为每台配置的计算机连接**Log**，分配IP地址后分析传输的数据（计算机管理菜单中的**Show Log**项）。
   2. Настроить интерфейс (сетевой карты) компьютера (пункт **Интерфейс** меню управления компьютера), назначив ему вручную IP-адреса, при этом автоматически появится маска, которая при необходимости может быть изменена.  
      配置计算机的接口（网卡）（计算机管理菜单中的**接口**项），手动为其分配IP地址，会自动出现一个掩码，需要时可以更改。 
   4. Назначить (присвоить) всем ПК IP-адреса из заданного множества адресов в меню **Интерфейс** и определить:  
      从 **Interface** 菜单中给定的一组地址中为所有 PC 分配（分配）IP 地址，并确定：
      - какие и зачем передаются служебные сообщения после назначения IP-адреса;  
        分配IP地址后传输什么以及为什么传输服务消息；
      - каково содержание этих сообщений.  
        这些消息的内容是什么。

3. **Анализ таблиц**  
   **表格分析**
   Проанализировать содержание таблиц маршрутизации и arp-таблиц компьютеров и определить:  
   分析计算机的路由表和arp表内容，确定：
   - появились ли в них изменения;  
     它们是否有任何变化；
   - если «да», то какие и почему.
     如果“是”，那么是哪些以及为什么。

4. **Тестирование сети (отправка пакетов)**.  
   **网络测试（发送数据包）**。
   1. Проанализировать передачу сообщений с использованием протокола UDP. Описать:  
      分析使用UDP协议的消息传输。 描述：   
      - какие пакеты и кадры передаются в сети;  
        网络上传输哪些数据包和帧；
      - в какой последовательности передаются пакеты и кадры:  
        数据包和帧按什么顺序传输：
      - какая информация содержится в пакетах и кадрах.  
        数据包和帧中包含哪些信息。
   2. Проанализировать передачу сообщений с использованием протокола TCP. Описать:  
      分析使用TCP协议的消息传输。 描述：
      - какие пакеты и кадры передаются в сети;  
        网络上传输哪些数据包和帧；
      - в какой последовательности передаются пакеты и кадры:  
        数据包和帧按什么顺序传输：
      - какая информация содержится в пакетах и кадрах;  
        数据包和帧中包含哪些信息；
      - какие основные отличия при передаче сообщений по протоколу UDP и протоколу TCP.  
        通过UDP协议和TCP协议传输消息时的主要区别是什么。
   3. Сохранить построенную локальную сеть.  
      保存构建的本地网络。

### Этап 2. Локальная сеть с коммутатором (Сеть 2) 

5. Построение локальной сети с коммутатором.  
   用交换机构建本地网络。
   1. Построить сеть из N2 компьютеров, объединенных в локальную сеть c помощью коммутатора (свитча) и открыть таблицу коммутации.  
      建立一个N2计算机网络，使用交换机（switch）连接到本地网络，并打开交换表。
   Описать: 描述：  
      - какие поля содержит таблица коммутации;  
        交换表包含哪些字段？
      - в каких единицах измеряется время жизни;  
        寿命用什么单位来衡量？
      - чему равно максимальное значение времени жизни.  
        最大终生价值是多少？
   2. Не заполняя таблицу коммутации провести эксперименты по передаче данных между компьютерами и описать:  
      在不填写交换表的情况下，进行计算机之间数据传输的实验并描述：
      - как происходит заполнение таблицы коммутации;  
        换算表是如何填写的；
      - на основе анализа какой информации заполняется таблица коммутации;  
        基于对交换表填写了哪些信息的分析；
      - в чем основные отличия передачи сообщений в сети с коммутатором от сети с концентратором;  
        带有交换机的网络和带有集线器的网络中消息传输的主要区别是什么；
      - когда (при каком условии) таблица коммутации будет построена полностью;  
        何时（在什么条件下）完全构建交换表；  
      - чему равно максимальное количество записей (строк) в таблице коммутации.  
        交换表中的最大条目（行）数是多少。
6. **Анализ таблиц 表格分析**
   Проанализировать содержимое таблиц маршрутизации и arp- таблиц ПК и определить:  
   分析PC的路由表和arp表内容，确定：
   - появились ли в них изменения и, если «да», то какие и почему.  
     它们是否发生了变化，如果“是”，那么发生了什么变化以及原因。

7. **Тестирование сети (отправка пакетов)**.  
   **网络测试（发送数据包）**。
   1. Проиллюстрировать передачу сообщений с использованием протокола UDP. Описать:  
      说明使用UDP协议的消息传输。 描述：
      - какие и в какой последовательности передаются служебные и пользовательские пакеты и кадры;   
        服务和用户数据包和帧的传输内容和顺序；
      - какие изменения происходят в таблицах маршрутизации, arp- таблицах и в таблице коммутации.  
        路由表、arp 表和交换表中发生了哪些变化。 
   2. Проиллюстрировать передачу сообщений с использованием протоколов UDP. и TCP. Описать:  
      说明使用UDP 协议的消息传输。 和 TCP。 描述：
      - какие и в какой последовательности передаются служебные и пользовательские пакеты и кадры;  
        服务和用户数据包和帧的传输内容和顺序；
      - какие изменения происходят в таблицах маршрутизации, arp-таблицах и в таблице коммутации.  
        路由表、arp 表和交换表中发生了哪些变化。
   3. Сохранить построенную локальную сеть.  
      保存构建的本地网络。 

### Этап 3. Многосегментная локальная сеть (Сеть 3) 

8. Формирование сети.  
   网络形成。
   1. Две ранее построенные локальные сеть 1 и сеть 2 (сегменты) с концентратором и коммутатором объединить в единую многосегментную сеть и подключить к этой сети еще один сегмент (сеть 3) с N3 компьютерами и коммутатором.  
      将两个先前构建的本地网络 1 和网络 2（网段）与集线器和交换机组合成一个多网段网络，并使用 N3 计算机和交换机将另一个网段（网络 3）连接到该网络。
   2. Проанализировать и описать: 分析描述：
      - содержимое таблиц маршрутизации и arp-таблиц в каждом ПК и таблицу коммутации коммутатора.  
        每台PC中的路由表和arp表以及交换机的交换表的内容。
   3. Рассмотреть и сравнить разные варианты связей коммутаторов и концентратора (последовательно друг с другом, «кольцо», …), и предложить наилучший вариант. На основе анализа таблиц коммутации определить:  
      考虑并比较连接交换机和集线器的不同选项（相互串联、“环”……），并提出最佳选项。 根据切换表分析，确定：
      - какие варианты связей между коммутаторами оказались нереализуемы и почему;  
        交换机之间的哪些连接选项被证明是无法实现的以及原因；
      - будет ли работоспособна сеть, если для нереализуемых вариантов концентраторы заменить на коммутаторы или наоборот.  
        如果对于无法实现的选项，用交换机替换集线器，则网络是否可以运行，反之亦然。

9. Тестирование сети (отправка пакетов).  
    网络测试（发送数据包）。
    1. Для выбранного варианта связей между проиллюстрировать передачу сообщений с использованием протокола UDP. Описать:  
       对于选定的连接选项，说明使用 UDP 协议传输消息。 描述：
       - какие и в какой последовательности передаются служебные и пользовательские пакеты и кадры;  
         服务和用户数据包和帧的传输内容和顺序；
       - какие изменения происходят в таблицах коммутации и arp- таблицах.  
         交换表和arp表发生了什么变化。
    2. Проиллюстрировать передачу сообщений с использованием протоколов UDP и TCP. Описать:  
       说明使用UDP 和TCP 协议进行消息传输。 描述：
       - какие и в какой последовательности передаются служебные и пользовательские пакеты и кадры;  
         服务和用户数据包和帧的传输内容和顺序；
       - какие изменения происходят в таблицах коммутации и arp- таблицах.  
         交换表和arp表发生了什么变化。
   3. Сохранить построенную многосегментную локальную сеть.  
      保存构建的多网段本地网络。

### 3. ТРЕБОВАНИЯ К СОДЕРЖАНИЮ ОТЧЁТА

Отчет по выполненной лабораторной работе состоит из двух частей:  
实验室工作报告由两部分组成：
1) краткое описание построенных сетей с результатами анализа и скриншотами, подтверждающими результаты и выводы по работе;  
   对所构建网络的简要描述，以及分析结果和确认工作结果和结论的屏幕截图；
2) сохранённые все построенные модели компьютерных сетей для иллюстрации их работы в среде NetEmul с целью подтверждения полученных результатов.  
   保存所有构建的计算机网络模型，以说明其在NetEmul环境中的工作，以确认所获得的结果。

Отчёт в электронном виде должен содержать следующие пункты.  
电子报告必须包含以下内容。

1. Постановку задачи с исходной информацией о количестве компьютеров, сетевых устройств и пуле IP-адресов в соответствии с вариантом лабораторной работы.  
   根据实验室工作选项，对问题进行陈述，并提供有关计算机数量、网络设备和 IP 地址池的初始信息。
2. Скриншоты: 截图：
   - рассмотренных в работе вариантов реализации локальных сетей с отображением назначенных интерфейсам устройств IP-адресов;  
     在显示分配给设备接口的 IP 地址的工作中考虑的实现本地网络的选项；  
   - таблиц коммутации, маршрутизации и arp-таблиц (выборочно, в основном таких таблиц, которые наиболее полно позволяют получить представление о принципах их заполнения и иллюстрируют процесс передачи данных в сети);  
     交换表、路由表和arp表（选择性地，主要是那些最能让你了解其填充原理并说明网络中数据传输过程的表）；
   - журналов устройств сети, иллюстрирующих процессы передачи данных в сети и содержание передаваемых пакетов и кадров.  
     网络设备的日志，说明网络上的数据传输过程以及传输的数据包和帧的内容。
3. Результаты анализа, полученные в процессе тестирования и моделирования, представляющие собой ответы на сформулированные выше вопросы, должны дать полное представление об основных принципах передачи данных в локальных сетях на основе протоколов UDP и TCP.  
   测试和建模过程中获得的分析结果是对上述问题的回答，应使您完全理解基于UDP和TCP协议的本地网络中数据传输的基本原理。

### 4. ВАРИАНТЫ ЛАБОРАТОРНОЙ РАБОТЫ

Вариант лабораторной работы выбирается ниже из Таблицы по номеру студента в списке группы в ИСУ университета.  
实验室工作选项根据大学 ИСУ 中小组列表中的学生人数从下表中选择。

4 байта IP-адресов для использования в лабораторной работе формируется в зависимости от заданного класса адресов следующим образом:  
实验室使用的 4 字节 IP 地址是根据给定的地址类别生成的，如下所示：

- для класса А:  (Ф+Н).(И+Н).(О+Н).(Ф+И) 
- для класса В:  (И+Н+128).(О+Н).(Ф+Н).(Ф+И) 
- для класса С:  (192+Н +О).(Ф+Н).(И+Н).(Ф+И) 
  
Здесь: 
- Ф, И, О – количество букв в Фамилии, Имени, Отчестве студента; 
- Н – две последние цифры в номере группы.


Пример. Студент группы Р3313 Иванов Петр Степанович будет иметь: 

Ф=6, И=4, О=10, Н=13.

В этом случае адреса сетей разных классов будут иметь вид: 
- класс А: 19.17.23.10 
- класс В: 145.23.19.10 
- класс С: 215.19.17.10 

В работе должен быть сформирован и использоваться в дальнейшем пул последовательных IP-адресов, представляющий собой множество адресов, начинающееся с полученного выше значения, размер которого достаточен для адресации всех интерфейсов сети.  
在工作中，将来必须形成并使用一个连续的IP地址池，它是以上面获得的值开始的一组地址，其大小足以寻址所有网络接口。

В нашем примере в сети класса В для нумерации 10-и интерфейсов будет использоваться пул последовательных адресов:   
在我们的示例中，在 B 类网络中，将使用顺序地址池对 10 个接口进行编号：

145.23.19.10 – 145.23.19.19 (10 адресов).