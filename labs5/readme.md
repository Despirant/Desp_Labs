# Лабораторная работа. Доступ к сетевым устройствам по протоколу SSH
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5Top.PNG)
## Таблица адресации. 

| Уст-во  | Интерфейс  | IP адрес  | Маска | Шлюз  |
|---|---|---|---|---|
| R1  | g0/0/1  | 192.168.1.1  | 255.255.255.0  | -  |
| S1  | Vlan 1  | 192.168.1.11  | 255.255.255.0  | 192.168.1.1  |
| PC-0  | NIC  | 192.168.1.3  | 255.255.255.0  | 192.168.1.1  |

 ### Задачи:
Часть 1. Настройка основных параметров устройства
Часть 2. Настройка маршрутизатора для доступа по протоколу SSH
Часть 3. Настройка коммутатора для доступа по протоколу SSH
Часть 4. SSH через интерфейс командной строки (CLI) коммутатора

### Используемые ресурсы
1. 1 Маршрутизатор
2. 1 Коммутатор
3. 1 ПК
4. Консольные кабели и Eth кабели

### Задача 1. Настройка основных параметров устройств.
#### Шаг 1.создание сети по топологии.
#### Шаг 2.Выполняем инициализацию и ребут устройств (кроме ПК) 
#### Шаг 3. Настраиваем маршрутизатор
а. Подключаемся и заходим в Enable режим. 

b. Заходим в режим conf t

с. Выключаем поиск DNS. 

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5Rdom.PNG)

d. Назначаем пароль для enable режима. 

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5RenPass.PNG)

e. Назначаем пароль для консоли и включаем вход по паролю

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5Rdom.PNG)

f. Назначаем пароль для VTY и включаем вход по паролю

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5RvtyPass.PNG)

h. создаём баннер и даём имя. 

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5RMotd.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5Rname.PNG)

i. настраиваем и включаем интерфейс g0/0/0

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5Rnoshut_ip.PNG)

j. сохраняем конфиг. 

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5Rwrmem.PNG)

- шаг 4. Настраиваем PC-0

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5PCipdef.PNG)

- шаг 5. Проверяем подключение к сети.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5PCPing.PNG)

### Задача 2. Настраиваем маршрутизатор для доступа по SSH. 
#### Шаг 1. Настроим аунтефикацию устройств. 

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5R_domainname.PNG)

#### Шаг 2. Создадим ключ шифровавания с указанием длины. (Заодно доказываем, что мы честно смотрели запись занятия :) )

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5rsakey.PNG)

#### Шаг 3. Настраиваем пользователя

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5UserAdmin.PNG)

#### Шаг 4. Активируем SSH на VTY и сохраняем конфиг

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5VTYLoginSSH.PNG)

#### Шаг 5. Подключаемся с PC-0 по SSH к R1.

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5PC0sshconnect.PNG)

### Задача 3. Настраиваем коммутатор. 
#### Шаг 1. Используем для настройки все те же комманды, что и на роутере (кроме интерфейса. На нём включаем vlan 1 и задаем параметры исходя из таблицы) 

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5S1Secret.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5s1VTY.PNG)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5s1motd.PNG)
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5s1crypto.PNG)
![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5s1domainuser.PNG)

### Шаг 2. Устанавливаем соединение с PC-0 к S1 по SSH

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5pc0sshS1connect.PNG)

### Задача 4. Настройка протокола SSH с использованием CLI коммутатора.
#### Шаг 1. Посмотрим параметры SSH в Cisco IOS

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5s1sshparam.PNG)

#### Шаг 2. Подключимся по SSH с S1 на R1 по SSH (так эе пробуем переключение между S1 и R1 с помощью комбинации ctrl + shift + 6 + x и обратно с помощью Enter)

![](https://github.com/Despirant/Desp_Labs/blob/main/pics/l5s1sshInteresting.PNG)

## Ответ на вопрос для повторения.
Необходимо добавить имя пользователя и пароль каждого пользователя в локальную базу данных с помощью команды username. 






