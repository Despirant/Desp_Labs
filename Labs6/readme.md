# Внедрение маршрутизации между виртуальными локальными сетями
## Топология
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6Topology.PNG)
### Таблица адресации.

| Устройство  | Интерфейс  | IP-адрес  | Маска подсети  | Шлюз по умолчанию  |
|---|---|---|---|---|
| R1  | G0/0/1.10  | 192.168.10.1  |  255.255.255.0 | NONE  |
| R1  | G0/0/1.20  | 192.168.20.1  |  255.255.255.0 | NONE  |
| R1  | G0/0/1.30  | 192.168.30.1  |  255.255.255.0 | NONE  |
| R1  | G0/0/1.1000  | NONE  | NONE  | NONE  |
| S1  | VLAN 10  | 192.168.10.11  | 255.255.255.0  | 192.168.10.1  |
| S2  | VLAN 10  | 192.168.10.12  | 255.255.255.0  | 192.168.10.1  |
| PC-A  | NIC  | 192.168.20.3  | 255.255.255.0  | 192.168.20.1  |
| PC-B  | NIC  | 192.168.30.3  | 255.255.255.0  | 192.168.30.1  |

### Таблица VLAN

| vlan  | имя  | Назначенный интерфейс  |
|---|---|---|
| 10  | Управление  | S1: Vlan 10 ; S2: Vlan 10  |
| 20  | Sales  | S1: F0/6  |
| 30  | Operation  | S2: F0/18  |
| 999  |  Parking_Lot | C1: F0/2-4, F0/7-24, G0/1-2 ; C2: F0/2-17, F0/19-24, G0/1-2  |
| 1000  | Собственная  | None  |

 #### Задачи.
 - Часть 1. Создание сети и настройка основных параметров устройства
 - Часть 2. Создание сетей VLAN и назначение портов коммутатора
 - Часть 3. Настройка транка 802.1Q между коммутаторами.
 - Часть 4. Настройка маршрутизации между сетями VLAN
 - Часть 5. Проверка, что маршрутизация между VLAN работает

 ### Используемые Платформа:
  - Cisco Packet Tracer
 ### Использумые ресурсы в платформе.
  - Маршрутизатор 1шт.
  - Коммутатор 2 шт.
  - ПК 2шт.
  - Кабели Ethernet расположенные в соотвествии с топологией

### Часть 1. Создание сети и настройка параметров. 
- Используя знания из прошлых лаб, настраиваем коммутатор, компы и маршрутизатор.
### Часть 2. Создание сетей Vlan и назначение порторв коммутатора. 
#### Шаг 1. 
- Создаём и даём название необходимым VLAN на каждом коммутаторе

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S1VlanNames.PNG)
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S2VlanNames.PNG)

- Настраиваем интерфейс управления и шлю по умолчанию

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S1VlanGateWay.PNG)
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S2VlanGateWay.PNG)

- Назначаем все неиспользуемые порты коммутатора Vlan Parking_Lot, настраиваем в статическом режиме и выключаем их.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S1Vlan999addshut.PNG)
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S1Vlan999addshut.PNG)


#### Шаг 2. Назначаем сети VLAN соотвествующим интерфейсам.
- назначаем используемые порты соответствующей Vlan и настраиваем их для статического доступа

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S1VlanInterface.PNG)
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S2VlanInterface.PNG)

- убеждаемся, что vlan назначены на правильные интерфейсы.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S1VlanAllOk.PNG)
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S2VlanAllOk.PNG)

### Часть 3. Конфигурация магистрального канала стандарта 802.1Q между свитчами.
#### Шаг 1. Настраиваем магистральный интерфейс F0/1 на коммутаторах 
- Настраиваем статический транкинг на F0/1

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S1TrunkF1.PNG)
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S2TrunkF1.PNG)

- Устанавливаем Native Vlan 1000

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S1Vlan1000.PNG)
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S2Vlan1000.PNG)

- Указываем, что 10, 20, 30 и 1000 vlan могу проходить по транку

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S1TrunkAllowed.PNG)
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S2TrunkAllowed.PNG)

- Проверяем транки, Native Vlan и разрешеные vlan через транк

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S1TrunkCheck.PNG)
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S2TrunkCheck.PNG)

#### Шаг 2. Настраиваем F0/5 на S1
- Настраиваем нужный интерфейс с параметрами транка, как и на F0/1
- Сохраняем конфиг.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6S1F5Trunk.PNG)
 
Ответ на доп. вопрос:  F0/5 не будет отображаться, если интерфейс g0/0/1 на маршрутизаторе отключен.

### Часть 4. Настройка маршрутизации между сетями VLAN. 
#### Шаг 1. Настраиваем интерфейс g0/0/1 на маршрутизаторе.
- Настраиваем подинтерфейсы для каждого Vlan. Убеждаемся, что Native Vlan не назначен IP. И включаем описание для каждого подинтерфейс.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6R1VlanConfig.PNG)
 
- Убеждаемся, что всё работает.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6R1VsoChotko.PNG)

### Часть 5. Проверяем, работает ли маршрутизация между VLAN. 
#### Шаг1. отправляем эхо с PC-1

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/labs6PCApingAll.PNG)

#### Шаг 2. Выполняем tracert на адрес PC-A

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs6PCBtoPCATracert.PNG)

Какие промежуточные адреса в результатах: Выходные данные tracert должны отображать две записи в результатах. Первый переход - это адрес интерфейса R1 G0 / 0 / 1.30, который является адресом шлюза для PC-B. Второй переход - это адрес PC-A.

