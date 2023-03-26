# Домашнее задание к занятию "10.1 Keepalived/vrrp" - Иванов Игорь


### Задание 1

Задание 1
Разверните топологию из лекции и выполните установку и настройку сервиса Keepalived.

```vrrp_instance test {

state "name_mode"

interface "name_interface"

virtual_router_id "number id"

priority "number priority"

advert_int "number advert"

authentication {

auth_type "auth type"

auth_pass "password"

}

unicast_peer {

"ip address host"

}

virtual_ipaddress {

"ip address host" dev "interface" label "interface":vip

}

}
```

В качестве решения предоставьте:
- рабочую конфигурацию обеих нод, оформленную как блок кода в вашем md-файле;
- скриншоты статуса сервисов, на которых видно, что одна нода перешла в MASTER, а вторая в BACKUP state.

Первая машина

```
vrrp_instance main {
state MASTER
interface enp0s3
virtual_router_id 10
priority 110
advert_int 4
authentication {
auth_type AH
auth_pass 1234
}
unicast_peer {
192.168.0.33
}
virtual_ipaddress {
192.168.0.150 dev enp0s3 label keepalived
}
}
```

![Keepalived](https://github.com/gaming4funNel/srlb-homework-10-01/blob/master/img/1machine.png)

Вторая машина

```
vrrp_instance test {
state BACKUP
interface enp0s3
virtual_router_id 11
priority 50
advert_int 4
authentication {
auth_type AH
auth_pass 1234
}
unicast_peer {
192.168.0.28
}
virtual_ipaddress {
192.168.0.150 dev enp0s3 label keepalived1
}
}
```

![Keepalived](https://github.com/gaming4funNel/srlb-homework-10-01/blob/master/img/2machine.png)


## Дополнительные задания (со звездочкой*)

### Задание 2*

Проведите тестирование работы ноды, когда один из интерфейсов выключен. Для этого:

добавьте ещё одну виртуальную машину и включите её в сеть;
на машине установите Wireshark и запустите процесс прослеживания интерфейса;
запустите процесс ping на виртуальный хост;
выключите интерфейс на одной ноде (мастер), остановите Wireshark;
найдите пакеты ICMP, в которых будет отображён процесс изменения MAC-адреса одной ноды на другой.
Пришлите скриншот до и после выключения интерфейса из Wireshark.

![Prometheus2](https://github.com/gaming4funNel/srlb-homework-9-05/blob/master/img/docker_dashboard.png)

