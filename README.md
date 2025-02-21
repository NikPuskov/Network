# Network

# Разворачиваем сетевую лабораторию

1. Скачать и развернуть Vagrant-стенд https://github.com/erlong15/otus-linux/tree/network
2. Построить следующую сетевую архитектуру:

    Сеть office1

- 192.168.2.0/26 - dev

- 192.168.2.64/26 - test servers

- 192.168.2.128/26 - managers

- 192.168.2.192/26 - office hardware
  
  Сеть office2

- 192.168.1.0/25 - dev

- 192.168.1.128/26 - test servers

- 192.168.1.192/26 - office hardware

  Сеть central


- 192.168.0.0/28 - directors

- 192.168.0.32/28 - office hardware

- 192.168.0.64/26 - wifi

![Image alt](https://github.com/NikPuskov/Network/blob/main/image.png)

Итого должны получиться следующие сервера:

- inetRouter

- centralRouter

- office1Router

- office2Router

- centralServer

- office1Server

- office2Server

Задание состоит из 2-х частей: теоретической и практической.

В теоретической части требуется:

1. Найти свободные подсети

2. Посчитать количество узлов в каждой подсети, включая свободные

3. Указать Broadcast-адрес для каждой подсети

4. Проверить, нет ли ошибок при разбиении

В практической части требуется:

1. Соединить офисы в сеть согласно логической схеме и настроить роутинг

2. Интернет-трафик со всех серверов должен ходить через inetRouter

3. Все сервера должны видеть друг друга (должен проходить ping)

4. У всех новых серверов отключить дефолт на NAT (eth0), который vagrant поднимает для связи

5. Добавить дополнительные сетевые интерфейсы, если потребуется

---------------------------------------------------------------------------------------------

Все задания практической работы выполняются с помощью Ansible при создании виртуальных машин командой `vagrant up`

---------------------------------------------------------------------------------------------

Теоретическая часть

Создаем таблицу топологии:

Согласно таблице видим следующие свободные подсети в указаных сетях класса С:

- 192.168.0.16/28

- 192.168.0.48/28

- 192.168.0.128/25

- 192.168.255.128/25

- 192.168.255.64/26

- 192.168.255.32/27

- 192.168.255.16/28

- 192.168.255.8/29

- 192.168.255.4/30

----------------------------------------------------------------------------------------------

Практическая часть

Схема сети, которую будем настраивать:

![Image alt](https://github.com/NikPuskov/Network/blob/main/image-1.png)

На основании этой схемы получаем следующий список серверов:

- inetRouter	Default-NAT address VirtualBox

                192.168.255.1/30

- centralRouter	192.168.255.2/30

                192.168.0.1/28

                192.168.0.33/28

                192.168.0.65/26

                192.168.255.9/30

                192.168.255.5/30

- centralServer	192.168.0.2/28

- office1Router	192.168.255.10/30

                192.168.2.1/26

                192.168.2.65/26

                192.168.2.129/26

                192.168.2.193/26

- office1Server	192.168.2.130/26

- office2Router	192.168.255.6/30

                192.168.1.1/25

                192.168.1.129/26

                192.168.1.193/26

- office2Server	192.168.1.2/25

