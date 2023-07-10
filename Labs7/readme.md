# Лабораторная работа. Развертывание коммутируемой сети с резервными каналами

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7Topology.PNG)

### Таблица адресации.

| Устройство  |  Интерфейс | IP-адрес  |  Маска подсети |
|---|---|---|---|
| S1  | VLAN 1  | 192.168.1.1  | 255.255.255.0  |
| S2  | VLAN 1  | 192.168.1.2  | 255.255.255.0  |
| S3  | VLAN 1  | 192.168.1.3  | 255.255.255.0  |

 #### Цели:
 - Часть 1. Создание сети и настройка основных параметров устройства
 - Часть 2. Выбор корневого моста
 - Часть 3. Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов
 - Часть 4. Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов

 ### Используемые Платформа:
  - Cisco Packet Tracer
 ### Использумые ресурсы в платформе:
  - 3 Коммутатора Cisco Catalyst 2960
----
### Часть 1. Создание сети и настройка основных параметров устройств.
- Используя знания полученные в предыдущих работах, создаем и настраиваем коммутаторы, используя адреса из таблица адресации.
- Проверяем, что эхо запрос с коммутаторов работает.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7PingOK.PNG)

Ответ на все 3 вопрос: да, они друг друга видят и пингуют.

### Часть 2. Определение корневого моста. 

#### Шаг 1. Выключаем все порты
- Используем команду Int range для облегчения процесса :)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S1IntShut.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S2IntShut.PNG)


![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S3IntShut.PNG)


#### Шаг 2. Настраиваем подключенные интерфейсы как транковые. 

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S1PortTrunk.PNG)


![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S2PortTrunk.PNG)


![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S3PortTrunk.PNG)


#### Шаг 3. Включаем порты F0/2 и F0/4

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S1Int24On.PNG)


![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S1Int24On.PNG)


![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S3Int24On.PNG)


#### Шаг 4. Отобразим данные spanning tree.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S1SpanningTree.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S1SpanningTree.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S3SpanningTree.PNG)


#### Ответы на вопросы.
- Корневым выбран S3
- Выбран по принципу наименьшего значения идентификатора моста (так как данные одиннаковые, кроме MAC, то коммутатор с наименьшим MAC становится корневым)
- S1 F0/4 и S2 F0/4
- S2 F0/2 и S3 F0/4 F0/2
- Заблокирован S1 F0/2
- исходя из стоимости пути. Если стоимость пути равна, затем сравниваются ставки. Предпочтительны меньшие числа. Cвязь между S1 и S2 имеет самую высокую стоимость для корневого моста. Стоимость пути через оба коммутатора одинакова, поэтому STA (spanning tree algorithm) выбрала путь через коммутатор с более низкой ценой и заблокировала порт (F0/2) на коммутаторе с более высокой ценой (S1)

### Часть 3. Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов
#### Шаг 1. Исходя из данных, мы определили коммутатор с заблокированным портом (им является F0/2 на коммутатор S1)
#### Шаг 2. Уменьшим стоимость корневого порта на S1. 

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S1IntF4CostChange.PNG)


#### Шаг 3. Посмотрим на результаты изменений

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S1AfterChange.PNG)


![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S3AfterChange.PNG)

Причина изменений заблокированного порта: STP сначала рассматривает стоимость пути. Порт с меньшей стоимостью пути всегда будет предпочтительнее порта с более высокой стоимостью пути.

#### Шаг 4. Удалим стоимость порта

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S1ChangeAgain.PNG)


- Проверяем, что всё вернулось к исходным значения

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S1S3AfterChange.PNG)


### Часть 3. Часть 4:	Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов.

- Включим порты F0/1 F0/3 на всех коммутаторах.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7F13Up.PNG)


- Посмотрим на изменения.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs7S1S2S3IntOn.PNG)


#### Ответы на вопросы. 

- На S1 корневым портом выбран: F0/3, а на S2 корневым портом выбран: F0/3
- Причина выбора: В качестве корневого порта был выбран порт с меньшим номером и заблокирован порт с большим номером с резервным путем к корневому мосту.

### Вопросы для повторения:

- Стоимость пути. Выбирается путь с меньшей накопленной стоимостью.

- BID, выбрав меньшее значение.

- При суммировании приоритета порта и номера порта предпочтительным является меньшее значение.
