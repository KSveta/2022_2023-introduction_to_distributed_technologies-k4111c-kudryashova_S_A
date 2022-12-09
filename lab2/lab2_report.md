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

### 1. Создание deployment и сервиса <br>
```bash
kubectl apply -f lab2.yaml
```

![image](https://user-images.githubusercontent.com/113091328/206441576-3f13daa9-56f6-4977-8a53-0d06316f9788.png)

Проверка создания подов: <br>

![image](https://user-images.githubusercontent.com/113091328/206486413-ec3d906c-4899-43f8-a384-2b1091facb16.png)

Проверка создания сервиса: <br>

![image](https://user-images.githubusercontent.com/113091328/206486579-407e6d76-f9f7-4987-86e7-a8b71ce8b69b.png)

### 2. Подключение через веб-браузер <br>
Для работы выбран тип сервиса LoadBalancer. Подключение к контейнеру происходит через сервис, данную процедуру можно выполнить с помощью следующей команды: 

![image](https://user-images.githubusercontent.com/113091328/206241643-f89033a2-2867-419d-8e38-2ff5b07f5f6f.png)

### 3. Проверка на странице в веб браузере переменных <br>

![image](https://user-images.githubusercontent.com/113091328/206498783-f9b17ae3-a143-4583-8693-417efab29503.png)


![image](https://user-images.githubusercontent.com/113091328/206498929-f3cfd4b2-7013-4237-acee-6644944b8c10.png)


Поля REACT_APP_USERNAME и REACT_APP_COMPANY_NAME остаются не изменными, поскольку это константы, указанные в манифесте, а поле Container name изменяется, т.к. сервис распределяет запросы между двумя репликами. <br><br>

### 4. Логи контейнеров

![image](https://user-images.githubusercontent.com/113091328/206489632-5cf5820f-7dd6-4dec-8aba-46b831bf4e19.png)


### 5. Схема организации сервисов и контейнеров

![image](https://user-images.githubusercontent.com/113091328/206490611-ccccac12-4110-4d1b-836c-3e5393b77b05.png)



