## Домашнее задание VLAN и LACP

### Описание домашнего задания
```
в Office1 в тестовой подсети появляется сервера с доп интерфесами и адресами
в internal сети: 
- testClient1 - 10.10.10.254
- testClient2 - 10.10.10.254
- testServer1- 10.10.10.1 
- testServer2- 10.10.10.1
Равести вланами:
testClient1 <-> testServer1
testClient2 <-> testServer2

Между centralRouter и inetRouter "пробросить" 2 линка (общая inernal сеть),
объединить их в бонд, проверить работу c отключением интерфейсов

VMs разворачиваются в среде VMware vSphere 7

Файлы:

- network_scheme.pdf:     заданная схема сети
- network.yml:            ansible playbook настройки VMs
- servers.yml             include файл, playbook развертывания VMs
- vars.yml:               переменные для создания VMs в VMware vSphere 7
- host:                   inventory
- protocol.pdf            проверка работы       

Каталог conf:
  office1Router
- ifcfg-vlan2:            /etc/sysconfig/network-scripts/ifcfg-vlan2
                          настройка интерфейса vlan2
- ifcfg-vlan3:            /etc/sysconfig/network-scripts/ifcfg-vlan3
                          настройка интерфейса vlan3
  inetRouter         
- route-bond0:            /etc/sysconfig/network-scripts/route-bond0
                          роутинг до 10.10.0.0/16
  centralRouter
- route-ens161:           /etc/sysconfig/network-scripts/route-ens161
                          роутинг до 10.10.0.0/16
- route-ens192:           роутинг до PC управления

Каталог templates:
  testClient2, testServer2
- 50-cloud-init.yaml.j2:  шаблон настройки сетевого интерфейса c vlan
                          для Ubuntu Server 22.04
  testClient1, testServer1
- ifcfg-vlan.j2:          шаблон настройки сетевого интерфейса c vlan
                          для Centos 8 Stream
  inetRouter,centralRouter
- ifcfg-bond0.j2:         шаблон настройки bond интерфейса
- ifcfg-ens224:           интерфейс 1 bond интерфейса
- ifcfg-ens256:           интерфейс 2 bond интерфейса
