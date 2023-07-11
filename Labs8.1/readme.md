# Лабраторная работа - Реализация DHCPv4

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8Topology.PNG)


### Таблица адресации.

| Устройство  | Интерфейс  | IP-адрес  | IP-адрес  | Шлюз по умолчанию  |
|---|---|---|---|---|
| R1  | G0/0/0  | 10.0.0.1  | 255.255.255.252  | N/A  |
|   | G0/0/1  | N/A  | N/A  | N/A  |
|   | G0/0/1.100  | 192.168.1.1  | 255.255.255.192  | N/A  |
|   | G0/0/1.200  | 192.168.1.65  | 255.255.255.224  |  N/A |
|   | G0/0/1.1000  | N/A | N/A  | N/A  |
| R2  | G0/0/0  | 10.0.0.2  | 255.255.255.252  | N/A  |
|   | G0/0/1  | 192.168.1.97  | 255.255.255.240  | N/A  |
| S1  | VLAN 200  | 192.168.1.66  | 255.255.255.224  | 192.168.1.65  |
| S2  | VLAN 1  | 192.168.1.98  | 255.255.255.240  | 192.168.1.97  |
| PC-A  | NIC  | DHCP  | DHCP  | DHCP  |
| PC-B  | NIC  | DHCP  | DHCP  | DHCP  |

### Таблица VLAN

|  VLAN | Имя  | Назначенный интерфейс  |
|---|---|---|
| 1  | НЕТ  | S2: F0/18  |
| 100  | Клиенты  | S1: F0/6   |
| 200  | Управление  | S1: F0/6   |
| 999  | Parking_lot  | S1: F0/1-4, F0/7-24, G0/1-2  |
| 1000  | собственная  | NA  |

 #### 3.	Задачи
 - Часть 1. Создание сети и настройка основных параметров устройства
 - Часть 2. Настройка и проверка двух серверов DHCPv4 на R1
 - Часть 3. Настройка и проверка DHCP-ретрансляции на R2



 ### Используемые Платформа:
  - Cisco Packet Tracer
 ### Использумые ресурсы в платформе:
  - 2 маршрутизатора (Cisco 4331)
  - 2 коммутатора (Cisco 2960)
  - 2 ПК

_____

### Часть 1.	Создание сети и настройка основных параметров устройства

#### Шаг 1. Настроим роутеры используя знания полученные в предыдущих лабораторных работах.

#### Шаг 2. Настроим маршрутизацию между сетями VLAN на R1

- активируем и настроим интерфейс и подинтерфейсы

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R1IntSubint.PNG)

- убеждаемся, что интерфейсы работают

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R1showintbrief.PNG)

#### Шаг 4. Настройка G0/1 на R2, затем G0/0/0 и статическую маршрутизацию для обоих маршрутизаторов

- Настроим g0/0/1 на R2

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R2G1.PNG)

- настроим интерфейс g0/0/0 для каждого маршрутизатора

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R2G0.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R1G0.PNG)

- Настроим маршрут на каждом маршрутизаторе

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R1route.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R2route.PNG)

- проверяем, что всё работает и сохраняем конфиг

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R1PingR2.PNG)


#### Шаг 5. Настраиваем базовые параметры на каждом коммуникаторе

#### Шаг 6. Создаём VLAN на S1

- Создадим необходимые VLAN на коммутаторе 1 и присвоим им имена

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1S1VLAN.PNG)

- Настроим и активируем интерфейс управления на S1 (VLAN 200), используя второй IP-адрес из подсети, рассчитанный ранее. Кроме того установим шлюз по умолчанию на S1.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1S1vlan200nastroika.PNG)

- Настроим и активируем интерфейс управления на S2 (VLAN 1), используя второй IP-адрес из подсети, рассчитанный ранее. Кроме того, установим шлюз по умолчанию на S2

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1S2Vlan1.PNG)
 
- Назначим все неиспользуемые порты S1 VLAN Parking_Lot, настроим их для статического режима доступа и административно деактивируем их. На S2 административно деактивируем все неиспользуемые порты.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1S1IntShut.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1S2IntShut.PNG)

#### Шаг 7. Назначьте сети VLAN соответствующим интерфейсам коммутатора.
 - Назначьте используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настройте их для режима статического доступа.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1S1IntF06.PNG)

 - Убеждаемся, что VLAN назначены на правильные интерфейсы.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1S1ShowBrief.PNG)

