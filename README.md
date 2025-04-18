<b>Архитектура системы мониторинга с использованием Prometheus, Grafana, Alertmanager и Victoria Metrics</b>

![image](https://github.com/user-attachments/assets/7b905a66-83fe-4096-a68e-7d5168d7b371)

Схема мониторинга сервисов с Prometheus, Alertmanager и Victoria Metrics, включающая сбор метрик через Node Exporter, хранение данных, визуализацию в Grafana и отправку уведомлений через Telegram и e-mail. Развёртывание выполнено с помощью Docker Compose


# Установка Docker на Oracle Linux
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

# Prometheus

- копирую конфигурационные файлы с github командой 

   - ```sudo git clone https://github.com/0minty/Grafana-Install.git```

   ![image](https://github.com/user-attachments/assets/54d81523-a681-4ad0-9f9b-7a482e25c670)

- проверяем что репозиторий успешно установился
  - используем команду ```ls```
    
   ![image](https://github.com/user-attachments/assets/3dc94a69-4af0-42b3-b02b-a2da37696138)

- копируем конфигурационный файл докера в папку с Grafan
   - используя команду ```cp docker-compose.yaml /home/fedor/grafana_stack_for_docker/```

  ![image](https://github.com/user-attachments/assets/f785d2ab-92c4-4bd2-a40f-720f8513494d)

- тоже самое делаем для конфигурационного файла prometheus
  - используя команду ```cp prometeus.yaml /home/fedor/grafana_stack_for_docker/```

  ![image](https://github.com/user-attachments/assets/b0667efa-214a-42d2-9309-d587afa18741)

- переименовываем конфигурационный файл с <b>prometeus.yaml</b> на <b>prometheus.yaml</b> (в нем содержалась ошибка в названии)
   - используя команду ```mv prometeus.yaml prometheus.yaml```

  ![image](https://github.com/user-attachments/assets/60fb8b46-5b4f-4bc1-8304-2234853bbdbf)

- переносим конфигурационный файл prometheus.yaml в конфиг Grafana
   - используя команду ```mv prometheus.yaml /mnt/common_volume/swarm/grafana/config```

  ![image](https://github.com/user-attachments/assets/19e754b0-0ad2-45f3-b6a9-64961059c518)

   - проверяем наличие файла
     - используя команду ```ls```
       
     ![image](https://github.com/user-attachments/assets/1a9824a7-e572-4fbb-9cb0-c4219961b0b1)

- запускаем docker compose в фоновом режиме
   - используя команду ```sudo docker compose up -d```

   ![image](https://github.com/user-attachments/assets/2a211f58-898e-45b0-8718-7776d008d7ed)


- переходим на сайт ```localhost:3000```
   - User & Password GRAFANA: ```admin```
   - Код графаны: ```3000```
   - Код прометеуса: ```http://prometheus:9090```

- в меню выбираем вкладку Dashboards и создаем Dashboard
   - жмем кнопку +Add visualization, а после "Configure a new data source"
   - выбираем Prometheus
     
     ![image](https://github.com/user-attachments/assets/ed2b6346-c9cd-4086-ac71-c84650a6f264)
   
   - Заполняем данные в открывшемся окне
      
      - Пункт  Connection
         - ```http://prometheus:9090```

      - Пункт Authentication
         - Basic authentication
         - User: ```admin```
         - Password: ```admin```
         - Нажимаем на Save & test и должно показывать зелёную галочку

- в меню выбираем вкладку Dashboards и создаем Dashboard
   - жмем кнопку "Import dashboard"
     
     ![image](https://github.com/user-attachments/assets/59b75269-46b6-4bdb-a7b1-c9c605cc7467)

   - В пункт ```Find and import dashboards for common applications at grafana.com/dashboards:```
      - вписываем ```1860```
        
        ![image](https://github.com/user-attachments/assets/ecdcf92e-4373-4477-a5ed-4249f97cb7fa)
        
      - жмем кнопку Load
   - Select Prometheus ждем кнопку "Import"

В итоге открывается такой Dashboard для мониторинга загрузки ОС

![image](https://github.com/user-attachments/assets/9f3b951e-21ec-4236-ab8a-357cfe85efbd)


# Victoria

- Вводим команду ```echo -e "# TYPE light_metric1 gauge\nlight_metric1 0" | curl --data-binary @- http://localhost:8428/api/v1/import/prometheus``` которая, отправляет бинарные данные (например, метрики в формате Prometheus) на локальный сервер, который слушает на порту 8428.
  
   ![image](https://github.com/user-attachments/assets/56ab401f-7312-41a0-9537-d40299d24bfa)

- Переходим в браузере по ссылке ```http://localhost:8428/```, открывается такое меню в нём нужно выбрать <b>vmui</b>

   ![image](https://github.com/user-attachments/assets/a66e3e16-667e-4577-946a-f2b27bea69ec)

- Вписываем <b>light_metric1</b> и нажимаем <b>Execute Query</b>

  ![image](https://github.com/user-attachments/assets/34cc95dc-826d-4fdd-a3bb-bcec0918aa33)

- Переходим на ```http://localhost:3000``` выбираем Dashboard и нажимаем <b>New Dashboard</b>, далее <b>Add Visualization</b>

  ![image](https://github.com/user-attachments/assets/83076396-3e13-4036-a3f4-67d7aa6d05f1)

- Нажимаем <b>Configure a new data source</b> и выбираем Prometheus

  ![image](https://github.com/user-attachments/assets/44e63d6a-6c24-4348-be0a-1f754c22f3d8)

- Вписываем:
   - Name: vik
   - Connection: ```http://victoriametrics:8428```
   - Нажимаем <b>Save & Test</b>
 
     ![image](https://github.com/user-attachments/assets/27099002-c2b2-4b1f-8592-604e02ffd3ec)
     

- Вписываем <b>light_metric1</b>

  ![image](https://github.com/user-attachments/assets/69c43e8f-5df8-4dfd-8a0a-1aa511ac310c)

- Выходит панель с графиком, где есть активность <b>light_metric1</b>

![image](https://github.com/user-attachments/assets/79bc6beb-9d7d-4394-a31f-70213ba14cd9)

# Alert Manager

![image](https://github.com/user-attachments/assets/a83e1a63-bc09-4683-abee-76dfa64136f0)

![image](https://github.com/user-attachments/assets/529184ed-a90a-4b87-b588-c33b1e21fc49)



