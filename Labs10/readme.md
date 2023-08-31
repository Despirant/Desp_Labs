# Лабораторная работа. Настройка протокола OSPFv2 для одной области

## Топология


![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10Topology.PNG)


## Таблица адресации.

| Уст-во  | Интерфейс  | Ip  | Маска  |
|---|---|---|---|
| R1  | g0/0/1  | 10.53.0.1  | 255.255.255.0  |
|   | Loopback1  | 172.16.1.1  | 255.255.255.0  |
| R2  | g0/0/1  | 10.53.0.2  | 255.255.255.0  |
|   | Loopback1  | 192.168.1.1  | 255.255.255.0|

## Цели:
 - Часть 1. Создание сети и настройка основных параметров устройства
 - Часть 2. Настройка и проверка базовой работы протокола  OSPFv2 для одной области
 - Часть 3. Оптимизация и проверка конфигурации OSPFv2 для одной области

## Часть 1. Создание сети и настройка основных параметров. 

- Как и прежде, мы пользуемся знаниями из предыдущих лабораторных :)

## Часть 2. Настройка и проверка базовой работы протокола OSPFv2 для одной области

### Шаг 1. Настройте адреса интерфейса и базового OSPFv2 на каждом маршрутизаторе.

 - a.	Настройте адреса интерфейсов на каждом маршрутизаторе, как показано в таблице адресации выше.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10R1_1.PNG)


![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10R2_1.PNG)


 - b.	Перейдите в режим конфигурации маршрутизатора OSPF, используя идентификатор процесса 56.
 - c.	Настройте статический идентификатор маршрутизатора для каждого маршрутизатора (1.1.1.1 для R1, 2.2.2.2 для R2).

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10R1_R2_1.PNG)

 - d.	Настройте инструкцию сети для сети между R1 и R2, поместив ее в область 0.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10R1_R2_2.PNG)

 - e.	Только на R2 добавьте конфигурацию, необходимую для объявления сети Loopback 1 в область OSPF 0.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10R2_2.PNG)

 - f.	Убедитесь, что OSPFv2 работает между маршрутизаторами. Выполните команду, чтобы убедиться, что R1 и R2 сформировали смежность.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10R1_R2_3.PNG)


Вопрос:
Какой маршрутизатор является DR? Какой маршрутизатор является BDR? Каковы критерии отбора?
Ответ: 
В этом примере R1 был настроен первым и использовал OSPF перед R2. Во время выбора OSPF только R1 был настроен для OSPF и он стал DR. После настройки R2 для OSPF он стал BDR. При выборе DR и BDR используется маршрутизатор с наибольшим идентификатором маршрутизатора.

g.	На R1 выполните команду show ip route ospf, чтобы убедиться, что сеть R2 Loopback1 присутствует в таблице маршрутизации. Обратите внимание, что поведение OSPF по умолчанию заключается в объявлении интерфейса обратной связи в качестве маршрута узла с использованием 32-битной маски.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10R1_2.PNG)


h.	Запустите Ping до  адреса интерфейса R2 Loopback 1 из R1. Выполнение команды ping должно быть успешным.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10R1_3.PNG)

## Часть 3. Оптимизация и проверка конфигурации OSPFv2 для одной области
### Шаг 1. Реализация различных оптимизаций на каждом маршрутизаторе.

- a.	На R1 настройте приоритет OSPF интерфейса G0/0/1 на 50, чтобы убедиться, что R1 является назначенным маршрутизатором.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10Part3R1.PNG)

- b.	Настройте таймеры OSPF на G0/0/1 каждого маршрутизатора для таймера приветствия, составляющего 30 секунд.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10Part3R1R2.PNG)

- c.	На R1 настройте статический маршрут по умолчанию, который использует интерфейс Loopback 1 в качестве интерфейса выхода. Затем распространите маршрут по умолчанию в OSPF. Обратите внимание на сообщение консоли после установки маршрута по умолчанию.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10Part3R1_2.PNG)

- d.	добавьте конфигурацию, необходимую для OSPF для обработки R2 Loopback 1 как сети точка-точка. Это приводит к тому, что OSPF объявляет Loopback 1 использует маску подсети интерфейса.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10Part3R2.PNG)

- e.	Только на R2 добавьте конфигурацию, необходимую для предотвращения отправки объявлений OSPF в сеть Loopback 1.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10Part3R2_2.PNG)

- f.	Измените базовую пропускную способность для маршрутизаторов. После этой настройки перезапустите OSPF с помощью команды clear ip ospf process . Обратите внимание на сообщение консоли после установки новой опорной полосы пропускания.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10Part3R1R2_2.PNG)


###Шаг 2. Убедитесь, что оптимизация OSPFv2 реализовалась.
- a.	Выполните команду show ip ospf interface g0/0/1 на R1 и убедитесь, что приоритет интерфейса установлен равным 50, а временные интервалы — Hello 30, Dead 120, а тип сети по умолчанию — Broadcast

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10Part3R1R2_3.PNG)

- b.	На R1 выполните команду show ip route ospf, чтобы убедиться, что сеть R2 Loopback1 присутствует в таблице маршрутизации. Обратите внимание на разницу в метрике между этим выходным и предыдущим выходным. Также обратите внимание, что маска теперь составляет 24 бита, в отличие от 32 битов, ранее объявленных.
- c.	Введите команду show ip route ospf на маршрутизаторе R2. Единственная информация о маршруте OSPF должна быть распространяемый по умолчанию маршрут R1.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10Part3R1R2_4.PNG)

- d.	Запустите Ping до адреса интерфейса R1 Loopback 1 из R2. Выполнение команды ping должно быть успешным.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/Labs10Part3R2_3.PNG)

Вопрос:
Почему стоимость OSPF для маршрута по умолчанию отличается от стоимости OSPF в R1 для сети 192.168.1.0/24?

Ответ:

Потому что, Сеть 192.168.1.0 /24 представляет собой внутренний маршрут OSPF, показатель которого является кумулятивным. 
