University: [ITMO University](https://itmo.ru/ru/) <br>
Faculty: [FICT](https://fict.itmo.ru) <br>
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies) <br>
Year: 2022/2023 <br>
Group: K4111c <br>
Author: Kudryashova Svetlana Andreevna <br>
Lab: Lab1 <br>
Date of create: 10.11.2022 <br>
Date of finished: <br>
<br>
## Цель работы <br>
Ознакомиться с инструментами Minikube и Docker, развернуть свой первый "под".<br>
<br>
## Ход работы<br>
1. Манифест для развертывания "пода"<br>
![image](https://user-images.githubusercontent.com/113091328/205375421-8c289eac-bd94-4b04-af46-c650bb762e31.png)

   Команда для создание пода <br> 
   
   ![image](https://user-images.githubusercontent.com/113091328/205431319-72302beb-9997-4143-98e5-0de02e6b70fe.png)

<br>
2. Создание сервиса для доступа к контейнеру vault <br>
Указываем тип сервиса NodePort. Он отвечает за доступ к нашим ресурсам извне (из других Nodes) <br>
Сервис создается для пода vault , который обслуживает порт 8200 <br>
 <br>
3. Команда позволяет прослушать порт на localhost и перенаправить на порт 8200 в кластере:<br>
 <br>
 4. Команда kubectl logs позволяет просматривать логи пода. Находим токен для входа. <br>
 <br>
 
 ## Cхема организации сервисов и контейнеров <br>
 
![image](https://user-images.githubusercontent.com/113091328/205427042-a77d77bd-1897-4915-a85f-8e6d340ba12d.png)