Вопрос:
Почему интерфейс F0/5 указан в VLAN 1?
Ответ:
Порт 5 находится в VLAN по умолчанию и не был настроен транковый.

#### Шаг 8. Вручную настроим S1 F0/5 в качестве транка.

 - Измените режим порта коммутатора, чтобы принудительно создать магистральный канал.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1S1F05.PNG)

 - В рамках конфигурации транка  установите для native  VLAN значение 1000.
 - В качестве другой части конфигурации магистрали укажите, что VLAN 100, 200 и 1000 могут проходить по транку.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1S1F05Vlans.PNG)

 - Сохраните текущую конфигурацию в файл загрузочной конфигурации.
 - Проверьте состояние транка.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1S1F05showtrunk.PNG)


Вопрос:
Какой IP-адрес был бы у ПК, если бы он был подключен к сети с помощью DHCP?
Ответ: самонастроилася бы с использованием автоматического частного IP-адреса (APIPA) в диапазоне 169.254.x.x 


### Часть 2. Настройка и проверка двух серверов DHCPv4 на R1.

### Шаг 1. Настроим R1 с пулами DHCPv4 для двух поддерживаемых подсетей. 

 - Исключите первые пять используемых адресов из каждого пула адресов.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R1Exclude.PNG)

 - Создайте пул DHCP (используйте уникальное имя для каждого пула).
 
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R1PoolCreate.PNG)
 
 - Укажите сеть, поддерживающую этот DHCP-сервер.
 
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R1PoolNetwork.PNG) 
 
 - В качестве имени домена укажите CCNA-lab.com.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R1domainname.PNG)

 - Настройте соответствующий шлюз по умолчанию для каждого пула DHCP.
 
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R1defrouter.PNG) 
 
 - Настройте время аренды на 2 дня 12 часов и 30 минут.
 
 К сожалению, в рамках Cisco Packet Tracer нет возможности прописать данную команду.
 
 - Затем настройте второй пул DHCPv4, используя имя пула R2_Client_LAN и вычислите сеть, маршрутизатор по умолчанию, и используйте то же имя домена и время аренды, что и предыдущий пул DHCP.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R1R2Pool.PNG)


### Шаг 2.	Сохраним конфигурацию.
### Шаг 3.	Проверка конфигурации сервера DHCPv4
 - Чтобы просмотреть сведения о пуле, выполните команду show ip dhcp pool

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1ShowdhcpPool.PNG)

 - Выполните команду show ip dhcp bindings для проверки установленных назначений адресов DHCP.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1ShowdhcpBinding.PNG)

 - Выполните команду show ip dhcp server statistics для проверки сообщений DHCP.

В рамках Packet Tracer не даёт посмотреть данную информацию

### Шаг 4.	Попытка получить IP-адрес от DHCP на PC-A
 - Из командной строки компьютера PC-A выполните команду ipconfig /all.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1PCaConfigAll.PNG)

 - После завершения процесса обновления выполните команду ipconfig для просмотра новой информации об IP-адресе.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1PCaConfig.PNG)

 - Проверьте подключение с помощью пинга IP-адреса интерфейса R0 G0/0/1.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1PCaPing.PNG)

### Часть 3.	Настройка и проверка DHCP-ретрансляции на R2

#### Шаг 1.	Настройка R2 в качестве агента DHCP-ретрансляции для локальной сети на G0/0/1
 - Настройте команду ip helper-address на G0/0/1, указав IP-адрес G0/0/0 R1 и сохраним конфинг

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1R2Helper.PNG)



#### Шаг 2.	Попытка получить IP-адрес от DHCP на PC-B
 - Из командной строки компьютера PC-B выполните команду ipconfig /all.
 - После завершения процесса обновления выполните команду ipconfig для просмотра новой информации об IP-адресе.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1PCBConfig.PNG)

 - Проверьте подключение с помощью пинга IP-адреса интерфейса R1 G0/0/1.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8.1PCpingR1.PNG)

 - Выполните show ip dhcp binding для R1 для проверки назначений адресов в DHCP.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8Topology.PNG)

 - Выполните команду show ip dhcp server statistics для проверки сообщений DHCP.

Невозможно в рамках Cisco Packet Tracer


