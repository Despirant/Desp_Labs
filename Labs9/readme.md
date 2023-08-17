# Лабраторная работа - Конфигурация безопасности коммутатора

## Топология

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9Topology.PNG)

## Таблица адресации.

|  Устройство | interface/vlan  | IP-адрес  |  Маска подсети |
|---|---|---|---|
| R1  | G0/0/1  | 192.168.10.1  | 255.255.255.0  |
|   | Loopback 0  | 10.10.1.1  |  255.255.255.0 |
| S1  | VLAN 10  | 192.168.10.201  | 255.255.255.0  |
| S2  | VLAN 10  | 192.168.10.202  | 255.255.255.0  |
| PC-1  |  NIC | DHCP  | 255.255.255.0  |
| PC-2  |  NIC |  DHCP | 255.255.255.0  |

### Цели
#### Часть 1. Настройка основного сетевого устройства
-	Создайте сеть.
-	Настройте маршрутизатор R1.
-	Настройка и проверка основных параметров коммутатора
#### Часть 2.Частройка сетей VLAN
- Конфигурируем vlan 10
- Конфигурируем SVI для vlan 10
- Настраиваем vlan 333 с именем Native на S1 и S2
- Настраиваем vlan 999 с именем Parking_loot на S1 и S2
#### Часть 3. Настройка безопасности коммутатора.
-	Реализация магистральных соединений 802.1Q
-	Настройка портов доступа
-	Безопасность неиспользуемых портов коммутатора
-	Документирование и реализация функций безопасности порта
-	Реализовать безопасность DHCP snooping
-	Реализация PortFast и BPDU Guard
-	Проверка сквозной связанности


### Часть 1. Настройка основного сетевого устройства
#### Шаг 1. Создаём сеть.
- Создаём и инициализируем устройства.
#### Шаг 2. Настраиваем маршрутизатор.
- Прописываем конфигурацию исходя из информации в методичке.
- Проверяем конфигурацию и убеждаемся, что все порты включены.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9R1.2.PNG)

#### Шаг 3. Настройка и проверка основных параметров коммутатора.
- а. Настройте имя хоста для коммутаторов S1 и S2

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S2.1.PNG)

- b.	Запретите нежелательный поиск в DNS.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S2.2.PNG)

- c.	Настройте описания интерфейса для портов, которые используются в S1 и S2.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S2.3.PNG)

- d.	Установите для шлюза по умолчанию для VLAN управления значение 192.168.10.1 на обоих коммутаторах. 

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S2.4.PNG)

### Часть 2. Настройка сетей VLAN на коммутаторах.

#### Шаг 1. Конфигурируем VLAN 10.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S2.5.PNG)

#### Шаг 2. Конфиг SVI для VLAN 10.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S2.6.PNG)

#### Шаг 3. Настройте VLAN 333 с именем Native на S1 и S2.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S2.7.PNG)

####Шаг 4. Настройте VLAN 999 с именем ParkingLot на S1 и S2.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S2.8.PNG)

### Часть 3. Настройки безопасности коммутатора.

#### Шаг 1. Релизация магистральных соединений 802.1Q.

 - a.	Настройте все магистральные порты Fa0/1 на обоих коммутаторах для использования VLAN 333 в качестве native VLAN.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S3.1.PNG)

 - b.	Убедитесь, что режим транкинга успешно настроен на всех коммутаторах

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S3.2.PNG)

- c.	Отключить согласование DTP F0/1 на S1 и S2

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S3.3.PNG)

- d.	Проверьте с помощью команды show interfaces

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S3.4.PNG)

#### Шаг 2. Настройка портов доступа

 - a.	На S1 настройте F0/5 и F0/6 в качестве портов доступа и свяжите их с VLAN 10.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S3.5.PNG)

 - b.	На S2 настройте порт доступа Fa0/18 и свяжите его с VLAN 10.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S3.6.PNG)

