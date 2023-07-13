# Лабраторная работа - Настройка DHCPv6

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8Topology.PNG)

### Таблица адресации.

| Устройство  | Интерфейс  | IPv6-адрес  |
|---|---|---|
| R1  | G/0/0/0  | 2001:db8:acad:2::1/64  |
|   |   | fe80::1  |
|   | G0/0/1  | 2001:db8:acad:1::1/64  |
|   |   | fe80::1  |
| R2  | G0/0/0  | 2001:db8:acad:2::2/64  |
|   |   | fe80::2  |
|   | G0/0/1  | 2001:db8:acad:3::1/64  |
|   |   | fe80::1  |
| PC-A  | NIC  |  DHCP |
| PC-B  | NIC  |  DHCP |

 #### Задачи
 - Часть 1. Создание сети и настройка основных параметров устройства
 - Часть 2. Проверка назначения адреса SLAAC от R1
 - Часть 3. Настройка и проверка сервера DHCPv6 без гражданства на R1
 - Часть 4. Настройка и проверка состояния DHCPv6 сервера на R1
 - Часть 5. Настройка и проверка DHCPv6 Relay на R2


 ### Используемые Платформа:
  - Cisco Packet Tracer
 ### Использумые ресурсы в платформе:
  - 2 маршрутизатора (Cisco 4331)
  - 2 коммутатора (Cisco 2960)
  - 2 ПК

_____

### Часть 1. Создание сети и настройка устройств. 
#### Шаг 1. Производим базовую настройку коммутаторов и роутеров используя знания из предыдущих лабораторных работ. 
#### Шаг 2. настройка интерфейсов и маршрутизации на каждом роутере.

- Настраиваем интерфейсы.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8R1IntV6.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8R2IntV6.PNG)

- Прописываем маршруты

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8R1IntV6Route.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8R2IntV6Route.PNG)


- маршрутизация работает с помощью пинга адреса G0/0/1 R2 из R1

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8R1PingOK.PNG)

_____

### Часть 2. Проверка назначения адреса SLAAC от R1

- Проверяем автоматическое получение IPv6 на PC-A и прописываем команду Ipconfig

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8PcaIpconfig.PNG)

Ответ на вопрос: хост генерирует случайный 64-разрядный адрес

___

### Часть 3. Часть 3. Настройка и проверка сервера DHCPv6 на R1.
#### Шаг 1. Более подробно изучаем конфиг PC-A

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8PcaIpconfigAll.PNG)

#### Шаг 2. Настроим R1 для предоставления DHCPv6 без состояния для PC-A

- a.	Создадим пул DHCP IPv6 на R1 с именем R1-STATELESS

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8R1Stateless.PNG)

- b.	Настроим интерфейс G0/0/1 на R1, чтобы предоставить флаг конфигурации OTHER для локальной сети R1.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8R1StatelessG001.PNG)

- c. сохраним конфигурацию, перезагрузим PC-A и посмотри на изменения в ipconfig /all на PC-A.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8PcaIpconfigAllAgain.PNG)

- d. Проверим подключение с помощью пинга G0/0/1 R2

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8PcaIpingR2.PNG)

___

### Часть 4. Часть 4. Настройка сервера DHCPv6 с сохранением состояния на R1

- a.	Создадим пул DHCPv6 на R1 для сети 2001:db8:acad:3:aaa::/80

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8R1StatelessR2.PNG)

- b. Назначим только что созданный пул DHCPv6 интерфейсу g0/0/0 на R1

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs8R1StatelessG000.PNG)

____


### Часть 5. Настройка и проверка Statefull DHCPv6 на R2.

В связи с тем, что в рамках CPT невозможно реализовать relay, реализуем DHCPv6 Statefull на R2, по анологии с R1 и посмотрим, как отработает данная реализация.



![](https://github.com/Despirant/Desp_Labs/blob/main/pics/PCAStatefyll.PNG)

