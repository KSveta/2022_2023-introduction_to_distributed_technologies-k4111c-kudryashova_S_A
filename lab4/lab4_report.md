University: [ITMO University](https://itmo.ru/ru/) <br>
Faculty: [FICT](https://fict.itmo.ru) <br>
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies) <br>
Year: 2022/2023 <br>
Group: K4111c <br>
Author: Kudryashova Svetlana Andreevna <br>
Lab: Lab4 <br>
Date of create: 10.12.2022 <br>
Date of finished:  <br>

## Цель работы <br>
Познакомиться с CNI Calico и функцией IPAM Plugin, изучить особенности работы CNI и CoreDNS.<br>
<br>

## Ход работы <br>

### 1. Создание кластера

- Создание кластера с двумя нодами <br>
``` bash
minikube start --nodes 2 --cni calico --kubernetes-version=v1.24.3
```
NetworkPolicies — это ориентированная на приложение конструкция, которая позволяет указать, какс Pod разрешено взаимодействовать  с различными сетевыми «сущностями» <br>
CNI ( Container Network Interface ), проект Cloud Native Computing Foundation , состоит из спецификации и библиотек для написания плагинов для настройки сетевых интерфейсов в контейнерах Linux, а также ряда поддерживаемых плагинов. <br>
Calico — это сетевое решение и решение для обеспечения безопасности для контейнеров, виртуальных машин и собственных рабочих нагрузок на основе хоста. <br>

- Проверка создания nodes<br>

![image](https://user-images.githubusercontent.com/113091328/206856845-a4fc7414-4a9c-425f-b9b9-81f301b60d5f.png)

- Проверка всех pod'ов <br>

![image](https://user-images.githubusercontent.com/113091328/206856894-332e8f67-9d6d-4025-ae65-be7551866ed1.png)

- Проверка статуса nodes<br>

![image](https://user-images.githubusercontent.com/113091328/206856939-9e0ab690-2553-42ff-9ed2-a089477cf689.png)

- Создание Calico pod
``` bash
kubectl apply -f calico_ctl.yaml
```
![image](https://user-images.githubusercontent.com/113091328/206857014-ee3a8222-bc86-454a-8387-2cdda593e569.png)

### 2. Создание IP-Pool и replicaset

- Создание ippool
``` bash
kubectl exec -i -n kube-system calicoctl -- /calicoctl create -f - < ip_pool.yaml
```
- Проверим созданные ippools
``` bash
kubectl exec -i -n kube-system calicoctl -- /calicoctl get ippools -o wide
```
![image](https://user-images.githubusercontent.com/113091328/206857086-5977fcd9-15e1-42f2-89b9-efbf0c0c18b3.png)

- Удаляем default ippool
``` bash
kubectl exec -i -n kube-system calicoctl -- /calicoctl delete ippools default-ipv4-ippool
```

- создание configMap <br>
`kubectl apply -f lab4-configmap.yaml` <br>

ConfigMap — это объект API, используемый для хранения неконфиденциальных данных в парах ключ-значение.<br>
Использование ConfigMaps позволяет разделять конфигурационные файлы и контейнеры с приложениями.<br>

- создание replicaset <br>
`kubectl apply -f lab4-replicaset.yaml` <br>
Цель ReplicaSet — поддерживать стабильный набор подов реплик, работающих в любой момент времени. Таким образом, он часто используется, чтобы гарантировать доступность определенного количества идентичных подов.<br>

- создание service <br>
`kubectl apply -f lab4-service.yaml`  <br>
В Kubernetes сервис — это абстракция, определяющая политику доступа к подам <br>

### 3. Проверка на странице в веб браузере переменных Container name и Container IP

![image](https://user-images.githubusercontent.com/113091328/206857362-2fab9e81-652a-4446-8a9d-f68708448a38.png)

![image](https://user-images.githubusercontent.com/113091328/206857373-60eed3a9-e7e4-4a30-96aa-d351cb218df0.png)

Обновив страницу произошло изменение полей "Container name" и "Container IP" т.к. сервис распределяет нагрузку межу существующими репликами <br>

### 4. Результаты пингов

![image](https://user-images.githubusercontent.com/113091328/206857517-eef5c674-b0d9-42da-a733-6ddd7b8168b5.png)

![image](https://user-images.githubusercontent.com/113091328/206857547-1b74610c-d433-4f77-b508-5f3dad8ccf01.png)
