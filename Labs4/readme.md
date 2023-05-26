# Лабораторная работа. Настройка IPv6-адресов на сетевых устройствах 
## Топология
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Topology.PNG)
## Таблица адресации

| Устройство  | Интерфейс  | IPv6-адрес  | Длина префикса  | Шлюз по умолчанию  |
|---|---|---|---|---|
| R1 | G0/0/0  | 2001:db8:acad:a::1  | 64  | none  |
|   | G0/0/1  | 2001:db8:acad:1::1   | 64  | none  |
| S1  | VLAN 1  | 2001:db8:acad:1::b  | 64  | none  |
| PC-A  | NIC  | 2001:db8:acad:1::3  | 64  | fe80::1  |
| PC-B  | NIC  | 2001:db8:acad:a::3  | 64  |  fe80::1 |

 #### Задачи:
 - Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора
 - Часть 2. Ручная настройка IPv6-адресов
 - Часть 3. Проверка сквозного соединения

 ### Использумые ресурсы в платформе:
  - Коммутатор Cisco Catalyst 2960
  - Роутер 4321
  - 2 ПК
  
  ---
 ### Часть первая. Настройка топологии и конфиг основных параметров маршрутизатора и коммутатора. 
 
 ### Шаг 1. Настройка маршрутизатора и роутра.
 - Даём имена нашим устройствам используя знания полученные во время первой лабораторной работы.


 ### Часть 2. Ручная настройка IPv6-адресов
 ### Шаг 1. Назначаем IPv6-адреса интерфейсам.
 -	Назначяем глобальные индивидуальные IPv6-адреса, указанные в таблице адресации обоим интерфейсам Ethernet на R1
 
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4RouIntIPV6add.PNG)
 - Вводим команду Show IPv6 Int brief
 
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4RouIntIPV6IntBrief.PNG)
 - Вручную пишем локальные адреса канала на интерфейсах роутера
 
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4RouIntIPV6LinkLocal.PNG)
 - проверяем, что всё корректно.
 
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4RouIntIPV6ShowLocalG0.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4RouIntIPV6ShowLocalG1.PNG)

Ответ на вопрос: Группа групповой рассылки на все узлы (FF02:: 1) и группа групповой рассылки на запрошенные узлы (FF02::1:FF00:1)

### Шаг 2. Активируем IPv6 маршрутизацию.
 - На PC1 вводим Ipconfig. Убеждаемся, что адреса Ipv6 не назначен
 
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4IpconfFirst.PNG)
 - Активируем IPv6 маршрутизацию командой IPv6 unicast-routing
 
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4RouIntIPV6UniCast.PNG)
 - На PC1 снова вводим ipconfig. 
 
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4IpconfSecond.PNG)

Ответ на вопрос: G0 / 0 теперь является частью группы многоадресной рассылки для всех маршрутизаторов, FF02:: 2. Это позволяет ему отправлять Router Advertisement запросы с глобальным сетевым адресом и информацией об идентификаторе подсети всем узлам локальной сети.

### Шаг 3. Назначаем коммутатору IPv6 адрес для интерфейса Vlan1

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/LabsSW1IPV6Vlan1.PNG)
### Шаг 4. Назначаем компьютерам статические IPv6 адреса. 

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4IpconfStaticPC0.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4IpconfStaticPC2.PNG)

### Часть 3. Прокидываем эхо запросы, как прописано в задании. 
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4PingR1FromPC0.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4PingSW1fromPC0.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4PingPC0fromPC1.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs4PingG0fromPC1.PNG)
 
 
## Ответы на "вопросы для повторения". 
1. Пакеты Link-local никогда не покидают локальную сеть, поэтому один и тот же link-local адрес может использоваться в интерфейсе, связанном с другой локальной сетью
2. 0 (ноль) или 0000 (нули). 4-й шестнадцатеричный код - это идентификатор подсети IPv6-адреса с префиксом / 64. В примере 4-й-й шестнадцатеричный набор содержит все нули, а правило IPv6, исключающее все сегменты 0, использует двойное двоеточие для обозначения идентификатора подсети и первых двух шестнадцатеричных наборов идентификатора интерфейса.
 
