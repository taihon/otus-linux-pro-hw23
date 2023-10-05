## OTUS Administrator Linux. Professional ДЗ №23: Сетевые пакеты. VLAN'ы. LACP

**Задание**

Для выполнения домашнего задания используйте методичку
https://docs.google.com/document/d/1BO5cUT0u4ABzEOjogeHyCaNiYh76Bh73/edit?usp=share_link&ouid=104106368295333385634&rtpof=true&sd=true

1. в Office1 в тестовой подсети появляется сервера с доп интерфесами и адресами

- в internal сети testLAN

  - testClient1 - 10.10.10.254
  - testClient2 - 10.10.10.254
  - testServer1 - 10.10.10.1
  - testServer2 - 10.10.10.1

- развести вланами
  - testClient1 <-> testServer1
  - testClient2 <-> testServer2

2. между centralRouter и inetRouter "пробросить" 2 линка (общая inernal сеть) и объединить их в бонд
3. проверить работу c отключением интерфейсов

Формат сдачи: Vagrantfile + ansible

**_Решение_**
Стенд построен с использованием vagrant и ansible.
Для развёртывания необходимо выполнить:
```
vagrant up
ansible-playbook playbook.yml
```
Для проверки работы bond во время запущенного ping 192.168.255.1 с centralRouter на inetRouter был выключен eth1. Пинг при этом не прерывался, а значит bond работает.