#### Шаг 3. Безопасность неиспользуемых портов коммутатора

 - a.	На S1 и S2 переместите неиспользуемые порты из VLAN 1 в VLAN 999 и отключите неиспользуемые порты

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S3.7.PNG)

- b.	Убедитесь, что неиспользуемые порты отключены и связаны с VLAN 999, введя команду  show

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S3.8.PNG)

### Шаг 4. Документирование и реализация функций безопасности порта.


| Конфигурация безопасности порта по умолчанию |  |
|---|---|
| Функция  | Настройка по умолчанию  |
| Защита портов  | Disables  |
| Максимальное количество записей MAC-адресов  | 1  |
| Режим проверки на нарушение безопасности  | Shutdown  |
| Aging Time  | 0 mins  |
| Aging Type  | Absolute  |
| Secure Static Address Aging  | Disables  |
| Sticky MAC Address  | 0  |

- b.	На S1 включите защиту порта на F0 / 6 со следующими настройками:
o	Максимальное количество записей MAC-адресов: 3
o	Режим безопасности: restrict
o	Aging time: 60 мин.
o	Aging type: неактивный

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S4.1.PNG)

- с. Verify port security on S1 F0/6.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S4.2.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S4.3.PNG)


- d. Включите безопасность порта для F0 / 18 на S2. Настройте каждый активный порт доступа таким образом, чтобы он автоматически добавлял адреса МАС, изученные на этом порту, в текущую конфигурацию.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S4.4.PNG)

- e. Настройте следующие параметры безопасности порта на S2 F / 18:
o	Максимальное количество записей MAC-адресов: 2
o	Тип безопасности: Protect
o	Aging time: 60 мин.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S4.5.PNG)

- f. Проверка функции безопасности портов на S2 F0/18.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S4.6.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S4.7.PNG)

### Шаг 5. Реализовать безопасность DHCP snooping.

- a.	На S2 включите DHCP snooping и настройте DHCP snooping во VLAN 10

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S4.8.PNG)

- b.	Настройте магистральные порты на S2 как доверенные порты.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S4.9.PNG)

- c.	Ограничьте ненадежный порт Fa0/18 на S2 пятью DHCP-пакетами в секунду

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S5.3.PNG)

- d.	Проверка DHCP Snooping на S2

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S5.4.PNG)

- e.	В командной строке на PC-B освободите, а затем обновите IP-адрес

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S5.5.PNG)

- f.	Проверьте привязку отслеживания DHCP с помощью команды show ip dhcp snooping binding.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S5.6.PNG)

### Шаг 6. Реализация PortFast и BPDU Guard

- a.	Настройте PortFast на всех портах доступа, которые используются на обоих коммутаторах.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S6.1.PNG)

- b.	Включите защиту BPDU на портах доступа VLAN 10 S1 и S2, подключенных к PC-A и PC-B.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S6.2.PNG)

- c.	Убедитесь, что защита BPDU и PortFast включены на соответствующих портах.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs9S6.3.PNG)

### Шаг 7. Проверьте наличие сквозного ⁪подключения.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8Topology.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8Topology.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8Topology.PNG)

### Вопросы для повторения
1.	С точки зрения безопасности порта на S2, почему нет значения таймера для оставшегося возраста в минутах, когда было сконфигурировано динамическое обучение - sticky?
У коммутатора нет поддержки данной функции/

3.	Что касается безопасности порта на S2, если вы загружаете скрипт текущей конфигурации на S2, почему порту 18 на PC-B никогда не получит IP-адрес через DHCP?
Безопасность порта установлена только для двух MAC-адресов, а порт 18 имеет два «липких» MAC-адреса, привязанных к порту.
	
1.	Что касается безопасности порта, в чем разница между типом абсолютного устаревания и типом устаревание по неактивности?
Абсолютное устаревание – После выделенного времени устаревает. 
Устаревание по неактивности – Если отсутствует трафик с адресов, в течении указанного времени
	
