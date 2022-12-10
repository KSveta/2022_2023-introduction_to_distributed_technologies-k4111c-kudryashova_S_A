University: [ITMO University](https://itmo.ru/ru/) <br>
Faculty: [FICT](https://fict.itmo.ru) <br>
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies) <br>
Year: 2022/2023 <br>
Group: K4111c <br>
Author: Kudryashova Svetlana Andreevna <br>
Lab: Lab2 <br>
Date of create: 6.12.2022 <br>
Date of finished: 8.12.2022 <br>

## Цель работы <br>
Ознакомиться с типами "контроллеров" развертывания контейнеров, ознакомится с сетевыми сервисами и развернуть свое веб приложение.<br>
<br>
## Ход работы<br>
### 1. Создание компонентов 
- configMap<br>
`kubectl apply -f lab3-configmap.yaml`<br>
ConfigMap — это объект API, используемый для хранения неконфиденциальных данных в парах ключ-значение.<br>
Использование ConfigMaps позволяет разделять конфигурационные файлы и контейнеры с приложениями.<br>

- replicaset<br>
`kubectl apply -f lab3-replicaset.yaml`<br>
Цель ReplicaSet — поддерживать стабильный набор подов реплик, работающих в любой момент времени. Таким образом, он часто используется, 
чтобы гарантировать доступность определенного количества идентичных подов.<br>

- service<br>
`kubectl apply -f lab3-service.yaml`<br>
В Kubernetes сервис — это абстракция, определяющая политику доступа к подам <br>

### 2.TLS сертификат
- Генерируем TLS сертификат<br>
`openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout tls.key -out tls.crt -subj "/CN=kudryashovalab3.com" -days 365`<br>
req — это генерация запросов на подпись сертификата, но если мы задаём ключ «-x509», это означает, что мы генерируем самоподписанный сертификат.<br>
Опция -newkey указывает, что нужно создать новую пару ключей, а в параметрах мы сообщаем тип rsa и сложность 4096 байт. <br>
Опция -nodes указывает, что шифровать ключ не нужно.<br>
-keyout - указываем в какой файл положим ключ.<br>
Опция -out указывает на имя файла для сохранения сертификата<br>
-subj — этот тот кому принадлежит сертификат<br>
С помощью параметра -days мы указываем что сертификат будет действительным в течение 365 дней<br>

- Создание Secret<br>
`kubectl create secret tls lab3-tls --cert=tls.crt --key=tls.key`<br>

### 3. Создание ingress
Ingress — это объект API, который определяет правила, разрешающие внешний доступ к сервисам в кластере.<br><br>

- Используем команду<br>
`kubectl apply -f lab3-ingress.yaml`<br>

- Конфигурирем minikube для работы с ingress<br>
`minikube addons enable ingress` <br>
`minikube addons enable ingress-dns` <br>

-  добавляем IP адрес ingress и FQDN (127.0.0.1 kudryashovalab3.com) в дирикторию C:\Windows\System32\drivers\etc<br>

- для доступа к ingress используем команду<br>
`minikube tunnel`<br>

### 4. Результат 

![image](https://user-images.githubusercontent.com/113091328/206838508-a4be1769-6a59-4cf6-a4f8-ca08595aee79.png)

Проверка сертификата <br>
![image](https://user-images.githubusercontent.com/113091328/206838446-fdd0b1ea-16de-4171-83f5-16b42de05de7.png)

### 5. Схема организации сервисов и контейнеров 

![image](https://user-images.githubusercontent.com/113091328/206839252-343ad14c-8af9-49ef-848d-4a4187b4e65c.png)
