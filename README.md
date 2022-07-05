# network

# Задание

Задание состоит из 2-х частей: теоретической и практической.
В теоретической части требуется:
● Найти свободные подсети
● Посчитать количество узлов в каждой подсети, включая
свободные
● Указать Broadcast-адрес для каждой подсети
● Проверить, нет ли ошибок при разбиении

В практической части требуется:
● Соединить офисы в сеть согласно логической схеме и настроить
роутинг
● Интернет-трафик со всех серверов должен ходить через inetRouter
● Все сервера должны видеть друг друга (должен проходить ping)
● У всех новых серверов отключить дефолт на NAT (eth0), который
vagrant поднимает для связи
● Добавить дополнительные сетевые интерфейсы, если потребуется


# Теоретическая часть. 

![image](https://user-images.githubusercontent.com/98832702/177270645-c57ddbc3-51ab-4af0-8b6c-0f72ae0155eb.png)

![image](https://user-images.githubusercontent.com/98832702/177270708-c1458f6b-e611-4962-9f9b-942f65ddf572.png)

![image](https://user-images.githubusercontent.com/98832702/177270745-657599e6-1dbd-48d0-8266-c906aabb75e9.png)

![image](https://user-images.githubusercontent.com/98832702/177270774-8a35c62d-8352-4f65-b1d1-1cc97bfa3d8d.png)

![image](https://user-images.githubusercontent.com/98832702/177270809-39241566-336c-4d30-834e-60560a3215a4.png)

# Практическая часть

Ниже представленная схема сети 

![image](https://user-images.githubusercontent.com/98832702/177271310-0c292539-5251-4cbc-b655-dcfc2a660a95.png)

Проверяю работу после развертывания стенда командой ```vagrant up```


```
root@office2Server:~# traceroute ya.ru
traceroute to ya.ru (87.250.250.242), 30 hops max, 60 byte packets
 1  192.168.1.1 (192.168.1.1)  4.732 ms  4.386 ms  4.265 ms
 2  192.168.255.5 (192.168.255.5)  2.553 ms  2.416 ms  2.151 ms
 3  192.168.255.1 (192.168.255.1)  3.983 ms  4.780 ms  4.499 ms
 4  * * *
 5  * * *
 6  * * *
 7  * * *
 8  host-static-212-0-200-232.moldtelecom.md (212.0.200.232)  90.935 ms host-static-212-0-200-234.moldtelecom.md (212.0.200.234)  88.311 ms host-static-212-0-200-232.moldtelecom.md (212.0.200.232)  88.610 ms
 9  212-0-199-229.agg12.C-IGW-1.telco.md (212.0.199.229)  87.217 ms 212-0-200-146.agg11.C-IGW-1.telco.md (212.0.200.146)  84.949 ms 212-0-200-176.agg11.C-IGW-2.telco.md (212.0.200.176)  89.956 ms
10  ipv4.de-cix.fra.de.as208722.yandex.com (80.81.192.251)  132.639 ms  132.416 ms  131.650 ms
11  178.18.226.119.ix.dataix.eu (178.18.226.119)  175.276 ms  174.131 ms *
12  * * *
13  * * *
14  ya.ru (87.250.250.242)  177.746 ms  177.458 ms  171.416 ms
```

```
root@office1Server:~# traceroute ya.ru
traceroute to ya.ru (87.250.250.242), 30 hops max, 60 byte packets
 1  _gateway (192.168.2.129)  1.675 ms  1.561 ms  1.861 ms
 2  192.168.255.9 (192.168.255.9)  2.475 ms  4.167 ms  4.103 ms
 3  192.168.255.1 (192.168.255.1)  4.038 ms  4.506 ms  4.413 ms
 4  * * *
 5  * * *
 6  * * *
 7  * * *
 8  host-static-212-0-200-234.moldtelecom.md (212.0.200.234)  88.944 ms  88.300 ms  88.714 ms
 9  212-0-199-229.agg12.C-IGW-1.telco.md (212.0.199.229)  88.618 ms  91.712 ms  91.457 ms
10  * * *
11  * 178.18.226.119.ix.dataix.eu (178.18.226.119)  170.673 ms *
12  * * sas-32z3-ae1.yndx.net (87.250.239.183)  171.049 ms
13  * * ya.ru (87.250.250.242)  173.874 ms
```

```
[root@centralServer ~]# traceroute ya.ru
traceroute to ya.ru (87.250.250.242), 30 hops max, 60 byte packets
 1  gateway (192.168.0.1)  0.793 ms  0.596 ms  0.495 ms
 2  192.168.255.1 (192.168.255.1)  1.187 ms  1.956 ms  2.266 ms
 3  * * *
 4  * * *
 5  * * *
 6  host-static-212-0-219-242.moldtelecom.md (212.0.219.242)  71.981 ms host-static-212-0-219-240.moldtelecom.md (212.0.219.240)  72.556 ms  72.467 ms
 7  host-static-212-0-200-234.moldtelecom.md (212.0.200.234)  72.077 ms host-static-212-0-200-232.moldtelecom.md (212.0.200.232)  71.842 ms  71.425 ms
 8  212-0-200-176.agg11.C-IGW-2.telco.md (212.0.200.176)  71.396 ms  71.009 ms 212-0-199-229.agg12.C-IGW-1.telco.md (212.0.199.229)  71.645 ms
 9  * * *
10  vla-32z3-ae1.yndx.net (93.158.172.21)  151.852 ms 178.18.226.119.ix.dataix.eu (178.18.226.119)  157.354 ms  151.337 ms
11  sas-32z3-ae2.yndx.net (87.250.239.185)  156.944 ms vla-32z3-ae1.yndx.net (93.158.172.21)  157.883 ms vla-32z1-ae2.yndx.net (93.158.172.19)  182.758 ms
12  * * *
13  ya.ru (87.250.250.242)  152.070 ms  150.976 ms  155.492 ms
```

Проверяю доступность других серверов с office2Server

```
root@office2Server:~# traceroute 192.168.2.130
traceroute to 192.168.2.130 (192.168.2.130), 30 hops max, 60 byte packets
 1  192.168.1.1 (192.168.1.1)  1.123 ms  1.400 ms  1.139 ms
 2  192.168.255.5 (192.168.255.5)  1.363 ms  1.962 ms  1.891 ms
 3  192.168.255.10 (192.168.255.10)  3.265 ms  4.167 ms  3.579 ms
 4  192.168.2.130 (192.168.2.130)  3.582 ms  3.819 ms  3.685 ms
 
root@office2Server:~# traceroute 192.168.0.2
traceroute to 192.168.0.2 (192.168.0.2), 30 hops max, 60 byte packets
 1  192.168.1.1 (192.168.1.1)  1.179 ms  0.912 ms  0.960 ms
 2  192.168.255.5 (192.168.255.5)  2.730 ms  2.632 ms  2.538 ms
 3  192.168.0.2 (192.168.0.2)  4.153 ms  4.016 ms  3.911 ms
```

C office1Server

```
traceroute to 192.168.1.2 (192.168.1.2), 30 hops max, 60 byte packets
 1  _gateway (192.168.2.129)  1.076 ms  0.887 ms  0.633 ms
 2  192.168.255.9 (192.168.255.9)  0.796 ms  0.676 ms  1.296 ms
 3  192.168.255.6 (192.168.255.6)  3.230 ms  3.116 ms  2.980 ms
 4  192.168.1.2 (192.168.1.2)  2.799 ms  2.683 ms  2.625 ms
 
root@office1Server:~# traceroute 192.168.0.2
traceroute to 192.168.0.2 (192.168.0.2), 30 hops max, 60 byte packets
 1  _gateway (192.168.2.129)  1.200 ms  1.106 ms  0.919 ms
 2  192.168.255.9 (192.168.255.9)  2.534 ms  2.529 ms  2.809 ms
 3  192.168.0.2 (192.168.0.2)  3.143 ms  4.135 ms  4.204 ms
```

C centralServer

```
[root@centralServer ~]# traceroute 192.168.2.130
traceroute to 192.168.2.130 (192.168.2.130), 30 hops max, 60 byte packets
 1  gateway (192.168.0.1)  0.487 ms  0.351 ms  0.369 ms
 2  192.168.255.10 (192.168.255.10)  1.336 ms  1.053 ms  0.887 ms
 3  192.168.2.130 (192.168.2.130)  2.143 ms  3.605 ms  3.536 ms
 
[root@centralServer ~]# traceroute 192.168.1.2
traceroute to 192.168.1.2 (192.168.1.2), 30 hops max, 60 byte packets
 1  gateway (192.168.0.1)  0.872 ms  0.731 ms  0.864 ms
 2  192.168.255.6 (192.168.255.6)  1.636 ms  1.101 ms  1.271 ms
 3  192.168.1.2 (192.168.1.2)  1.475 ms  1.547 ms  1.544 ms
```
