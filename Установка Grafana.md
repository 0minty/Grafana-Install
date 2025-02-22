![image](https://github.com/user-attachments/assets/68b2f3e5-09c6-4895-92d8-3e5575a0210e)# LAB1_Установка Docker на Oracle Linux
1. Начал с установки пакета <b>wget</b>, используя команду ```sudo yum install wget```, данный пакет даёт возможность загружать файлы из интернета
   
   ![image](https://github.com/user-attachments/assets/81ffa714-132f-4ade-89b9-d72be8018ce7)
   
2. Следом установил пакет <b>curl</b> ```sudo yum install curl```,данный пакет даёт возможность отправлять HTTP/HTTPS запросы
   
   ![image](https://github.com/user-attachments/assets/d89019b2-3053-4320-b829-f730576085a5)
   
3. Копирую репозиторий докера, для того чтобы его потом установить, используя <b>wget</b> используя тег <b>-P</b> для чтения <br>```sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo```

   ![image](https://github.com/user-attachments/assets/34eb77ad-9b3d-42e6-93e8-d96f9e72dce9) 
   
4. C помощью пакета <b>yum</b> устанавливаем докер из копированного репозитория выше <br>```sudo yum install docker-ce docker-ce-cli containerd.io```
   
   ![image](https://github.com/user-attachments/assets/245c96d4-816b-479b-bad7-d0914e037cc0)
   ![image](https://github.com/user-attachments/assets/7ec33469-db1f-4f1f-87f7-0c336141fca6)

   
5. Запускаем докер используя команду ```sudo systemctl enable docker --now``` эта команда добавляет doker в список служб, которые запустятся при запуске ОС
   
   ![image](https://github.com/user-attachments/assets/a416064c-9e96-41c6-a73f-e7820770ad1b) 

6. Получаем последнюю версию Docker Compose, используя команду
 ```COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)```

   ![image](https://github.com/user-attachments/assets/07c35729-1e88-40ae-a452-22e4c9bfe71f)

7. Скачиваем и устанавливаем последнюю версию Docker Compose с помощью команды
 ```sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose```

   ![image](https://github.com/user-attachments/assets/fe059437-964a-4739-8966-8467dc0db459)

8. Устанавливаем права на выполнение (делает файл исполняемым) ```sudo chmod +x /usr/bin/docker-compose```

    ![image](https://github.com/user-attachments/assets/8fcc8dca-8c0c-4fd3-b6ca-06eb3fc6e376)
    
9. Проверяем установленную версию docker c помощью команды ```docker --version```

    ![image](https://github.com/user-attachments/assets/9d17ca47-20e1-4579-aa5a-f2c2f30c02d8)

10. Клонируем репозиторий с github, где содержится Grafana с помощью команды
```git clone https://github.com/skl256/grafana_stack_for_docker.git```

      ![image](https://github.com/user-attachments/assets/aadb5c9c-c6be-48fc-9326-31f590c73be2)

11. Переходим в директорию с Grafana с помощью команды ```cd grafana_stack_for_docker```

    ![image](https://github.com/user-attachments/assets/58545aab-32c5-4801-9365-505eeb3c8139)
    
12. Создаем директории для файлов Grafana с помощью команд ```sudo mkdir -p /mnt/common_volume/swarm/grafana/config
sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}```

   ![image](https://github.com/user-attachments/assets/72dc29ae-7572-4993-afee-c4667490c172)

13. Изменяем владельца на текущего пользователя с помощью
```sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}```

   ![image](https://github.com/user-attachments/assets/8703ff56-fdc6-434c-83db-f8a59f1e6887)

14. Создаем файл конфигурации с помощью команды ```touch /mnt/common_volume/grafana/grafana-config/grafana.ini``` 

   ![image](https://github.com/user-attachments/assets/7b72a4f2-2ae0-4cea-8531-b36f7c1ea008)

15. Копируем все файлы из директории config в /mnt/common_volume/swarm/grafana/config/ c помощью команды ```cp config/* /mnt/common_volume/swarm/grafana/config/```

   ![image](https://github.com/user-attachments/assets/e41ca8ae-93c1-4e28-b917-c2979218ccee)

16. Переименовываем файл grafana.yaml в docker-compose.yaml ```mv grafana.yaml docker-compose.yaml```

   ![image](https://github.com/user-attachments/assets/c8511cdc-1265-4e87-bfa9-80800ac768df)

17. Запускаем Docker Compose в фоновом режиме с помощью ```sudo docker compose up -d```

   ![image](https://github.com/user-attachments/assets/5a1912c5-a57b-4fda-a3b0-0c9dea99988c)

    Успешный запуск
   
   ![image](https://github.com/user-attachments/assets/5918f777-d8dd-4be0-8749-9a3d121af245)


18. Открываем браузер и переходим по адресу <b>localhost:3000</b>

   ![image](https://github.com/user-attachments/assets/e06e15eb-3739-4540-b24c-e90f279cefed)

   <b>Вводим логин и пароль<br>
      Логин: admin<br>
      Пароль: admin</b>

19.  Попадаем на страницу Home

   ![image](https://github.com/user-attachments/assets/1cc82851-0cf6-4d1e-9be3-536c447bf71b)

20. Заходим в конфигурационный файл докера с помощью команды ```vi docker-compose.yaml```

    ![image](https://github.com/user-attachments/assets/cb969c40-8734-4f67-8e69-5ed9096bf237)

    ![image](https://github.com/user-attachments/assets/0b1e6b93-8d72-48f9-8bea-bf7393c37ba6)

21. Выходим с конфигурационного  вписав команду ```:wq```

    ![image](https://github.com/user-attachments/assets/fc1388f9-457d-44bb-be68-12fab8454c46)

22. Переходим в директорию с конфигурационным файлом используя команду
    ```cd grafana_stack_for_docker```

    ![image](https://github.com/user-attachments/assets/5d60d570-cab0-4167-a53b-26b75df3976e)

23. Запускаем grafana используя команду
    ```sudo docker compose up -d```

    ![image](https://github.com/user-attachments/assets/eb3b7e29-3a9e-4f5e-acf1-d12f51f13d14)
    
    ![image](https://github.com/user-attachments/assets/9bbc38c1-f050-4d28-a039-0ea7c9764549)


25. Выполняем остановку grafana вписав команду
    ```sudo docker compose stop```
    ![image](https://github.com/user-attachments/assets/25c8a171-087a-4a6b-ae4c-848d512dd7f1)

26. Полностью останавливаем grafana используя команду
    ```sudo docker compose down```

    ![image](https://github.com/user-attachments/assets/773efa09-d67c-4e03-a723-b09c2544b247)








